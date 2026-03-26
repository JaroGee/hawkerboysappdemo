# Hawker Boys — App & AI Platform

## Overview

Hawker Boys is a Singapore-based social enterprise that takes individuals from marginalised or rehabilitative backgrounds and gives them a structured, supported pathway into the hawker trade. The app is the operational backbone of that programme — a mobile-first platform that tracks progress, delivers knowledge, connects stakeholders, and supports trainees from their first day of culinary training through to independently running a licensed hawker stall.

The app is not a passive learning tool. It is a live record of a trainee's journey — gamified to sustain motivation, but substantive enough to serve as an audit trail for programme administrators, employers, counsellors, and government authorities. Every function exists to serve at least one of six user groups, and most serve several simultaneously.

---

## The Four-Stage Programme

All features in the app are structured around four sequential stages. Understanding this framework is essential to understanding why every function exists.

| Stage | Name | Description |
|-------|------|-------------|
| 1 | **Training** | Culinary skills, food safety, kitchen operations under experienced mentors |
| 2 | **Placement** | Live stall under supervision. Real customers, real revenue targets, real accountability |
| 3 | **Aftercare** | Business support, financial counselling, peer mentorship to stabilise the stall |
| 4 | **Ownership** | Independent operation. Own stall, own brand, own income. Alumni network entry |

Each stage has four milestones that must be completed before the next stage unlocks. Progress within each stage is tracked as a percentage. The app reflects the trainee's real-world standing at all times.

---

## User Groups

The app is designed to serve six distinct user groups, each with different permissions, views, and use cases.

| Group | Who They Are |
|-------|-------------|
| **Trainee** | The individual going through the programme — may be an ex-offender, at-risk youth, or someone referred through social services |
| **Trainer** | Hawker Boys culinary and operations mentor responsible for hands-on teaching |
| **Employer** | The hawker stall owner or food court operator who takes on a placed trainee |
| **Counsellor** | Social worker, case manager, or pastoral support figure attached to the trainee |
| **Administrator** | Hawker Boys staff — programme coordinators, operations leads, management |
| **Authority** | Singapore Prison Service Yellow Ribbon rehabilitation officer, MSF case worker, or court-appointed supervisor |

Where a feature is described below, the relevant user groups are noted.

---

## Navigation

The app uses a five-tab bottom navigation bar:

```
Home  |  Pathway  |  AI  |  Tools  |  Profile
```

---

## Tab 1 — Home (Dashboard)

The Home tab is the daily entry point for the trainee. It surfaces everything they need to know at a glance.

### What It Shows

**User Identity Row**
Displays the trainee's name, cohort number, and current stage. A level badge shows their gamification rank (Novice → Trainee → Operator → Owner).

**XP Progress Bar**
Shows experience points accumulated and progress toward the next level. XP is earned through quiz completions, tool usage, stage milestone achievements, and (planned) elective course completions and customer compliments received.

**Stats Tiles**
Three headline metrics always visible:
- **Streak** — consecutive active days on the app. Sustained engagement indicates programme commitment.
- **Days In** — total days since programme start.
- **Total XP** — cumulative experience, used as an objective measure of effort and engagement.

**Your Journey Card**
A compact view of the four-stage journey: which stage the trainee is on, percentage completion of that stage, and a visual status of all four stages (locked / active / complete). Quick "On Track" status indicator.

**Today's Challenge**
A daily Hawker Culture Quiz — 10 questions covering Singapore food heritage, hawker history, hygiene rules, business knowledge. Completion earns +50 XP minimum. Designed to maintain daily engagement and reinforce cultural and vocational knowledge.

**Quick Actions**
Direct shortcuts to Pathway and AI tabs — the two most-used functions in the programme.

**Bell Icon (Notifications — planned)**
Future notifications for: shift reminders, reporting dates, MC acknowledgement, new course availability, employer feedback received, stage completion confirmation.

### User Group Context

| User | How They Use Home |
|------|------------------|
| **Trainee** | Daily check-in. Streak motivates return. XP bar gives sense of progression. Quiz builds knowledge in micro-doses. |
| **Administrator** | (Admin portal view) Cohort-level dashboard showing how many trainees are active today, average XP by stage, streak distribution — flags disengagement early. |
| **Counsellor** | Streak and days-active data is meaningful — a sudden streak break may indicate a personal crisis worth checking on. |
| **Authority** | Engagement data (days active, streak, quiz completion) provides evidence of rehabilitative effort for reporting periods. |

