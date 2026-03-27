# Hawker Boys — Developer Handoff

This document is for the developer building the production version of the Hawker Boys app alongside Claude and the product owner. It covers the current codebase architecture, what Claude has built and why, where the demo intentionally cuts corners, what the planned features actually require to build properly, and open decisions that need a developer's judgment.

---

## Context

The product owner is not a developer. Claude (AI) has been building the demo iteratively through conversation — filling in logic, data, and UI as requirements are clarified verbally. The demo is functional and deployed but is a prototype, not production software. Your role is to:

1. Convert the demo's architecture into a scalable, maintainable production codebase
2. Implement features that Claude cannot build alone (backend, auth, multi-role access, real-time data, native device features)
3. Close gaps where Claude's outputs needed better prompting or where the AI hit a capability ceiling
4. Be the technical decision-maker on stack, infra, and architecture

Claude will continue to build UI components, data structures, and logic. You and Claude are co-contributors — Claude handles the front-end React and content layer; you own the backend, architecture, and anything requiring persistent infrastructure.

---

## Current Codebase

### Overview

The entire app is a single file: `index.html` — 2,784 lines of HTML, CSS, and a `<script type="text/babel">` block containing all React components and data. There is no build step, no bundler, no package.json.

**This is intentional for the demo** — it allows rapid iteration via Claude without a development environment. The production app should be a proper React project.

### Dependencies (all CDN, no npm)

| Library | Version | Purpose |
|---------|---------|---------|
| React | 18 | UI framework |
| ReactDOM | 18 | DOM rendering |
| Recharts | 2.5.0 | Cost Engine 6-year projection chart |
| Tailwind CSS | CDN | Utility styling |
| Babel Standalone | latest | JSX transpilation in-browser |
| DM Sans / DM Mono / Inter / Press Start 2P | Google Fonts | Typography |

> **Note:** Babel Standalone in-browser transpilation is fine for demos but adds ~2MB of client-side JS. Production should use a proper build pipeline (Vite recommended).

### File Structure (inside `index.html`)

All code lives inside a single `<script type="text/babel">` starting at line 125. Sections are delineated by banner comments:

```
Line 129  // ─── Constants & Data
Line 147  function loadState()           — localStorage read with fallback to DEFAULT_STATE
Line 154  function saveState()           — localStorage write
Line 158  function isToolUnlocked()      — returns true (all tools unlocked in demo)
Line 175  function toolUnlockRequirement() — maps toolId to required stage (dormant in demo)
Line 188  function stateReducer()        — all state mutations
Line 224  // ─── Quiz Data              — 10 quiz questions array
Line 238  // ─── Business Tool Data     — VENUES[], RECIPES[], TIPS[], EQUIPMENT[], GRANTS[]
Line 305  // ─── AI                     — AI_CONFIG persona map + callAI() fetch function
Line 323  function findCanned()          — canned response matching (fallback when no API key)
Line 350  // ─── SVG Icon Components    — ~30 inline SVG icon components
Line 654  // ─── Shared UI Helpers      — PbarTrack, LBadge, LCard, ToolPanel shell
Line 691  // ─── Celebration Modal
Line 715  // ─── Quiz Component
Line 815  // ─── COST ENGINE            — calcCosts() + CostEngine component
Line 930  // ─── CULINARY MODULE
Line 977  // ─── STALL FINDER
Line 1008 // ─── TENDER MODULE
Line 1032 // ─── OPERATIONS MODULE
Line 1058 // ─── INSIDER TIPS MODULE
Line 1082 // ─── BUSINESS MODULE
Line 1095 // ─── RECIPE BOOK DATA       — RECIPE_BOOK[] array, 23 dishes (~1,000 lines)
Line 2100 // ─── RECIPE BOOK MODULE     — RecipeBook() component
Line 2303 // ─── TOOL DEFINITIONS       — TOOLS[] array wiring components to nav
Line 2315 // ─── SCREENS
Line 2317 function HomeScreen()
Line 2416 function PathwayScreen()
Line 2497 function AIScreen()
Line 2588 function ToolsScreen()
Line 2631 function ProfileScreen()
Line 2700 function App()                — root component, tab routing, nav bar
Line 2780 ReactDOM.createRoot(...)      — mount point
```

### State Management

App state is managed with `useReducer`. The reducer (`stateReducer`, line 188) handles:

