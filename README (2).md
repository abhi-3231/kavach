# Kavach ⚡ — कवच — AI-Powered Parametric Income Insurance for Q-Commerce Riders

> **Guidewire DEVTrails 2026 | University Hackathon**
> Protecting India's Zepto & Blinkit dark-store delivery partners from income loss caused by uncontrollable external disruptions.

---

## 🎯 The Problem

India's Q-Commerce riders (Zepto, Blinkit, Swiggy Instamart) operate in hyper-local dark-store zones of radius 1–3 km. When a disruption hits — a flash flood, a sudden curfew, a zone-level app outage — they lose income immediately, with **zero financial safety net**.

Unlike food delivery riders who can ride across a city, Q-Commerce riders are **geographically tethered** to their dark store zone. This means:
- A localised waterlogging event in Koramangala blocks **only those riders**, not city-wide
- Zone-level disruptions are **highly precise** and verifiable — ideal for parametric insurance
- Current insurance products are city-level and fail to capture this micro-geographic reality

**Kavach is the first hyper-local, zone-aware parametric income insurance platform built exclusively for Q-Commerce delivery partners.**

---

## 👤 Persona — Ravi, Zepto Delivery Partner (Chennai)

**Ravi** is a 26-year-old Zepto rider based out of the T. Nagar dark store, Chennai.
- Works 10–12 hours/day, 6 days a week
- Earns approximately ₹600–₹800/day; ~₹4,200/week
- Loses 1–3 working days per month to rain, zone closures, or local strikes
- Has no savings buffer, no employer, and no existing insurance
- Speaks Tamil; low digital literacy; uses a budget Android phone

**Ravi's Disruption Scenarios:**

| Scenario | Trigger | Income Lost |
|---|---|---|
| Heavy rain (>35mm/hr) near his zone | Weather API threshold breach | ₹600–800/day |
| Waterlogging closes his pickup zone | Dark store closure event | ₹600–800/day |
| AQI > 300 (hazardous) in his pin code | CPCB AQI feed | ₹400–600/day |
| Local shutdown/curfew in zone | Govt/news alert classification | ₹600–800/day |
| Dark store app outage > 3 hours | Platform API / mock signal | ₹300–500/day |

**Coverage:** Loss of income ONLY. No vehicle repair, no health, no accidents.

---

## 🧠 The Kavach Differentiator — Zone Intelligence

Most teams will build city-level disruption checks. We don't.

Kavach introduces **Zone Intelligence** — a micro-geographic risk layer that:

1. **Assigns every rider to a dark store zone** at onboarding (pin code + GPS cluster)
2. **Scores each zone weekly** using historical weather, flood, strike, and app-outage data
3. **Sets hyper-local premiums** — a zone historically safe from waterlogging pays ₹8–10 less per week
4. **Validates claims against zone data** — if a disruption is detected in Zone A, only Zone A riders get an auto-payout; GPS and activity data confirm the rider was actually offline

This means **no city-wide false triggers, no cross-zone fraud, ultra-precise payouts.**

---

## 💰 Weekly Premium Model

Gig workers operate week-to-week. Kavach aligns perfectly:

```
Weekly Premium = Base Rate + Zone Risk Score + Income Coverage Tier - Loyalty Discount
```

**Base tiers:**

| Plan | Weekly Premium | Max Weekly Payout | Coverage |
|---|---|---|---|
| Basic | ₹29/week | ₹800/week | 1 trigger event |
| Standard | ₹49/week | ₹1,500/week | Up to 2 trigger events |
| Shield+ | ₹79/week | ₹3,000/week | Unlimited triggers + priority payout |

**Dynamic adjustments (AI-driven):**
- Zone flood risk HIGH → +₹10/week
- Zone flood risk LOW (historically safe) → -₹8/week
- Rider active for 8+ weeks straight (loyalty) → -₹5/week
- Prior week had 0 claims industry-wide → -₹3/week (pool adjustment)

**Auto-renew every Monday.** Premium deducted from the rider's linked UPI/Razorpay account. No paperwork, no agent, no branch.

