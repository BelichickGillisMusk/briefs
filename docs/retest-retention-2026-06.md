# Monthly Retest Retention Check — June 2026

_Generated 2026-06-23 from `leads/retest-customers-sample.csv` by `leads/retest_retention_check.py`._

> ⚠️ **Demo data.** This run used the synthetic sample dataset because no `leads/retest-customers.csv` export was present. Export the Master CRM (`1TdNnf7eLaPNN3anaBGpNdjo_unK04zWwZJ859ZDvIO4`) to `leads/retest-customers.csv` and re-run before calling anyone.

> **Spec:** [`briefs/retest-retention-check.json`](../briefs/retest-retention-check.json)  
> **Trigger:** Calendar event _Monthly Retest Retention Check - Run Skill_ (23rd of every month)  
> **Trigger phrase:** `Run monthly retest check`

## Summary

| Bucket | Window | Action | Count |
|---|---|---|---:|
| 🔴 URGENT | ≤ 7 days (incl. overdue) | Call immediately | 4 |
| 🟠 HOT | 8–30 days | Call this week | 4 |
| 🟡 WARM | 31–60 days | Email + follow-up call | 4 |
| 🟢 EARLY | 61–90 days | Email reminder only | 2 |
| ⚪ OUT OF WINDOW | > 90 days | Re-check next month | 6 |
| **Total** | — | — | **20** |

**Actionable this cycle:** 14 of 20 (70% of customers).

## 🔴 URGENT — Call immediately (≤ 7 days)

| # | Company | Contact | Phone | Email | City | Vehicle | Last test | Cadence | Next due | Days |
|---:|---|---|---|---|---|---|---|---:|---|---:|
| 1 | Diablo Diesel Hauling | Marco Rivera | 510-555-0142 | marco@diablodiesel.example | Hayward | Class 8 Trucking ×6 | 2025-06-10 | 12 mo | 2026-06-10 | **-13** |
| 2 | Bayside Arbor Pros | Kevin Lam | 510-555-0177 | kevin@baysidearbor.example | San Leandro | Tree Service ×4 | 2025-06-12 | 12 mo | 2026-06-12 | **-11** |
| 3 | Foothill Ready-Mix | Patricia Núñez | 925-555-0193 | pnunez@foothillrm.example | Castro Valley | Concrete ×3 | 2025-06-15 | 12 mo | 2026-06-15 | **-8** |
| 4 | Crosstown Couriers HD | Riley Bennett | 510-555-0562 | riley@crosstown.example | San Leandro | Trucking ×4 | 2024-06-25 | 24 mo | 2026-06-25 | **2** |

## 🟠 HOT — Call this week (8–30 days)

| # | Company | Contact | Phone | Email | City | Vehicle | Last test | Cadence | Next due | Days |
|---:|---|---|---|---|---|---|---|---:|---|---:|
| 1 | Tri-City Towing Co | Andre Brooks | 510-555-0204 | andre@tricitytow.example | Oakland | HD Towing ×5 | 2025-07-05 | 12 mo | 2026-07-05 | 12 |
| 2 | Mission Asphalt Inc | Jeff Calhoun | 510-555-0221 | jeff@missionasphalt.example | Hayward | Asphalt/Paving ×4 | 2025-07-08 | 12 mo | 2026-07-08 | 15 |
| 3 | GoldGate Drilling | Linh Pham | 510-555-0245 | linh@goldgatedrill.example | Fremont | Drilling/Excavation ×3 | 2025-07-14 | 12 mo | 2026-07-14 | 21 |
| 4 | Redwood Tree Surgeons | Eric Tanaka | 650-555-0268 | eric@redwoodtree.example | Redwood City | Tree Service ×2 | 2025-07-22 | 12 mo | 2026-07-22 | 29 |

## 🟡 WARM — Email + follow-up call (31–60 days)

