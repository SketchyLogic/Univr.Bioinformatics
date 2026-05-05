---
tags:
  - __DEFINITION
  - Module1
CreatedAt: 2026-05-02
LastUpdateAt: 2026-05-02
LastReviewAt: null
ReviewerIds:
  - admin
OwnerIds:
  - admin
IssueNotes: null
GeneratedById: claude-sonnet-4-6
---

**Generic Feature Format version 3** — the standard tab-separated text file format for storing genome annotation. Each line describes one genomic feature.

**Columns** (9 fields, tab-separated):

| # | Field | Description |
|---|-------|-------------|
| 1 | `seqname` | Chromosome or scaffold identifier |
| 2 | `source` | Program or database that generated the feature |
| 3 | `feature` | Feature type: `gene`, `transcript`, `exon`, `CDS`, `UTR`, etc. |
| 4 | `start` | 1-based start coordinate |
| 5 | `end` | End coordinate (inclusive) |
| 6 | `score` | Numeric score or `.` if absent |
| 7 | `strand` | `+` (forward), `-` (reverse), or `.` |
| 8 | `frame` | Reading frame (0, 1, 2) for CDS features, `.` otherwise |
| 9 | `attributes` | Semicolon-separated `key=value` pairs (ID, Name, Parent, biotype…) |

**Hierarchy**: features are linked via the `Parent` attribute. A `gene` record is the parent of one or more `transcript` records; each `transcript` is the parent of its `exon` and `CDS` records.

**Example** (simplified from Vitis vinifera data):
```
1  Ensembl  gene        3028681  3030154  .  -  .  ID=Vv01s0011g03340
1  Ensembl  transcript  3028681  3030154  .  -  .  ID=Vv01s0011g03340.t01;Parent=Vv01s0011g03340
1  Ensembl  exon        3030130  3030154  .  -  1  Parent=Vv01s0011g03340.t01
1  Ensembl  CDS         3030130  3030154  .  -  1  Parent=Vv01s0011g03340.t01
```

GFF3 is the most widely used format for exchanging annotation between genome browsers (e.g., Ensembl, JBrowse) and annotation tools. The related **GTF** format (used by Ensembl/GENCODE) uses `gene_id` and `transcript_id` attributes rather than the `Parent` hierarchy.