---

## ⚡ Parametric Triggers — How Claims Fire Automatically

Kavach monitors 5 parametric trigger signals every 30 minutes:

| Trigger | Data Source | Threshold | Auto-Claim |
|---|---|---|---|
| Extreme Rain | OpenWeatherMap API | > 35mm/hr in zone pin code | Yes |
| Waterlogging | IMD flood data / mock | Zone-level alert issued | Yes |
| Hazardous AQI | CPCB API / mock | AQI > 300 in zone district | Yes |
| Zone Curfew / Strike | News classifier (AI) | Verified unplanned closure | Yes |
| Dark Store App Outage | Platform webhook / mock | > 3 hrs downtime in zone | Yes |

**Zero-touch claim flow:**
1. Trigger threshold breached → Claim auto-initiated for all active policyholders in zone
2. Fraud Guard validates: GPS confirms rider was NOT active (offline during disruption)
3. Payout approved → UPI credit within 30 seconds (simulated via Razorpay sandbox)
4. Rider receives WhatsApp notification: *"₹600 credited to your UPI. Kavach has you covered."*

No form filling. No uploads. No waiting. No agent.

---

## 🤖 AI/ML Integration Plan

### 1. Dynamic Premium Calculation (Week 2–3)
- **Model:** Gradient Boosted Regressor (scikit-learn / XGBoost)
- **Features:** Zone historical disruption frequency, rider tenure, claim history, season, nearby dark store density
- **Output:** Per-zone weekly premium adjustment (±₹2–₹15)
- **Training data:** Synthetic historical weather + disruption dataset for 10 Indian cities

### 2. Disruption Classifier (Week 2)
- **Model:** Fine-tuned zero-shot text classifier (HuggingFace `facebook/bart-large-mnli`)
- **Input:** Live news headlines / govt alerts (scraped or mocked)
- **Output:** `disruption_type`, `affected_zone`, `confidence_score`
- **Fallback:** Keyword-rule engine for demo reliability

### 3. Fraud Detection — Fraud Guard (Week 4–5)
- **GPS Spoofing Detection:** Checks if rider GPS was suspiciously static in an "unaffected" sub-zone during a claimed disruption. Flags riders whose GPS trace doesn't match zone disruption boundaries.
- **Duplicate Claim Prevention:** Hash of (rider_id + zone_id + disruption_event_id) ensures one payout per event.
- **Anomaly Scoring:** If a rider claims in week 1 of a new policy during an unusual micro-event, anomaly score flags manual review.
- **Historical Cross-Check:** If AQI was zone-level but rider's GPS was 15km away, claim is auto-rejected.

### 4. Predictive Risk Dashboard (Week 5–6)
- **Forecast model:** Time-series (LSTM or Prophet) on weather + historical claims
- **Output for insurers:** "Next week Zone 7 (Koramangala) has 68% probability of >1 rain trigger event — reserve ₹42,000"

---

## 🛠️ Tech Stack

| Layer | Technology |
|---|---|
| Frontend | React.js (PWA — mobile-first for riders) |
| Backend | FastAPI (Python) |
| Database | PostgreSQL (via Supabase for rapid dev) |
| AI/ML | Python: scikit-learn, XGBoost, HuggingFace transformers |
| Weather API | OpenWeatherMap free tier + mocked responses |
| AQI API | CPCB open data / mock |
| Payment | Razorpay test mode / UPI simulator |
| Maps | Leaflet.js for zone heat maps |
| Notifications | Twilio WhatsApp sandbox |
| Hosting | Vercel (frontend) + Railway (backend) |

**Platform choice: Web (PWA)**
- Riders don't need to install an app
- Works on low-spec Android browsers
- Insurer admin portal needs desktop-grade dashboard → same codebase

---

## 📱 Application Workflow