| Action | Effect |
|--------|--------|
| `ADD_XP` | Increments XP, triggers level-up if threshold crossed |
| `COMPLETE_STAGE` | Advances stage, unlocks tools, fires celebration |
| `COMPLETE_MILESTONE` | Marks a milestone complete, adds XP |
| `UPDATE_COST_PARAMS` | Updates Cost Engine parameters |
| `SET_API_KEY` | Stores Claude API key in state |
| `SET_STREAK` | Updates daily streak on app open |

State is persisted to `localStorage` under key `hb_v1` on every dispatch. On load, `loadState()` merges stored state with `DEFAULT_STATE` — this means adding new keys to `DEFAULT_STATE` won't break existing users.

**Production implication:** `localStorage` is fine for a demo but has no cross-device sync, no server-side record, and no audit trail. Production state must live in a database.

### AI Integration

The AI is Claude (Anthropic) accessed via a Cloudflare Workers proxy. The relevant code is at line 305.

```js
// AI_CONFIG maps stage number to persona name + system prompt
const AI_CONFIG = { 1: {...}, 2: {...}, 3: {...}, 4: {...} }

// callAI() posts to the Cloudflare Worker endpoint
async function callAI(messages, stagePersona) {
  const res = await fetch('https://hawkerboysappdemo.jarogee.workers.dev/api/chat', {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify({ messages, system: stagePersona.systemPrompt })
  });
  ...
}
```

The Cloudflare Worker (`wrangler.jsonc`) is currently configured as a static asset host. **The `/api/chat` route does not yet exist as a Worker function** — this endpoint needs to be built. See the AI Backend section below.

**Fallback:** `findCanned()` (line 323) matches keywords in the user's message and returns a pre-written response if no API key or Worker endpoint is available. This is how the demo AI works without a live backend.

### Tool Unlock System

`isToolUnlocked()` at line 158 currently returns `true` unconditionally — all tools are unlocked in the demo. The real unlock logic is in `toolUnlockRequirement()` at line 175, which maps each tool to a required stage. To restore gated unlocks in production, remove the `return true` override.

---

## What Needs to Be Built

The following planned features cannot be fully delivered by Claude alone. Each requires backend infrastructure, and several require architectural decisions that are yours to make.

---

### 1. Authentication & Multi-Role Access

**The gap:** The demo has no auth. Everyone sees the same trainee view (Ahmad R., Stage 1). Production needs six distinct authenticated roles: Trainee, Trainer, Employer, Counsellor, Administrator, Authority.

**What it requires:**
- Auth provider: **Supabase Auth** recommended (email/password + magic link + optional SSO for Authority users)
- Row-Level Security in the database — each user role sees only what they're permitted to see
- Role assignment managed by Administrators
- Session token handling in the React app

**Role-specific views (summary):**

| Role | Portal Type | Key Data Access |
|------|-------------|-----------------|
| Trainee | Mobile app (current demo) | Own profile, own stage, own calendar |
| Trainer | Mobile or tablet web | Assigned trainees' progress, milestone verification |
| Employer | Web portal | Placed trainees' schedules, attendance, stage status |
| Counsellor | Web portal | Trainees on caseload — engagement, attendance, red flags |
| Administrator | Web dashboard | Full cohort view, milestone verification, calendar management |
| Authority | Web portal (read-only) | Assigned trainees — stage, attendance, reporting dates |

---

### 2. Database Schema

**The gap:** All data is hardcoded in the frontend. Production needs a proper database.

**Recommended stack:** Supabase (PostgreSQL + real-time + auth in one)

**Core tables (suggested):**

```sql
users           — id, email, role, full_name, cohort_id, created_at
trainees        — user_id, programme_stage, stage_progress (jsonb), xp, streak, badges (jsonb), employer_id, counsellor_id
milestones      — id, stage_num, name, description
trainee_milestones — trainee_id, milestone_id, completed_at, verified_by (admin user_id)
calendar_events — id, trainee_id, event_type (shift|reporting|mc|appointment), date, start_time, end_time, employer_id, verified_by_admin, status (pending|confirmed|flagged), document_url
courses         — id, title, description, price_sgd, xp_reward, content_url, active
trainee_courses — trainee_id, course_id, purchased_at, completed_at
feedback        — id, trainee_id, customer_name (optional), message, rating, submitted_at, approved_by, approved_at
notifications   — id, user_id, type, message, read, created_at
quiz_attempts   — trainee_id, score, xp_earned, attempted_at
```

---

### 3. Cloudflare Workers — AI Backend