---

## Tab 2 — Pathway

The Pathway tab is the programme's official stage tracker. It shows the trainee exactly where they are, what milestones they have completed, what remains, and what comes next.

### What It Shows

**Stage Cards (×4)**
Each stage has a dedicated card showing:
- Stage name, number, and status (Locked / Active / Complete)
- A description of the stage's purpose
- A progress bar (0–100% completion)
- Four milestones specific to that stage, with completed items marked
- Lock state — a stage cannot be started until the previous is fully complete

**Stage Milestones**

*Stage 1 — Training:*
Food Hygiene Certificate · Basic Cooking Assessment · Advanced Techniques · Final Practical Exam

*Stage 2 — Placement:*
Stall Setup & NEA Inspection · First Week Service · Revenue Target Hit · Supervisor Sign-off

*Stage 3 — Aftercare:*
Monthly P&L Review · Supplier Agreements · SFA Compliance Audit · Peer Mentorship Session

*Stage 4 — Ownership:*
NEA Tender Submitted · Stall Licence Obtained · First Month Revenue · Alumni Network Joined

**Celebration Modal**
When a stage is completed, a full-screen celebration overlay fires — acknowledging the achievement, listing newly unlocked tools, and reinforcing the sense of genuine milestone reached.

**Alumni Outcome**
At Stage 4 completion, the app surfaces the alumni average revenue: $12,000/month — an evidence-backed aspirational anchor showing what successful programme completion looks like.

### User Group Context

| User | How They Use Pathway |
|------|---------------------|
| **Trainee** | Understands exactly what they need to do next. Milestones are concrete, achievable, and meaningful. |
| **Trainer** | Verifies real-world milestone completion and marks it in the admin portal, which reflects on the trainee's app in real time. |
| **Employer** | Can see at a glance which stage the trainee is at and what milestones they have cleared — confirms readiness for greater responsibility. |
| **Counsellor** | Stage progress provides a factual basis for case notes and intervention timing. A stall trainee stuck at the same stage for months needs outreach. |
| **Authority** | Stage data is audit-grade evidence of programme participation and progression — directly useful for Yellow Ribbon reporting requirements. |
| **Administrator** | Cohort-wide stage distribution — how many in Training, Placement, Aftercare, Ownership — gives pipeline visibility. |

---

### Planned: Calendar & Scheduling Module (Pathway Tab)

> **This feature is on the roadmap and not yet built in the current demo.**

The Pathway tab will be extended with a Calendar sub-view. This is one of the most operationally critical planned features because it bridges the trainee's personal app with the verified record-keeping needs of employers and authorities.

**Work Schedule**
Once a trainee is placed (Stage 2+), their employer uploads and confirms a weekly work schedule through the employer portal. This schedule appears in the trainee's calendar. The trainee can see which days and hours they are rostered. The employer can see whether the trainee has viewed the schedule.

**Official Reporting Dates**
For trainees on remission, supervision orders, or other conditional release arrangements, reporting dates to authorities (e.g. Yellow Ribbon officers, probation officers) must be tracked carefully. Hawker Boys administrators upload and verify these dates in the admin portal. Once confirmed, they appear as immovable calendar events on the trainee's app — colour-coded distinctly from work shifts. Trainees can refer to them at any time. Employers can see that a reporting date exists (without seeing its nature) so they can plan rostering. Authorities can verify that dates have been issued and acknowledged.

**MC and Appointment Tracking**
When a trainee is unwell or has a medical or legal appointment that causes them to miss work, they log it directly through the app:
- Upload a photo of the MC or appointment letter
- Log the date and expected duration
- Submit to the system for admin acknowledgement

The submission immediately notifies the employer that an absence has been logged with a supporting document. Administrators verify the submission and mark it as approved or flagged. Authorities can see absence patterns — the distinction between a medical absence with documentation and unexplained absences matters significantly in rehabilitation oversight.

**Why This Matters Per User Group**

| User | Value of Calendar Feature |
|------|--------------------------|
| **Trainee** | One place to see work shifts, reporting dates, and absences. No missed dates, no miscommunication with employer or officer. |
| **Employer** | Verified schedule, notified absences with documentation. Reduces friction and builds trust in the trainee. |
| **Counsellor** | Attendance patterns are rich data — consistent attendance suggests stability; erratic patterns prompt early intervention. |
| **Authority** | Verified reporting date delivery and acknowledgement. Absence documentation that is admin-verified. Attendance record for compliance reporting. |
| **Administrator** | Central source of truth across all trainees — who is rostered, who has reported, who is absent, and whether documentation is in order. |