| # | Company | Contact | Phone | Email | City | Vehicle | Last test | Cadence | Next due | Days |
|---:|---|---|---|---|---|---|---|---:|---|---:|
| 1 | East Bay Concrete Pumping | Marisol Ortega | 510-555-0289 | marisol@ebconcrete.example | San Leandro | Concrete Pumping ×4 | 2025-08-01 | 12 mo | 2026-08-01 | 39 |
| 2 | Sierra Waste Hauling | Doug Whitaker | 510-555-0312 | doug@sierrawaste.example | Hayward | Waste/Hauling ×8 | 2025-08-09 | 12 mo | 2026-08-09 | 47 |
| 3 | Northbay LTL Express | Sandra Liu | 510-555-0341 | sandra@northbayltl.example | San Leandro | LTL Freight ×12 | 2025-08-15 | 12 mo | 2026-08-15 | 53 |
| 4 | Coastal Tree & Stump | Brian Holloway | 650-555-0367 | brian@coastaltree.example | San Mateo | Tree Service ×3 | 2025-08-22 | 12 mo | 2026-08-22 | 60 |

## 🟢 EARLY — Email reminder only (61–90 days)

| # | Company | Contact | Phone | Email | City | Vehicle | Last test | Cadence | Next due | Days |
|---:|---|---|---|---|---|---|---|---:|---|---:|
| 1 | Iron Horse Trucking | Naomi Park | 510-555-0388 | naomi@ironhorse.example | Oakland | Trucking ×5 | 2025-09-02 | 12 mo | 2026-09-02 | 71 |
| 2 | Summit Concrete Inc | Raj Patel | 925-555-0410 | raj@summitconcrete.example | Dublin | Concrete ×4 | 2025-09-15 | 12 mo | 2026-09-15 | 84 |

## ⚪ OUT OF WINDOW — Re-check next month (> 90 days)

| # | Company | Contact | Phone | Email | City | Vehicle | Last test | Cadence | Next due | Days |
|---:|---|---|---|---|---|---|---|---:|---|---:|
| 1 | Cascade Paving Co | Eddie Sandoval | 510-555-0432 | eddie@cascadepaving.example | Union City | Asphalt/Paving ×3 | 2025-09-22 | 12 mo | 2026-09-22 | 91 |
| 2 | Pacific Crane & Rigging | Tomás Ruiz | 510-555-0456 | tomas@pacificrane.example | Oakland | Crane/Rigging ×2 | 2025-09-28 | 12 mo | 2026-09-28 | 97 |
| 3 | Westside Vacuum Trucks | Ana Beltrán | 510-555-0478 | ana@westsidevac.example | Hayward | Vacuum/Sewer ×3 | 2025-12-05 | 12 mo | 2026-12-05 | 165 |
| 4 | Alameda Tree Care LLC | Mike O'Donnell | 510-555-0491 | mike@alamedatree.example | Alameda | Tree Service ×2 | 2025-12-12 | 12 mo | 2026-12-12 | 172 |
| 5 | Granite Bay Logistics | Felicia Owens | 916-555-0517 | felicia@granitebay.example | Sacramento | Trucking ×7 | 2026-01-10 | 12 mo | 2027-01-10 | 201 |
| 6 | Harbor Bay Excavation | Daniel Cho | 510-555-0539 | daniel@harborbay.example | Alameda | Excavation ×3 | 2026-01-22 | 12 mo | 2027-01-22 | 213 |

## Suggested email blast (WARM + EARLY)

**Subject:** Your CARB Clean Truck Check is coming up — we'll come to you

```
Hi {{contactName}},

Quick reminder from Bryan at NorCal CARB Mobile — your last Clean Truck Check on {{lastTestDate}} for {{vehicleType}} puts your next CARB
compliance check due around {{nextDueDate}} (~{{daysUntilDue}} days out).

Let's get ahead of it before the State does. Mobile OBD + smoke opacity, 30 min per truck, 24/7.

Reply with a window that works, or text 916-890-4427.

Bryan — NorCal CARB Mobile — 916-890-4427
```

## Next steps

1. Create call tasks in Gumption → Cold Calls for every 🔴 URGENT and 🟠 HOT row.
2. Paste the email body above into Squarespace Email Campaigns; audience = 🟡 WARM + 🟢 EARLY.
3. After each touch, update the Master CRM (`contact_status`, `contact_date`, `next_action`).
4. Send Google Calendar invites for confirmed retest appointments.
