# Work Repo

The single source of truth for one loan officer's entire book of business,
managed by [Mortgage Work](https://github.com/) (the desktop IDE). The LO never
touches this repo directly — the IDE clones it, edits it, commits it, and syncs
it. Everything else (vector / graph / SQL indexes) is derived from this repo
and can be rebuilt from it at any time.

## Layout

```
.
├── clients/              # one folder per client, named by slug
│   └── <client-slug>/
│       ├── client.yaml   # machine-managed structured facts (see below)
│       ├── PROFILE.md    # free-form profile — AI-maintained, human-editable
│       └── …             # any files/folders the LO likes (income/, assets/, …)
└── products/             # one folder per lender, named as the LO likes
    ├── index.jsonl      # machine-managed global doc_id → path index (see below)
    └── <lender>/
        └── …             # guidelines, matrices, rate sheets — any layout
```

Rules the IDE enforces (and everything it assumes):

- A **client exists iff its folder exists** under `clients/`. `client.yaml` is
  the description, not the existence test — if it's missing or unparsable the
  client still shows up, flagged for repair (AI rebuilds it from the folder).
- Inside a client folder the layout is **free**. The conventional scaffold
  (`income/ assets/ credit/ ai/`) is only a starting point.
- `products/` folders carry **no hand-written metadata**. Folder name = lender
  name, files are the product docs. The only reserved file is
  `products/index.jsonl`, written by the IDE. Indexing status is runtime state
  and never stored here.
- A repo is considered valid iff `clients/` and `products/` exist at the root.

## client.yaml

Machine-managed: the IDE writes it, parsers read it, humans stay out. Only
facts that cannot be derived from the folder go in here — counts, timestamps,
and analysis results are computed, never stored.

```yaml
schema: 1                       # client.yaml schema version
name: Sarah Mitchell            # display name (folder name is the slug)
purpose: purchase               # purchase | refinance | cash_out_refinance |
                                #   heloc | investment
amount: 680000                  # target loan amount, USD, integer
stage: docs                     # lead | docs | active | closed
city: Irvine, CA                # optional
contact:                        # optional
  phone: "+1 (949) 555-0134"
  email: sarah@example.com
borrowers:                      # ≥1; first entry is the primary borrower
  - name: Sarah Mitchell
    citizenship: us_citizen     # us_citizen | permanent_resident |
                                #   non_permanent_resident | foreign_national
created: 2026-07-10             # date the client file was opened
closed: 2026-09-30              # only present when stage == closed
```

## products/index.jsonl

Machine-managed global index mapping every file in the repo (clients +
products) to its `doc_id`. Agents reference documents by `doc_id`; this file
is how a `doc_id` resolves back to a physical file.

- `doc_id` is the **xxh64 content hash** of the file — byte-for-byte the same
  algorithm as kg-service, so the IDs line up with `allowed_doc_ids` and the
  graph's `Product.doc_ids` by construction.
- Content is the identity: renaming keeps the doc_id, editing changes it.
- Updated automatically on every file CRUD (rides in the same commit).
- The same file may appear under multiple paths — each gets its own record.

```jsonl
{"doc_id": "ef73ecbb4dff95b4", "path": "products/itrust/DSCR 10.22.24.pdf", "size": 140922, "indexed_at": "2026-08-05T12:00:00Z"}
```

## Conventions

- `*.ai` files are AI-generated output — plain markdown under the hood, the
  extension only drives the badge/viewer in the IDE.
- Empty folders are kept in git with a `.gitkeep` placeholder.
- Commits are made automatically by the IDE (debounced after file activity);
  history is surfaced to the LO as the "History" panel, never as raw git.