---

## Tab 3 — AI (Hawker AI Chatbot)

The AI tab is a conversational interface powered by Claude (Anthropic). It is the most versatile tool in the app — part business advisor, part operational guide, part emotional support, part compliance assistant. The AI adapts its persona and depth based on the trainee's current stage:

| Stage | AI Persona |
|-------|-----------|
| 1 — Training | **Training Mentor** — culinary guidance, hygiene, technique, food safety compliance |
| 2 — Placement | **Business Coach** — daily ops, pricing, customer service, supplier management |
| 3 — Aftercare | **Business Advisor** — financial stability, SFA compliance, scaling early operations |
| 4 — Ownership | **HAWKR.AI** — full business intelligence partner |

### Current Quick-Prompt Chips

The AI screen surfaces six pre-built prompt chips to lower the barrier to first use:

| Chip | What It Does |
|------|-------------|
| **Cost a dish** | Walks the trainee through food cost calculation for any dish — ingredients, portion cost, suggested sell price, margin percentage |
| **Supplier message** | Drafts a professional supplier enquiry, negotiation, or complaint message |
| **Opening SOP** | Generates a step-by-step opening procedure checklist for the stall |
| **Price my menu** | Analyses a described menu and suggests pricing based on Singapore hawker benchmarks and food cost targets |
| **Customer complaint** | Helps the trainee respond professionally to a customer complaint — written or verbal |
| **Track revenue** | Explains a simple daily revenue tracking methodology suited to a solo hawker operation |

### Full AI Capability Map

Beyond the quick chips, the AI is capable of handling — and should be explicitly marketed as handling — the following use cases:

**Culinary & Recipe Intelligence**
- Scale any recipe from 1 to 200 portions with adjusted quantities
- Advise on ingredient substitutions based on availability or cost
- Explain technique steps in plain language for a trainee with no prior cooking background
- Identify likely causes of a dish quality problem ("my chicken rice skin is loose — why?")

**Financial & Costing**
- Food cost percentage calculation for any dish
- Break-even analysis: how many portions must I sell to cover today's costs?
- Monthly P&L walkthrough — what to track, what to watch
- 6-year projection modelling (tied to the Cost Engine tool)
- Advice on when to raise prices and how to communicate it to regular customers

**Regulatory & Compliance**
- SFA Food Stall Licence requirements and application steps
- NEA tender process explained step by step
- Food hygiene rules and common inspection failure points
- Productive Hawker Centre (PHC) crockery deposit requirements
- What triggers a licence suspension and how to avoid it

**Operations**
- Opening and closing SOP generation
- Prep schedule optimisation for a given menu
- Equipment sourcing guidance (new vs used, where to buy in Singapore)
- Waste reduction strategies for specific dishes
- Staff rostering for a 1–2 person stall

**Supplier & Procurement**
- Which wet market or supplier to use for specific ingredients
- Negotiating terms with suppliers
- Draft formal procurement messages
- Comparing supplier quotes

**Business Growth**
- Grant eligibility assessment (NEA ISP, EDG, SkillsFuture for Enterprises)
- Catering and event enquiry handling
- When to consider a central kitchen
- NEA rules on subletting (important legal boundary)
- How to build a second stall operation

**Emotional & Motivational Support**
- The AI is trained to recognise expressions of frustration, anxiety, or discouragement that are common in this trainee cohort
- It responds with practical reframing and a realistic but encouraging tone
- It does not replace a counsellor but can be the first point of contact at 2am when a trainee is stressed about tomorrow's service

**Admin & Document Drafting**
- Drafting emails to employers, landlords, or government bodies
- Writing a stall introduction for social media or a signboard
- Preparing for a NEA tender interview — likely questions and answers
- Complaint letters to suppliers

---

### Planned AI Capabilities (Roadmap)

These are not yet in the demo but represent the intended trajectory of the AI system.

**Computer Vision — Stall Optimisation**
The trainee uploads a photo of their stall layout or food display. The AI analyses:
- Customer flow and visibility of key items
- Signage readability and placement
- Food display hygiene and presentation
- Suggested layout changes to increase impulse purchases
- Comparison against proven high-revenue hawker stall configurations