**The gap:** The `/api/chat` route in the Worker does not exist. The demo's AI works via canned responses client-side.

**What to build:**

```
hawkerboysappdemo/
  workers/
    api-chat.js    ← the Worker function
  wrangler.jsonc   ← update to route /api/chat to the Worker
```

The Worker needs to:
1. Receive `{ messages, system }` from the client
2. Forward to Anthropic API (`claude-sonnet-4-6` or `claude-haiku-4-5` for speed)
3. Stream the response back to the client (important for UX — users see tokens appear as they arrive)
4. Handle auth — only authenticated requests (valid session token from Supabase) should be forwarded
5. Rate limit per user to prevent abuse

**Environment variables needed in Cloudflare:**
```
ANTHROPIC_API_KEY=...
SUPABASE_SERVICE_ROLE_KEY=... (for validating session tokens server-side)
```

**Streaming pattern:**
```js
// Worker: forward Claude stream back to client
const stream = await anthropic.messages.stream({ ... });
return new Response(stream.toReadableStream(), {
  headers: { 'Content-Type': 'text/event-stream' }
});
```

The `AIScreen` component (line 2497) will need to be updated to read a streaming response. Currently it awaits a single JSON blob.

---

### 4. Calendar & Scheduling Module

**The gap:** No calendar exists in the app. This is a Pathway tab feature.

**What it requires:**

- **Database:** `calendar_events` table (see schema above)
- **File storage:** Supabase Storage for MC/appointment document uploads (PDFs, images)
- **Frontend:** A calendar UI component — recommend `react-big-calendar` or a custom week/month grid
- **Push notifications:** When an employer uploads a shift schedule, the trainee gets a push notification. Requires a notification service — **Expo Push Notifications** if going React Native, or **Web Push API** if staying PWA.

**Three event types to support:**

| Type | Created By | Visible To | Notes |
|------|-----------|------------|-------|
| Work Shift | Employer | Trainee, Employer, Admin | Employer uploads schedule; trainee acknowledges |
| Reporting Date | Administrator | Trainee, Authority, Admin | Admin uploads verified dates; Authority can confirm |
| MC / Absence | Trainee | Employer, Counsellor, Admin | Trainee uploads document; Admin verifies |

**Key UX flow — MC submission:**
1. Trainee taps "Log Absence" in calendar
2. Selects date, reason type (MC / appointment / other)
3. Camera opens — photograph MC cert or appointment letter
4. Submits → status = `pending`
5. Admin reviews in dashboard → approves or flags
6. Employer notified: "Trainee has logged a verified absence for [date]"
7. Status → `confirmed`; absence visible on both employer and authority views

---

### 5. Elective Course Marketplace

**The gap:** No course system exists. Courses are described in the README but not built.

**What it requires:**

- **Payments:** Stripe (recommended) or PayNow QR (simpler for Singapore context). Stripe has a Singapore entity and supports SGD.
- **Content delivery:** For video courses, Vimeo (private) or Cloudflare Stream. For document-based courses, PDFs hosted on Supabase Storage with signed URLs.
- **LMS logic:** `trainee_courses` table tracks purchase and completion. Completion triggers XP award via a Supabase Edge Function or Cloudflare Worker.
- **Grade contribution:** A `programme_grade` field on the `trainees` table, recalculated when a course is completed.

**Stripe integration note:** Stripe's hosted checkout is the fastest path. It handles SGD, sends webhooks on payment success, and requires minimal server-side code. On webhook receipt, insert a `trainee_courses` record and award XP.

---

### 6. Customer Compliment Portal

**The gap:** No customer-facing portal exists.

**What it requires:**

- **Separate URL** (e.g. `feedback.hawkerboys.sg`) — a lightweight form page, not the full app
- **Trainee lookup** by programme ID (printed on stall badge QR)
- **Moderation queue** in the Admin dashboard — compliments do not go live until approved
- **Rate limiting** — one submission per IP per trainee per 24 hours (prevent spam)
- **QR code generation** for each trainee — auto-generated when a trainee enters Stage 2. Printable PDF.

**Claude can build:** The feedback form UI, the admin moderation queue UI, the trainee profile compliments display.

**You need to build:** The backend route that receives submissions, stores them pending, and sends the admin notification. The QR generation logic. The rate limiting middleware.

---

### 7. Mobile App

**The gap:** The current app is a web page rendered inside a phone-shaped `<div>`. It is not installable as a native app.

**Options:**

