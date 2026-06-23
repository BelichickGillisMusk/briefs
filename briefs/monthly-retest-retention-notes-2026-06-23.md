# Monthly Retest Retention Check — Meeting Notes

**Event:** Monthly Retest Retention Check  
**Date:** Tuesday, June 23, 2026 · 10:00–10:30 PM  
**Recurrence:** Monthly on day 23  
**Facilitator:** Silverback Prime / Client Relations Agent  
**Data source:** [Gumption CRM](https://gumption.manus.space) + Master CRM Sheet `1TdNnf7eLaPNN3anaBGpNdjo_unK04zWwZJ859ZDvIO4`  
**Full lead export:** `briefs/retest-retention-2026-06-23.json`

---

## Executive Summary

| Metric | Value |
|--------|-------|
| Total tests in CRM | 957 |
| Unique vehicles tracked | 718 |
| **Actionable retests (0–90 days)** | **164** |
| Revenue at stake (est.) | $24,600 – $82,000 |
| Retention goal | 90%+ |
| Active clients in CRM | 92 |

### Priority Breakdown

| Tier | Window | Count | Action |
|------|--------|-------|--------|
| 🔴 URGENT | 0–7 days | **13** | Call immediately |
| 🟠 HOT | 8–30 days | **48** | Call this week |
| 🟡 WARM | 31–60 days | **60** | Email + call |
| 🟢 EARLY | 61–90 days | **43** | Email reminder |
| ⚪ FUTURE | 91+ days | 554 | Monitor |

---

## ⚠️ Data Quality Blocker

**All 957 test records lack `clientId` linkage in Gumption CRM** — vehicle-level retest dates are accurate (last test + 365 days), but phone/email must be enriched from the Master CRM sheet before outreach.

**Before calling or emailing:**
1. Open Master CRM → match license plates / VINs from the brief JSON to customer records
2. Dedupe against active clients (92 in CRM)
3. Update Gumption test enrichment (`/enrichment`) to link tests → clients (long-term fix)

---

## 🔴 URGENT — Call Immediately (13 vehicles)

| Days | Retest Due | Plate / ID | Notes |
|------|------------|------------|-------|
| 4 | 2026-06-27 | 55489T2 | Lookup in Master CRM |
| 4 | 2026-06-27 | YP80934 | Lookup in Master CRM |
| 4 | 2026-06-27 | 9E37405 | Lookup in Master CRM |
| 5 | 2026-06-28 | 05010F2 | Lookup in Master CRM |
| 5 | 2026-06-28 | 32219P2 | Lookup in Master CRM |
| 5 | 2026-06-28 | 0581952 | Lookup in Master CRM |
| 5 | 2026-06-28 | 3901293 | Lookup in Master CRM |
| 5 | 2026-06-28 | 33950X3 | Lookup in Master CRM |
| 5 | 2026-06-28 | 33960X3 | Lookup in Master CRM |
| 6 | 2026-06-29 | 50610W2 | Lookup in Master CRM |
| 7 | 2026-06-30 | 30143A3 | Lookup in Master CRM |
| 7 | 2026-06-30 | 16534S3 | Lookup in Master CRM |
| 7 | 2026-06-30 | 53163A3 | Lookup in Master CRM |

**Call script (retest):**
> Hi [Name], Bryan with NorCal CARB Mobile. We tested your [plate/VIN] about a year ago and your annual Clean Truck Check is due [date]. I can come to you — same mobile OBD + smoke test, usually same day. Want me to lock in a time this week before CA enforcement catches up?

---

## 🟠 HOT — Call This Week (48 vehicles)

Top of queue (due within 14 days):

| Days | Retest Due | Plate / ID |
|------|------------|------------|
| 8 | 2026-07-01 | 1XKAD49X1EJ418122 |
| 8 | 2026-07-01 | 21015G3 |
| 8 | 2026-07-01 | 01194F2 |
| 9 | 2026-07-02 | 7476873 |
| 9 | 2026-07-02 | 34580C2 |
| 9 | 2026-07-02 | 40434X3 |
| 9 | 2026-07-02 | 24000D3 |
| 9 | 2026-07-02 | 29353J3 |
| 9 | 2026-07-02 | 13620J3 |
| 9 | 2026-07-02 | 52507R2 |
| 10 | 2026-07-03 | XP75909 |
| 10 | 2026-07-03 | 70396E2 |
| 10 | 2026-07-03 | 10302K2 |
| 14 | 2026-07-07 | 11585S3, 99472K3, 81655R3, 27533Z3, 28721E2, 63266T1, 89498P3, 63267T1, 09646S3, 62478X3 |

*Full HOT list (48) in `briefs/retest-retention-2026-06-23.json` → `callTasks`.*

---

## 🟡 WARM + 🟢 EARLY — Email Blast (103 vehicles)

**Audience:** 60 WARM + 43 EARLY = 103 vehicles needing email reminder (+ follow-up call for WARM).

### Email subject
`Your CARB Clean Truck Check is due soon — NorCal CARB Mobile`

### Email body (template)
```
Hi [First Name],

Bryan here from NorCal CARB Mobile. Our records show your diesel vehicle [PLATE/VIN] is due for its annual CARB Clean Truck Check around [RETEST DATE].

We come to you — mobile OBD scan + OVI smoke opacity, same trip. No shop visit, no downtime.

✅ Annual compliance before CA enforcement
✅ OBD + smoke test on-site
✅ 24/7 scheduling — we work around your route

Reply to this email or call 916-890-4427 to book your retest.

Thanks,
Bryan
NorCal CARB Mobile
norcalcarbmobile.com
```

*Per-vehicle list in `briefs/retest-retention-2026-06-23.json` → `emailBlast`.*

---

## Action Checklist

- [ ] **Step 1:** Export URGENT + HOT plates from brief JSON
- [ ] **Step 2:** Match plates → customer phone/email in Master CRM sheet
- [ ] **Step 3:** Create 61 call tasks (13 URGENT + 48 HOT) in Gumption / calendar
- [ ] **Step 4:** Send WARM/EARLY email blast via Squarespace (after enriching contacts)
- [ ] **Step 5:** Update CRM contact status after each touch (`contacted`, `scheduled`, `declined`)
- [ ] **Step 6:** Schedule confirmed appointments + send calendar invites
- [ ] **Step 7:** Log outcomes in this doc before next month's check (July 23)

---

## Session Notes

*(Capture live notes during the 10:00–10:30 PM session below)*

### Attendees
- Bryan
- Client Relations Agent
- NorCal Operations Agent

### Decisions
- 

### Calls placed
| Time | Customer | Plate | Outcome | Follow-up |
|------|----------|-------|---------|-----------|
| | | | | |

### Emails sent
| Time | Customer | Email | Tier | Status |
|------|----------|-------|------|--------|
| | | | | |

### Appointments scheduled
| Customer | Date/Time | Vehicle(s) | Calendar invite sent? |
|----------|-----------|------------|----------------------|
| | | | |

### Blockers / issues
- CRM test → client linkage missing (957/957 unlinked). Enrichment pass needed.
- Contact info not on test records — must cross-ref Master CRM sheet.

### Revenue tracking
| Tier | Contacted | Scheduled | Retained | Est. revenue secured |
|------|-----------|-----------|----------|---------------------|
| URGENT | 0/13 | 0 | 0 | $0 |
| HOT | 0/48 | 0 | 0 | $0 |
| WARM | 0/60 | 0 | 0 | $0 |
| EARLY | 0/43 | 0 | 0 | $0 |

---

## Next Monthly Check

**July 23, 2026** — trigger phrase: *"Run monthly retest check"*

---

*Generated by Retest Retention Engine · June 23, 2026*