A second use case: upload a photo of the stall space before tendering for it. The AI estimates A&A costs, equipment fit, exhaust hood compatibility, and flags potential issues (3-phase power availability, drainage, shared infrastructure) — reducing expensive surprises post-bid.

**Computer Vision — Menu Costing from Receipt**
Photograph a supplier receipt or wet market purchase. The AI reads the itemised costs, maps them to dishes on the trainee's menu, updates food cost calculations automatically, and flags if any ingredient cost has spiked significantly since last purchase.

**Rental & Tender Optimisation**
Input a NEA tender notice number or venue details. The AI retrieves available public data on that hawker centre — historical AMR, vacancy duration, nearby competitor stalls, footfall proxies — and provides a data-informed bid range recommendation with risk notes.

**Mini Job Portal**
Trainees completing Stage 4 who are ready to hire staff can post opportunities through the app. Similarly, trainees who have completed training but are waiting for stall placement can register availability for temporary hawker assistant work. Employers and alumni stall owners can search and match. This creates a closed, trusted job market within the Hawker Boys ecosystem — where every listed candidate has a verified programme background.

**Training Portal & Elective Courses**
See dedicated section below.

**Voice Mode**
The trainee speaks to the AI instead of typing — useful during food prep when hands are occupied. The AI responds with voice. Practical in a hot kitchen environment where a touchscreen is impractical.

**Multi-language Support**
Singapore's hawker cohort includes Malay, Tamil, Mandarin, and Hokkien speakers. The AI responds in the trainee's preferred language while keeping all official record data in English for compliance purposes.

---

### User Group Context — AI

| User | How They Use AI |
|------|----------------|
| **Trainee** | Daily business advisor, learning resource, recipe guide, emotional support, document drafter |
| **Trainer** | Can review common AI queries from their trainee cohort — identifies knowledge gaps to address in sessions |
| **Employer** | (Future) A separate employer AI instance helps with scheduling, payroll queries, and reporting their trainee's attendance |
| **Counsellor** | AI interaction logs (with consent) can surface mental health signals — unusual query patterns, expressions of stress — for review |
| **Administrator** | Aggregate AI query data reveals what topics trainees most need help with — informs curriculum updates and resource allocation |
| **Authority** | The AI's responses are consistent, documented, and auditable — providing a traceable advice trail if any compliance question arises |

---

## Tab 4 — Tools

The Tools tab is the business intelligence suite. Eight tools are available, all unlocked by default in the demo. In the live programme, tools unlock progressively as stages are completed — reinforcing the idea that capability is earned, not given.

Each tool opens as a full-screen bottom-sheet panel within the app.

---

### Tool 1 — Cost Engine

**What It Does**
A financial modelling tool. The trainee inputs their stall parameters — rent, staff count, daily covers, average spend, food cost percentage, operating hours, days per week. The tool calculates monthly costs broken down by category and projects a 6-year financial outlook.

**Cost Categories Modelled**
Tendered Rent · S&CC (15% of rent) · Table Cleaning ($150/month flat) · Utilities · Labour (including CPF 17%) · Ingredients/COGS · Packaging

**Why It Exists**
Most hawker stall failures are financial, not culinary. Trainees who understand their cost structure before opening are dramatically less likely to be caught off-guard by a bad month. The 6-year projection models rent escalation and helps trainees understand whether a stall is viable at the bid price they are considering.

**Scenario — Trainee:**
Ahmad is preparing to bid on a stall. He inputs a rental bid of $2,400/month. The Cost Engine shows him his break-even is 110 covers/day at $5.50 average spend — doable, but tight. He considers whether to lower his bid.

**Scenario — Trainer:**
Trainer uses it in a classroom session to show a cohort why a $3,000/month rental bid at a slow centre is financially dangerous.

**Scenario — Counsellor:**
A trainee is anxious about finances. The counsellor walks through the Cost Engine with them to show their plan is viable and where the risks actually sit.

**Scenario — Authority:**
During a supervision review, the trainee can show a printed or screen-shared Cost Engine output demonstrating their business plan is financially sound — evidence of serious vocational preparation.

---

### Tool 2 — Culinary Knowledge

**What It Does**
A searchable recipe and supplier reference. Each recipe shows cost per portion, sell price, margin percentage, key ingredients, and operational notes. A wholesale supplier directory is also included, covering wet markets, seafood ports, dry goods, specialty spice suppliers, frozen/chilled, and packaging.

