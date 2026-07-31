# Expected: priya-raman

| Fact | Expected value | Sole source | Commit | Trap |
|---|---|---|---|---|
| borrower | Priya Raman · borrower · us_citizen (sole) | `client.yaml` | `open(raman): intake call…` | — |
| purpose | purchase, primary residence | `client.yaml` | `open(raman): intake call…` | — |
| city | San Jose, CA | `client.yaml` | `open(raman): intake call…` | — |
| property | 908 Larkspur Lane, San Jose, CA 95126 · SFR | `PROFILE.md` | `open(raman): intake call…` | — |
| purchase price | $1,150,000 | `PROFILE.md` | `open(raman): intake call…` | — |
| loan amount | $920,000 | `client.yaml` | `open(raman): intake call…` | — |
| LTV | 80.0% | `PROFILE.md` | `open(raman): intake call…` | — |
| stage | active | `client.yaml` | `docs(raman): CPA-prepared P&L…` | — |
| business | Raman Design Studio, sole proprietorship, since 2019 | `PROFILE.md` | `open(raman): intake call…` | — |
| credit score | both reported: PROFILE.md says FICO 712; credit-report.pdf says FICO 694 | `PROFILE.md`, `credit/credit-report.pdf` | — | T5 |
| credit pull date | 2026-07-13 | `credit/credit-report.pdf` | `docs(raman): credit pulled…` | — |
| tax transcript | image-only scan, no text layer | `credit/tax-transcript-2025.pdf` | `docs(raman): credit pulled…` | T8 |
| 12-month deposit total | $572,200 | `assets/bank-statement-*.pdf` (sum of all twelve) | `docs(raman): business bank statements…` | — |
| large deposit excluded | $73,000 INCOMING WIRE on 2026-05-19 | `assets/bank-statement-2026-05.pdf` | `docs(raman): business bank statements…` | T1 |
| average monthly deposits | $41,600 | `ai/income-analysis.ai` | `docs(raman): CPA-prepared P&L…` | — |
| expense factor | 50% | `ai/income-analysis.ai` | `docs(raman): CPA-prepared P&L…` | — |
| qualifying income | $20,800/mo | `ai/income-analysis.ai` | `docs(raman): CPA-prepared P&L…` | — |
| PITIA | $9,200/mo | `ai/income-analysis.ai` | `docs(raman): CPA-prepared P&L…` | — |
| other monthly debts | $1,616/mo | `ai/income-analysis.ai` | `docs(raman): CPA-prepared P&L…` | — |
| back-end DTI | 52.0% — exceeds program maximum | `ai/income-analysis.ai` | `docs(raman): CPA-prepared P&L…` | T7 |
| self-prepared P&L net income | $512,000 | `income/pl-2025-draft.pdf` | `docs(raman): self-prepared P&L…` | T3 |
| CPA-prepared P&L net income | $498,000 (supersedes draft) | `income/pl-2025-cpa.pdf` | `docs(raman): CPA-prepared P&L…` | T3 |
| appraisal status | unknown | — | — | T4 |