| Approach | Effort | Notes |
|----------|--------|-------|
| **PWA (Progressive Web App)** | Low | Add `manifest.json` + service worker. Works on iOS (limited) and Android. Installable from browser. No App Store. |
| **React Native (Expo)** | High | Full native app. Push notifications, camera access, biometrics. App Store + Play Store distribution. Most of the existing React component logic is portable. |
| **Capacitor (wrap existing React)** | Medium | Wraps the web app in a native shell. Gets you camera and push notifications with less rewrite than Expo. |

**Recommendation:** Start with PWA for the pilot cohort — fast to ship, no App Store review. Migrate to Expo/Capacitor when the programme scales and push notifications become critical.

**PWA minimum to implement:**
```
manifest.json        — app name, icons, theme colour, display: standalone
service-worker.js    — cache strategy for offline access
<link rel="manifest"> in index.html
```

---

### 8. Admin Dashboard

**The gap:** No admin view exists anywhere.

**What it requires:**
- Separate web app (or protected routes in the same app) — React + Tailwind, same stack
- Auth gated to `role = 'admin'`
- Key views: Cohort roster, individual trainee drill-down, milestone verification queue, calendar event management, course management, compliment moderation queue, MC approval queue
- Data tables: recommend **TanStack Table** (formerly react-table)

**Claude can build:** All UI components for the dashboard given a clear spec.

---

## Open Decisions

These require product or technical judgment — decisions Claude cannot make alone.

| Decision | Options | Notes |
|----------|---------|-------|
| **Mobile target** | PWA vs React Native (Expo) vs Capacitor | See above |
| **Payments** | Stripe vs PayNow QR | PayNow simpler for SG users; Stripe easier to integrate with webhooks |
| **Auth provider** | Supabase Auth vs Firebase vs custom | Supabase recommended — consistent with DB choice |
| **AI model for production** | `claude-haiku-4-5` (fast, cheap) vs `claude-sonnet-4-6` (better) | Sonnet for complex queries, Haiku for simple tool queries. Could route by type. |
| **Calendar UI library** | react-big-calendar vs FullCalendar vs custom | FullCalendar has best mobile UX; react-big-calendar lighter |
| **Authority portal access** | Full portal login vs read-only shared link with expiry | Shared link simpler for authorities who may not engage regularly |
| **Offline support** | Full offline (service worker cache) vs online-only | Trainees in hawker centres often have patchy connectivity — offline read access has value |
| **Language** | English only vs multilingual (Malay, Tamil, Mandarin) | Multilingual AI responses are feasible via Claude; UI translation requires i18n setup |
| **Hosting** | Cloudflare Pages (current) vs Vercel vs self-hosted | Cloudflare Pages is already configured and works; no reason to change |

---

## What Claude Can Build (Ongoing)

Claude can be handed component-level tasks and will produce working React code that integrates with the existing patterns in the codebase. Hand Claude:

- New tool modules (given a data spec and desired UX)
- Form UI (given field names and validation rules)
- Screen layouts (given a wireframe description or Figma export description)
- Data structures and seed data
- Copy — labels, tooltips, empty states, error messages
- The Recipe Book, tool content, quiz questions — any content-heavy layer

**Always verify Claude's output:**
- Claude does not run the code — it does not catch runtime errors
- Claude sometimes introduces subtle logic bugs in complex `useReducer` actions
- Claude may drift from the existing styling conventions if not reminded
- Claude cannot test on a real device

---

## Local Development

The demo runs by opening `index.html` in any browser — no server required for basic UI. For AI features, you need the Cloudflare Worker running:

```bash
npm install -g wrangler
wrangler dev        # starts local Worker at localhost:8787
```

Update the `callAI()` fetch URL in `index.html` to `http://localhost:8787/api/chat` for local testing.

For production builds, the recommendation is to migrate to Vite:

```bash
npm create vite@latest hawkerboys-app -- --template react
# Copy components from index.html into src/
# Install: recharts tailwindcss @tailwindcss/vite
```

---

## Deployment

Current deployment is via **Cloudflare Pages** — push to `main` on `JaroGee/hawkerboysappdemo` and Cloudflare automatically deploys.

Repo: `github.com/JaroGee/hawkerboysappdemo`
Live URL: configured in Cloudflare dashboard

---

## Key Contacts

| Role | Person |
|------|--------|
| Product Owner | JaroGee (via Claude Code sessions) |
| AI Co-developer | Claude (Anthropic) — via Claude Code CLI |
| Lead Developer | You |