**Why It Exists**
Stage 1 trainees do not yet have the business tools, but they need culinary reference material immediately. This tool bridges the gap — it is both a study resource and a practical kitchen companion.

**Scenario — Trainee:**
In the middle of prep, a trainee forgets the ratio for laksa rempah. They open the app, search Laksa, and have the full recipe in front of them in seconds.

**Scenario — Trainer:**
Points trainees to the supplier directory when they ask where to source cockles or fresh pandan leaves.

---

### Tool 3 — Stall Finder

**What It Does**
A searchable directory of hawker venue types in Singapore — NEA hawker centres, SEHC (Social Enterprise Hawker Centres), Town Council-managed centres, private kopitiams, and food courts. Each entry shows rental range, operational model, pros and cons of that venue type, and key considerations.

**Why It Exists**
Choosing the wrong venue is one of the most costly and irreversible decisions a new hawker can make. Trainees need to understand the difference between an NEA tender (competitive, subsidised, long lease) and a private kopitiam (lower barrier, higher rent, different risk profile) before they commit.

**Scenario — Trainee (Stage 3–4):**
Preparing to bid independently, a trainee uses Stall Finder to compare venues in their target neighbourhood — understanding the rental model, footfall, and risk profile of each option before making a decision.

**Scenario — Counsellor:**
A trainee is considering a private kopitiam offer that seems attractive. The counsellor opens Stall Finder together with the trainee to review the cons section — which includes higher S&CC, shorter lease security, and landlord dependency — helping the trainee make an informed choice.

---

### Tool 4 — Tender Intelligence

**What It Does**
A knowledge base on NEA tender strategy, categorised into three areas: Tender Tricks, Ops Survival, and Cost Traps. Topics include reading vacancy signals, calculating the true cost of overbidding, equipment red flags in tender notices, R&R closure risk, first-3-months cash buffer requirements, and NEA subletting rules.

**Why It Exists**
The NEA tender process is opaque and unforgiving. Hawkers who overbid are locked into unviable economics for the entire 3- or 6-year lease. This tool translates institutional knowledge — accumulated from alumni who have made these mistakes — into actionable guidance.

**Scenario — Trainee (Stage 4):**
About to submit a tender bid. Reviews the "Overbid Cost Calculator" entry: every $100 over AMR costs $3,600 over 3 years. Recalibrates their bid.

**Scenario — Administrator:**
Uses Tender Intelligence content in pre-bid workshops for cohorts approaching Stage 4.

---

### Tool 5 — Operations

**What It Does**
A comprehensive operations reference covering daily SOPs, SFA compliance requirements, and equipment sourcing. Equipment directory includes commercial wok ranges, griddles, deep fryers, steamers, chillers, rice cookers, POS systems, and display warmers — with new/used price ranges and Singapore supplier locations.

**Why It Exists**
Stage 2 trainees face a steep learning curve when they hit a live stall. This tool gives them a consolidated operational reference — reducing reliance on the trainer for procedural questions and building operational independence.

**Scenario — Trainee (Stage 2):**
First week on placement. Opens Operations, runs through the opening SOP before service. Trainer verifies this becomes a habit.

**Scenario — Employer:**
New to hosting a Hawker Boys trainee, the employer reviews the Operations tool to align their own procedures with what the trainee has been trained on.

---

### Tool 6 — Insider Tips

**What It Does**
Real intelligence from experienced hawkers — things not found in any official guide. Topics include reading NEA vacancy signals, R&R closure risk, opening week stock calibration, S&CC negotiation in private venues, SFA licence timeline traps, crockery floats at PHCs, and central kitchen readiness indicators.

**Why It Exists**
Formal training teaches craft and compliance. Insider Tips teaches survival. The content is drawn from real experiences of alumni and programme graduates — the unwritten knowledge that separates hawkers who last from those who don't.

**Scenario — Trainee (Stage 3):**
Surprised by a large S&CC invoice. Opens Insider Tips, finds the S&CC Negotiation entry, and discovers they can request an itemised breakdown and potentially reduce costs by $100–300/month.

---

### Tool 7 — Business Builder

**What It Does**
A grants and funding directory covering Singapore programmes relevant to hawkers and food entrepreneurs. Currently includes: NEA Incubation Stall Programme, Enterprise Development Grant (EDG), Productivity Solutions Grant (PSG), SkillsFuture Enterprise Credit (SFEC), and the Hawkers' Development Programme.

