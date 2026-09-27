# Time-Based Email Router & Dispatcher

Automated Microsoft Power Automate flow designed to inspect incoming service/travel requests, apply sender filtration, and dynamically route emails based on operational hours (Working Hours, After Hours, and Weekends).

---

## 📌 Problem Statement
Manual processing of incoming travel and operational requests often creates severe bottlenecks and delays, especially outside standard working hours. Without an automated routing system, urgent requests sent during weekends or after-hours are frequently missed or delayed until the following business day.

---

## 📐 Logic Flow & Architecture

```text
[Incoming Email]
       │
       ▼
[Exclusion Filter] ─── (Match System/Internal Emails) ───> [Terminate Flow]
       │
       ▼
[Timezone Conversion to Local Time (UTC+7)]
       │
       ├── Weekend Check (Sat-Sun) ─────────> Route to Weekend Support Queue
       │
       └── Weekday Check (Mon-Fri)
              ├── Working Hours (08:00 - 17:00) ──> Route to Primary Support Queue
              └── After Hours (17:01 - 07:59)   ──> Route to 24/7 On-Call Support

```

---

## ✨ Key Features

* **Sender Exclusion Guard:** Automatically filters out system-generated emails, postmasters, and internal automated notifications (e.g., Workday, system alerts) to prevent infinite loops.
* **Timezone Standardization:** Converts UTC timestamps dynamically into local working timezone (`SE Asia Standard Time` / UTC+7).
* **Dynamic Routing Engine:**
* **Working Hours (Mon–Fri, 08:00–17:00):** Directs incoming requests directly to the primary operations counter.
* **After Hours (Mon–Fri, 17:01–07:59):** Dual-routes requests to both the primary counter and the 24/7 emergency support team.
* **Weekends (Saturday–Sunday):** Routes requests directly to the dedicated weekend on-call team.



---

## 🛠️ Tech Stack & Components

* **Platform:** Microsoft Power Automate
* **Connectors:** Office 365 Outlook API
* **Logic Functions:** Expression-based timezone conversion, Day-of-Week evaluation, and conditional branching logic.

---

## 📂 Repository Structure

```text
time-based-email-router/
├── README.md               <-- Documentation & system overview
└── src/
    └── flow-definition.json <-- Sanitized Power Automate flow definition

```

---

## 🚀 Setup & Deployment

1. Download or clone `src/flow-definition.json`.
2. Import the flow definition into your **Microsoft Power Automate** environment.
3. Re-bind the **Office 365 Outlook** connection references to your organization's mailbox account.
4. Adjust the operational thresholds (working hours and target email addresses) in `Condition_3` to match your team's schedule.

---

> **Note:** All email addresses, domains, and sensitive operational variables in this repository have been fully sanitized for public portfolio presentation.
