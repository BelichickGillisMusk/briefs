# Gumption Architecture Review (Reverse-Engineered)

**Live app:** https://gumption.manus.space  
**Review date:** 2026-05-22  
**Method:** Production bundle analysis + public tRPC API probing  

## Executive summary

Gumption is a **NorCal CARB / Gillis Institute CRM** deployed on **Manus** (`*.manus.space`). The **source code is not in the `briefs` repo** or any public `BelichickGillisMusk/gumption` GitHub repo. It exists as a compiled Vite/React app with an Express + tRPC backend.

The closest related repo is [GILLIS-HQ](https://github.com/BelichickGillisMusk/GILLIS-HQ) (virtual office / Spark app) — **different product**, no Cold Calls or Knowledge Base modules.

To add features (file upload → assimilate into Knowledge / Leads / Cold Calls), you need either:

1. **Export the Manus project** that built Gumption into GitHub, or  
2. **Rebuild** using this reverse-engineered map + the implementation spec below.

---

## Tech stack (confirmed)

| Layer | Technology |
|-------|------------|
| Hosting | Manus (`gumption.manus.space`, `x-powered-by: Express`) |
| Frontend | React + Vite, Wouter routing, TanStack Query + tRPC client (`tt.*`) |
| UI | shadcn-style components (`client/src/components/ui/*`) |
| API | tRPC at `/api/trpc` |
| Auth (UI) | `PasscodeGate.tsx` — **client-only** `sessionStorage` key `gumption_unlocked` |
| Assets | `/manus-storage/*` |
| Analytics | manus-analytics.com, Plausible |

---

## Source tree (from production bundle)

Recovered from `index-CrS2bJz8.js` source paths:

```
client/src/
├── App.tsx
├── main.tsx
├── components/
│   ├── PasscodeGate.tsx      # unlock gate
│   ├── DashboardLayout.tsx
│   ├── Sidebar.tsx
│   └── ui/                   # button, card, dialog, input, ...
├── pages/
│   ├── Home.tsx              # /dashboard
│   ├── ColdCallPage.tsx      # /coldcall
│   ├── LeadsPage.tsx         # /leads
│   ├── ClientsPage.tsx       # /clients
│   ├── KnowledgeBasePage.tsx # /knowledge  ← file assimilation target
│   ├── TestEnrichmentPage.tsx# /enrichment
│   ├── AgentsPage.tsx        # /agents
│   ├── OrchestraPage.tsx     # /orchestra
│   ├── SquarespaceOrdersPage.tsx
│   ├── InvoicesPage.tsx
│   ├── GmailPage.tsx
│   ├── GCalendarPage.tsx
│   └── VirtualOffice.tsx     # /office
```

---

## Routes

| Path | Page | Purpose |
|------|------|---------|
| `/dashboard` | Home | KPIs, pipeline |
| `/coldcall` | ColdCallPage | Failed-test retest outreach, call scripts |
| `/leads` | LeadsPage | Lead CRUD |
| `/clients` | ClientsPage | Client profiles |
| `/knowledge` | KnowledgeBasePage | Document library (**Add Document** UI) |
| `/enrichment` | TestEnrichmentPage | Link 957 tests → 82 clients |
| `/tests` | TestsWrapper | Test records |
| `/invoices` | CashFlo invoicing |
| `/squarespace` | Orders |
| `/agents` | AI agent roster |
| `/orchestra` | AI Orchestra |
| `/office` | Virtual office |
| `/calendar`, `/emails` | Google integrations |

---

## tRPC API (live, mostly unauthenticated)

### Queries (GET works today)

| Procedure | Example use |
|-----------|-------------|
| `leads.list` | All leads (389+ records) |
| `clients.list` | 92 clients |
| `jobs.list` | 957 OBD/smoke tests; filter `passFailStatus: "Fail"` for cold call table |
| `knowledge.list` | Docs with `title`, `category`, `content`, `source_file`, `tags` |
| `invoices.list` | 232 invoices |
| `squarespace.list` | Squarespace orders |
| `dashboard.stats` | Revenue, pass/fail counts |
| `jobs.stats` | Test aggregates |

Example:

```bash
curl -s 'https://gumption.manus.space/api/trpc/jobs.list?input={"json":{"passFailStatus":"Fail","limit":5}}'
```

### Mutations (exist but require POST)

| Procedure | Used by |
|-----------|---------|
| `leads.create` | LeadsPage |
| `leads.update` | LeadsPage, follow-ups |
| `clients.create` / `clients.update` | ClientsPage |
| `jobs.update` | Test enrichment / call status |
| `invoices.create` / `invoices.update` | CashFlo |
| `jobs.createPlaceholderInvoice` | Billing workflow |

### Missing mutations (gaps for your feature request)

| Expected | Status |
|----------|--------|
| `knowledge.create` | **Not in client bundle** — "Add Document" button has no `useMutation` |
| `knowledge.update` / `delete` | Not exposed |
| `leads.importCsv` | Not exposed — CSV import is manual today |
| `coldcall.*` | No router — Cold Call uses `jobs.list` + static UI |
| File upload endpoint | **None** |

---

## Knowledge Base — existing “assimilation” model

`knowledge.list` returns documents that were **already ingested** (likely via Manus build-time seed or one-off script):

| id | title | source_file |
|----|-------|-------------|
| 1 | AI Agents Orchestrator | `agents-orchestrator.md` |
| 2 | NorCal site plan | `BGnewsiteplanaddlocationsfixthisisv1.txt` |
| 3–5 | Blog posts | `BLOG_POSTS_READY.md.gdoc` |
| 6 | GIA deploy zip | `GIA_Deploy_2026-02-13(3).zip` |

**Schema (inferred):**

```ts
{
  id: number;
  title: string;
  category: string;  // "AI & Automation" | "Strategy & Planning" | "Blog Posts" | ...
  content: string;   // full text stored in DB
  source_file: string;
  tags: string;      // comma-separated
  status: "active";
  created_at: string;
  updated_at: string;
}
```

UI (`KnowledgeBasePage.tsx`) already renders `source_file` and has **Add Document** + search — but **no upload/create pipeline is wired**.

---

## Cold Calls module

- Route: `/coldcall`
- Data: `jobs.list` with `passFailStatus: "Fail"` (69 failed vehicles)
- UI: call status dropdown (Not Called, Left Voicemail, …), scripts accordion, link to `/enrichment`
- **No** `coldcall.import` — Hayward CSV from `briefs` repo must be pasted/imported manually or via new `leads.create` loop

---

## Security findings (important)

1. **Passcode is client-side only** (`PasscodeGate.tsx` in bundle). Anyone can call tRPC without unlocking.
2. **tRPC read endpoints are public** (`leads.list`, `clients.list`, `knowledge.list`, etc.).
3. **Mutations are unprotected** — POST to `leads.create` would work if discovered.

Before adding file upload, add **server-side auth** (API key, session cookie, or Manus SSO).

---

## Implementation spec: file upload → assimilate into code/Knowledge

### Goal

Upload `.md`, `.txt`, `.csv`, `.json`, `.zip` (and optionally `.pdf`) → parse → store as Knowledge doc (and optionally spawn Leads / Cold Call rows).

### Phase 1 — Backend (`server/routers/knowledge.ts`)

```ts
// knowledge.ingestFile (mutation)
input: {
  filename: string;
  mimeType: string;
  contentBase64: string;  // or multipart on Express
  category?: string;
  tags?: string[];
}
output: { docId: number; title: string; bytesIngested: number }

// Parser pipeline
switch (ext) {
  case '.md':
  case '.txt':  content = utf8; title = filename; break;
  case '.csv':  rows = parseCsv; content = summarize(rows); tags += 'csv,leads'; break;
  case '.json': content = JSON.stringify(parsed, null, 2); break;
  case '.zip':  extract text/md entries only; store manifest in content; break;
}
await db.insert(knowledgeDocs).values({ title, category, content, source_file: filename, tags });
await storage.put(`/manus-storage/uploads/${id}_${filename}`, buffer);  // optional binary retention
```

### Phase 2 — Frontend (`KnowledgeBasePage.tsx`)

Wire **Add Document** to:

```tsx
<input type="file" accept=".md,.txt,.csv,.json,.zip" hidden ref={fileRef} />
// on change → FileReader.readAsDataURL → trpc.knowledge.ingestFile.mutate(...)
```

Add `tt.knowledge.ingestFile.useMutation` + invalidate `knowledge.list` on success.

### Phase 3 — CSV → Leads + Cold Calls

```ts
// leads.importCsv (mutation)
input: { csvText: string; source?: string }
// For each row: map Company→company, Phone→phone, Priority→score tier
// → leads.create in transaction
// Optionally set stage: "New" for Cold Call tracking
```

Reuse column layout from `leads/gumption-cold-calls-import.csv` in this repo.

### Phase 4 — Optional AI assimilation

After text extract, call LLM once:

- Propose `category` + `tags`
- Generate 3-bullet summary prepended to `content`
- For code files: store under `category: "Code"` with syntax hint in tags

---

## How to get the actual source code

1. Log into **Manus** → project for `gumption.manus.space` → Export / Connect GitHub.  
2. Or download the Manus project ZIP if offered.  
3. Search exported tree for `client/src/pages/KnowledgeBasePage.tsx` — that is the file to extend.  
4. Clone into `BelichickGillisMusk/gumption` and wire CI deploy back to Manus.

Until export, use this doc + `curl` probes against `/api/trpc` as the contract.

---

## Related files in `briefs` repo

| File | Role |
|------|------|
| `leads/gumption-cold-calls-import.csv` | Cold Calls import schema |
| `leads/Leads_2026-05-22.csv` | CRM import + `sms_body` |
| `briefs/hayward-leads-2026-05-22-outreach.json` | Outreach metadata |

---

## Next steps (recommended order)

1. Export Gumption source from Manus → GitHub `gumption` repo.  
2. Add server auth on tRPC middleware.  
3. Implement `knowledge.ingestFile` + wire Add Document UI.  
4. Implement `leads.importCsv` for Cold Call / Hayward batches.  
5. Redeploy to `gumption.manus.space`.