**Why It Exists**
Grant funding is available but underutilised because eligible hawkers don't know about it or find the application process opaque. Business Builder demystifies what is available and who qualifies — potentially worth tens of thousands of dollars to a trainee who applies.

**Scenario — Trainee (Stage 4):**
Six months into running their own stall, wants to invest in a POS system and signage refresh. Business Builder surfaces the Productivity Solutions Grant — up to 50% subsidy. Applies successfully.

**Scenario — Administrator:**
Reviews Business Builder grants against current government updates quarterly, ensuring the content stays current.

---

### Tool 8 — Recipe Book

**What It Does**
The app's definitive culinary reference — 23 authentic Singapore hawker dishes across Chinese, Malay, Indian, and Peranakan cuisines. Each recipe includes:

- Cost per portion and suggested sell price
- Margin percentage
- Prep time and cook time
- Difficulty rating (Easy / Medium / Hard)
- Full ingredient list with sourcing notes
- **Portion Scaler** — dynamically recalculates all ingredient quantities for ×1, ×10, ×50, ×100, or ×200 portions
- Step-by-step method
- Chef Tips — the non-obvious knowledge that determines success or failure
- Hawker Scale Guide — operational guidance specific to each volume tier
- Common Mistakes — the errors most likely to cause a dish to fail at the stall

**Cuisine and Category Filters**
Filter by cuisine (Chinese, Malay, Indian, Peranakan) and category (Rice, Noodles, Bread, Snacks, Grilled, Curry, Dessert, Breakfast).

**Current Dishes**

| Dish | Cuisine | Category | Margin |
|------|---------|----------|--------|
| Hainanese Chicken Rice | Chinese | Rice | 60% |
| Char Kway Teow | Chinese | Noodles | 69% |
| Laksa | Peranakan | Noodles | 63% |
| Nasi Lemak | Malay | Rice | 60% |
| Hokkien Mee | Chinese | Noodles | 67% |
| Roti Prata | Indian | Bread | 69% |
| Bak Chor Mee | Chinese | Noodles | 70% |
| Chicken Biryani | Indian | Rice | 63% |
| Carrot Cake (Chai Tow Kway) | Chinese | Snacks | 80% |
| Mee Rebus | Malay | Noodles | 68% |
| Wanton Mee | Chinese | Noodles | 73% |
| Oyster Omelette (Orh Luak) | Chinese | Snacks | 68% |
| Satay | Malay | Grilled | 67% |
| Prawn Noodle Soup | Chinese | Noodles | 67% |
| Curry Chicken | Indian | Curry | 63% |
| Fish Head Curry | Indian | Curry | 64% |
| Popiah | Peranakan | Snacks | 64% |
| Chwee Kueh | Chinese | Snacks | 75% |
| Nasi Goreng | Malay | Rice | 73% |
| Chendol | Malay | Dessert | 77% |
| Ice Kachang | Chinese | Dessert | 77% |
| Kaya Toast Set | Chinese | Breakfast | 77% |
| Tau Huay (Soya Beancurd) | Chinese | Dessert | 80% |

**Why It Exists**
Singapore's hawker culture is a UNESCO Intangible Cultural Heritage. This tool treats it with that seriousness. The Recipe Book is not a simplified list — it is a reference built for trainees who will be cooking these dishes commercially, at volume, every day. The Hawker Scale Guide in particular bridges the gap between "following a recipe" and "running a stall" — an operational distinction that is not made in any other cooking reference available to this cohort.

**Scenario — Trainee (Stage 1):**
Studying for the Basic Cooking Assessment. Uses the Recipe Book to review technique for Hainanese Chicken Rice. The Common Mistakes section ("Never boil — poach at 85°C") explains exactly why their trainer keeps correcting them.

**Scenario — Trainee (Stage 2):**
First week on a live stall. A customer orders Mee Rebus. The trainee cannot remember the gravy thickening ratio. Opens Recipe Book, checks the mashed sweet potato notes in under 10 seconds.

**Scenario — Trainer:**
Uses the Recipe Book's Hawker Scale Guide in class to show trainees the operational difference between cooking for 10 and cooking for 100. Uses the portion scaler as a live classroom exercise.

**Scenario — Administrator:**
The Recipe Book serves as the programme's canonical culinary curriculum — ensuring all trainers across cohorts are teaching consistent standards.

---

## Tab 5 — Profile