### Rider Onboarding (< 3 minutes)
1. Enter mobile number → OTP login (no email needed)
2. Select delivery platform (Zepto / Blinkit / Swiggy Instamart)
3. Upload earnings screenshot OR enter self-declared weekly income (₹3,000 – ₹8,000)
4. GPS auto-detects nearest dark store zone → assigned to Zone
5. AI generates weekly premium quote → rider selects plan
6. UPI ID linked → policy active from next Monday

### Policy Management
- Rider sees: active week coverage, zone status (🟢 Normal / 🟡 Alert / 🔴 Disruption), payout history
- Auto-renew toggle (default ON)
- Weekly coverage certificate (downloadable PDF)

### Claim Flow (Zero-touch)
- When trigger fires → rider gets WhatsApp: *"Disruption detected in your zone. Claim auto-processing…"*
- 30 seconds later: *"₹600 credited. Stay safe!"*
- Rider can also check claim history in app

### Admin Dashboard (Insurer)
- Zone heat map: which zones are disrupted right now
- Live claims queue with fraud scores
- Loss ratio by zone, by week, by disruption type
- Predictive alerts: zones at elevated risk next 48 hours

---

## 📅 Development Plan

### Phase 1 (March 4–20) — CURRENT ✅
- [x] Idea document and README
- [x] System architecture design
- [x] Tech stack finalised
- [x] Synthetic dataset creation (weather + disruptions for 10 Indian cities)
- [x] Basic frontend scaffolding (React + routing)
- [x] Onboarding UI (prototype)

### Phase 2 (March 21 – April 4) — Automation & Protection
- [ ] Full onboarding flow (mobile-first)
- [ ] Zone assignment engine (GPS clustering)
- [ ] Weekly premium calculator (ML model v1)
- [ ] Policy creation and management module
- [ ] 5 automated parametric triggers (3 real APIs + 2 mocks)
- [ ] Zero-touch claim initiation flow
- [ ] Razorpay sandbox payout integration
- [ ] Basic fraud guard (duplicate prevention + GPS validation)

### Phase 3 (April 5–17) — Scale & Optimise
- [ ] Advanced fraud detection (GPS spoofing, anomaly scoring)
- [ ] Instant payout simulation end-to-end
- [ ] Rider dashboard (full PWA)
- [ ] Insurer admin dashboard with heat maps + predictive analytics
- [ ] Disruption simulation tool (for demo: "trigger fake rainstorm in Zone 3")
- [ ] Final pitch deck + 5-min demo video

---

## 🚫 Explicitly Excluded (per contest rules)
- ❌ Vehicle repair or damage coverage
- ❌ Health or medical insurance
- ❌ Life insurance or accident coverage
- ❌ Daily/monthly pricing models (weekly only)

---

## 👥 Team

| Member | Role |
|---|---|
| Abhishek Roy | System Architecture & Frontend |
| Rishika Raj | AI / ML Engineering |
| Tejas Sharma | Backend & API Development |
| Raunak Raj | Parametric Trigger Engine & Integrations |
| Sneha | Research & Data Collection |

---

## 🔗 Repository Structure

```
kavach/
├── frontend/          # React PWA
│   ├── src/
│   │   ├── pages/     # Onboarding, Dashboard, Claims, Admin
│   │   ├── components/
│   │   └── utils/
├── backend/           # FastAPI
│   ├── api/
│   │   ├── onboarding.py
│   │   ├── premium.py
│   │   ├── claims.py
│   │   └── triggers.py
│   ├── ml/            # AI/ML models
│   │   ├── premium_model.py
│   │   ├── fraud_guard.py
│   │   └── disruption_classifier.py
│   └── data/          # Synthetic datasets
├── docs/              # Architecture diagrams
└── README.md
```

---

## 📹 Demo Video (Phase 1)

> *(Insert your 2-minute video link here after recording)*

**What to cover in the video:**
1. The problem — Ravi's story (30 sec)
2. The Kavach solution — Zone Intelligence differentiator (40 sec)
3. Quick walkthrough of onboarding prototype (30 sec)
4. Weekly premium model explained (20 sec)

---

*Kavach — Because every rider deserves a Kavach — a shield as fast as the deliveries they make.*