The Profile tab is the trainee's personal record within the programme.

### What It Shows

**Identity**
Name, cohort, batch, current stage, and level title (Novice → Trainee → Operator → Owner).

**XP & Level Progress**
Visual progress bar to the next level, with XP remaining displayed numerically.

**Achievements (Badges)**
Eight badges that are earned through programme milestones and app engagement:

| Badge | Earned By |
|-------|-----------|
| First Day | Logging in on programme Day 1 |
| 7 Streak | Seven consecutive daily active days |
| Certified | Completing food hygiene certification |
| 300 XP | Accumulating 300 experience points |
| Placed | Reaching Stage 2 — stall placement |
| First $1K | Recording first $1,000 in monthly stall revenue |
| Owner | Completing Stage 4 |
| Mentor | Completing a peer mentorship session as a mentor |

**Stats Panel**
Total XP · Days Active · Day Streak · Stage Completion Percentage

**Why Badges Matter**
For a trainee cohort that has often experienced environments where effort went unrecognised, explicit acknowledgement of milestones — however small — has documented motivational value. Badges are also meaningful to employers and authorities as evidence of consistent engagement. The Mentor badge is particularly significant: it indicates that a trainee has reached the stage of giving back to others in the programme.

### User Group Context

| User | How They Use Profile |
|------|---------------------|
| **Trainee** | Pride of record. Tracks personal progress. Shares achievements with family. |
| **Employer** | Verifies programme stage, certifications earned, and engagement levels before making placement decisions. |
| **Authority** | Achievement record provides an objective, app-verified account of rehabilitative effort — useful in supervision reviews and court reporting. |
| **Counsellor** | Streak patterns and badge gaps inform pastoral check-ins. |

---

## Gamification System

The app uses a light gamification layer throughout — not as a gimmick, but as a structural engagement mechanism calibrated to a cohort that has historically struggled with institutional programmes that feel punitive or passive.

**XP (Experience Points)**
Earned through: quiz completion, tool usage, stage milestone completion, daily active days, and (planned) elective courses and customer compliments.

**Levels**
XP accumulation unlocks levels: Novice → Trainee → Operator → Owner. Level titles mirror the real-world progression of a hawker's career.

**Streaks**
Consecutive daily active days are tracked. A streak break is a signal — and a prompt for trainer or counsellor outreach.

**Stage Locks**
Tools unlock progressively with stage completion in the live programme (all unlocked in demo). This creates forward momentum — the next set of capabilities is visible but gated, creating anticipation.

**Celebration Modals**
Stage completions trigger a full-screen acknowledgement. In a programme context, this moment is shared — trainers celebrate it, the cohort sees it. It is a designed social moment.

---

## Planned Features — Elective Courses

> **This feature is on the roadmap and not yet built in the current demo.**

### What It Is
A marketplace of short, purchasable courses adjacent to hawker business operations. Courses are practical, Singapore-specific, and designed to give trainees a genuine business edge. Examples:

| Course | Description | Approx. Price |
|--------|-------------|--------------|
| Social Media for Hawkers | Instagram and TikTok content strategy for food stalls | $18 |
| GrabFood & Deliveroo Onboarding | Setting up and optimising delivery platform listings | $12 |
| Basic Business Accounting | P&L, GST threshold awareness, simple bookkeeping | $25 |
| Halal Certification Walkthrough | MUIS halal certification process for eligible stalls | $15 |
| Wok Hei Masterclass | Advanced wok technique from a Michelin-recognised hawker | $38 |
| Customer Service for Hawkers | Handling complaints, building regulars, managing queues | $12 |
| Central Kitchen Setup 101 | When and how to move to a central kitchen model | $22 |

### Gamification Integration
Completing an elective course awards XP. The amount is weighted to reflect the investment made — paid courses give more XP than free daily quizzes. In programme grading, elective completions are recorded as additional effort and contribute positively to the trainee's programme assessment score. The signal is clear: self-directed learning beyond the minimum requirement is recognised and rewarded.

### User Group Context

| User | Value |
|------|-------|
| **Trainee** | Real skills, recognised effort, higher programme grade |
| **Trainer** | Recommends relevant courses to individual trainees based on their gaps |
| **Administrator** | Revenue stream for Hawker Boys. Course completion data informs curriculum development. |
| **Authority** | Elective completions are additional evidence of proactive rehabilitation and vocational investment |

---

## Planned Features — Customer Feedback Portal

> **This feature is on the roadmap and not yet built in the current demo.**

### What It Is
A separate, public-facing web portal (not the trainee app) where customers who have visited a Hawker Boys trainee's stall can leave verified positive feedback.

### How It Works
1. A customer scans a QR code displayed at the stall, or visits the portal URL.
2. They enter the trainee's programme ID (printed on the stall's Hawker Boys badge) or search by stall name.
3. They are prompted to submit a compliment — a short text note, optionally with a star rating for food quality, friendliness, and value.
4. The submission is sent to Hawker Boys for moderation. Approved compliments appear on the trainee's profile.
5. Each verified compliment earns the trainee a small XP reward.

### Why It Matters
For trainees from marginalised backgrounds, unsolicited positive feedback from a stranger — a real customer who chose to take 30 seconds to say something kind — carries disproportionate motivational weight. It also creates a public record of community reception that is meaningful in counselling, employer relations, and authority reporting. It is evidence that the trainee has not just completed a programme but has genuinely connected with the public they serve.

### Moderation
Hawker Boys administrators approve all submissions before they appear. This protects trainees from any malicious or inappropriate content, and ensures the record remains a positive asset.

### User Group Context

| User | Value |
|------|-------|
| **Trainee** | Direct positive reinforcement from the community they serve |
| **Employer** | Real customer feedback validates the trainee's front-of-house quality |
| **Counsellor** | Positive community reception is a powerful anchoring tool in counselling sessions |
| **Authority** | Community compliments are evidence of successful social reintegration — particularly significant for ex-offenders on supervision orders |
| **Administrator** | Aggregate feedback data identifies standout trainees for awards, media features, and alumni ambassador roles |

---

## Technical Architecture

The current demo is a fully self-contained single-file web application:

- **Framework:** React 18 (loaded via CDN, no build step)
- **Styling:** Tailwind CSS + custom dark-theme CSS variables
- **State Management:** React `useReducer` with `localStorage` persistence
- **AI Backend:** Cloudflare Workers proxy → Claude API (Anthropic). The proxy handles authentication — no API key is exposed client-side in production.
- **Deployment:** Static HTML file, deployable to any web host, Cloudflare Pages, or GitHub Pages
- **Data:** All reference data (recipes, venues, tips, equipment, grants) is embedded in the file — no external database dependency for core content

### Cloudflare Workers Integration
The `wrangler.jsonc` file configures the Cloudflare Workers deployment. The worker acts as a secure proxy between the app and Claude API — abstracting the API key from the client and enabling rate limiting, logging, and multi-tenant support as the programme scales.

---

## Roadmap Summary

| Feature | Status |
|---------|--------|
| Home Dashboard | ✅ Live |
| Pathway Stage Tracker | ✅ Live |
| AI Chatbot (Claude-powered) | ✅ Live |
| Cost Engine | ✅ Live |
| Culinary Knowledge | ✅ Live |
| Stall Finder | ✅ Live |
| Tender Intelligence | ✅ Live |
| Operations Module | ✅ Live |
| Insider Tips | ✅ Live |
| Business Builder (Grants) | ✅ Live |
| Recipe Book (23 dishes) | ✅ Live |
| Calendar & Work Scheduling | 🔲 Planned |
| Official Reporting Dates | 🔲 Planned |
| MC & Absence Tracking | 🔲 Planned |
| Elective Course Marketplace | 🔲 Planned |
| Customer Compliment Portal | 🔲 Planned |
| AI Computer Vision (Stall) | 🔲 Planned |
| AI Tender Optimisation | 🔲 Planned |
| Mini Job Portal | 🔲 Planned |
| AI Voice Mode | 🔲 Planned |
| Multi-language AI | 🔲 Planned |
| Multi-role Portals (Employer, Authority, Admin) | 🔲 Planned |

---

## About Hawker Boys

Hawker Boys is a social enterprise dedicated to preserving Singapore's hawker culture while creating meaningful second chances for individuals who need them. The programme has helped graduates build self-sustaining businesses, with alumni averaging $12,000/month in revenue. The app is the infrastructure that makes the programme scalable, accountable, and evidenced — so that every stakeholder, from a trainee eating breakfast before their shift to a Yellow Ribbon officer preparing a supervision report, has what they need, when they need it.

---

*Demo built with React + Tailwind CSS. AI powered by Claude (Anthropic) via Cloudflare Workers.*
