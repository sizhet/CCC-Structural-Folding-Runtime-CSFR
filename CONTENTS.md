# CONTENTS — CCC Structural Folding Runtime (CSFR)

## Repository Navigation and Reading Map

**CCC Structural Folding Runtime (CSFR)**
**From Metric-Space Objects to Runtime Localization**

---

# 1. Core Question

CSFR focuses on one central question:

> **How does a set of metric-space objects become a folded CCC structure that can support runtime localization?**

The core progression is:

$$
\boxed{
Representation
\rightarrow
Metric
\rightarrow
Cluster
\rightarrow
Structural\ Merge
\rightarrow
CCC
\rightarrow
Localization
}
$$

At scale:

$$
\boxed{
CCC
\rightarrow
DNA
\rightarrow
Retrieve
\rightarrow
Verify
\rightarrow
Localization
}
$$

---

# 2. Recommended Reading Order

For first-time readers:

```text
README.md
   ↓
START-HERE.md
   ↓
CSFR-001
   ↓
CSFR-002
   ↓
CSFR-003
   ↓
CSFR-004
   ↓
CSFR-005
   ↓
CASE-001
```

For a fast conceptual path:

```text
README
→ CSFR-001
→ CSFR-003
→ CSFR-004
→ CSFR-005
```

For implementation-oriented readers:

```text
CSFR-002
→ CSFR-003
→ CSFR-004
→ CSFR-005
```

---

# 3. Repository Structure

```text
CCC-Structural-Folding-Runtime-CSFR/
│
├── README.md
├── START-HERE.md
├── CONTENTS.md
│
├── CSFR-001-From-Metric-Clusters-to-Structural-Folding-Runtime.md
├── CSFR-002-Metric-Representation-and-Composite-Structural-Distance.md
├── CSFR-003-Sequence-Claw-Dragon-Merge-and-Cluster-CCC.md
├── CSFR-004-CCC-Metric-and-Runtime-Structural-Localization.md
├── CSFR-005-CCC-DNA-Two-Way-Dispatch-and-Two-Phase-Structural-Search.md
│
├── cases/
│   └── CASE-001-Stock-Market-Structural-Folding.md
│
├── figures/
│   ├── Fig-001-CSFR-Grand-Map.png
│   ├── Fig-002-Pattern-to-Pattern-vs-Pattern-to-CCC-Metric.png
│   ├── Fig-003-Sequence-Claw-Dragon-Merge.png
│   ├── Fig-004-Cluster-CCC-Structural-Possibility-Set.png
│   └── Fig-005-Two-Way-CCC-Runtime.png
│
├── FIGURE-INDEX.md
├── GLOSSARY.md
├── FUTURE-DIRECTIONS.md
├── CHANGELOG.md
├── CITATION.cff
└── .zenodo.json
```

---

# 4. Entry Documents

## `README.md`

**Purpose:** Repository-level overview.

Covers:

* what CSFR is;
* why clustering alone is insufficient;
* Cluster CCC;
* \(D_{PP}\), \(D_{PC}\), \(D_{CC}\);
* Structural Localization;
* CCC DNA;
* Two-Way CCC;
* Two-Phase Structural Search;
* relationship to SMSF.

Use this as the main repository landing page.

---

## `START-HERE.md`

**Purpose:** 10–15 minute conceptual introduction.

Focuses on:

```text
one central question
three metric relationships
one structural merge
one runtime localization process
one scalable Two-Phase search
```

Recommended for readers entering the repository for the first time.

---

## `CONTENTS.md`

**Purpose:** Repository navigation and reading map.

Use this file to locate:

* core papers;
* application cases;
* figures;
* supporting documents;
* recommended reading sequences.

---

# 5. Core Paper Series

---

## CSFR-001 — From Metric Clusters to Structural Folding Runtime

**File**

`CSFR-001-From-Metric-Clusters-to-Structural-Folding-Runtime.md`

**Role**

Foundation and overall thesis.

**Central question**

> How does a metric-space cluster become a reusable runtime structure?

**Key ideas**

```text
Cluster ≠ Runtime Structure
Metric Organization
Structural Folding
Cluster CCC
Runtime Localization
```

**Core transformation**

$$
Metric\ Cluster
\rightarrow
Structural\ Merge
\rightarrow
Cluster\ CCC.
$$

**Recommended for**

Everyone.

This is the conceptual entry point to the paper series.

---

## CSFR-002 — Metric Representation and Composite Structural Distance

**File**

`CSFR-002-Metric-Representation-and-Composite-Structural-Distance.md`

**Role**

Defines the pre-folding representation and metric substrate.

**Key topics**

```text
Generic Structural Representation
Named Numeric Values
Named Categorical Values
Numeric Sequences
Categorical Sequences
Bucketing
Bigrams
Trigrams
Forward / Reverse Descriptors
Composite Structural Metric
```

**Primary metric**

$$
\boxed{
D_{PP}
:
Object
\leftrightarrow
Object
}
$$

**Used for**

```text
nearest-pair analysis
metric-space clustering
candidate K discovery
structural organization
```

**Key idea**

> Structurally different evidence should not be forced prematurely into one primitive geometry.

---

## CSFR-003 — Sequence Claw-Dragon Merge and Cluster CCC

**File**

`CSFR-003-Sequence-Claw-Dragon-Merge-and-Cluster-CCC.md`

**Role**

Defines the central CSFR folding algorithm.

**Key topics**

```text
General Claw-Dragon Merge
Equal-Length Sequence Special Case
Strict Positional Alignment
Per-Position Distribution Merge
Policy Filtering
Cluster CCC
Core + Delta
Selected Uncertainty Preservation
```

**Canonical result**

$$
CCC_C
=
[P_0,P_1,\ldots,P_{n-1}].
$$

Each:

$$
P_j
=
\{(v_1,w_1),(v_2,w_2),\ldots\}.
$$

**Core statement**

> **A Cluster CCC is a policy-compressed structural possibility set.**

**Key distinction**

$$
\boxed{
Cluster\ CCC \neq Centroid
}
$$

This is the most distinctive structural folding paper in the CSFR series.

---

## CSFR-004 — CCC Metric and Runtime Structural Localization

**File**

`CSFR-004-CCC-Metric-and-Runtime-Structural-Localization.md`

**Role**

Turns folded CCC structures into runtime dispatch structures.

**Primary metric**

$$
\boxed{
D_{PC}
:
Object
\leftrightarrow
Cluster\ CCC
}
$$

**Key topics**

```text
Object-to-CCC Distance
Weighted Consensus Distance
Runtime Dispatch
Top-1
Top-N
Margin
Threshold
UNKNOWN
Fallback
Beam Search
Structural Localization
Per-Node Intelligence
```

**Canonical runtime chain**

$$
CCC
\rightarrow
D_{PC}
\rightarrow
Dispatch
\rightarrow
Localization
\rightarrow
Per\text{-}Node\ Intelligence.
$$

**Key principle**

$$
\boxed{
Localization
\rightarrow
Local\ Intelligence
}
$$

rather than immediately:

$$
Object
\rightarrow
Global\ Prediction.
$$

---

## CSFR-005 — CCC DNA, Two-Way Dispatch, and Two-Phase Structural Search

**File**

`CSFR-005-CCC-DNA-Two-Way-Dispatch-and-Two-Phase-Structural-Search.md`

**Role**

Adds reverse structural access and scalable runtime search.

**Key topics**

```text
CCC DNA
Structural Tokens
Reverse Index
Two-Way CCC
Candidate Retrieval
Weighted Voting
Structural TF-IDF
Two-Phase Search
Direct Structural Jumping
Cross-Branch Recovery
Scalable Localization
```

**Canonical scalable runtime**

$$
Object
\rightarrow
DNA
\rightarrow
Candidate\ CCCs
\rightarrow
D_{PC}
\rightarrow
Localization.
$$

**Core principle**

$$
\boxed{
Retrieve\ First,
Verify\ Second
}
$$

**Key distinction**

$$
DNA(CCC)
\neq
CCC.
$$

CCC DNA is the retrieval handle.

The full CCC remains the structural truth source.

---

# 6. The Three CSFR Metrics

The core papers distinguish three relationships.

| Metric     | Relationship         | Primary Role                              |
| ---------- | -------------------- | ----------------------------------------- |
| \(D_{PP}\) | Object ↔ Object      | clustering and structural discovery       |
| \(D_{PC}\) | Object ↔ Cluster CCC | runtime dispatch and localization         |
| \(D_{CC}\) | CCC ↔ CCC            | CCC organization and structural evolution |

A compact interpretation is:

```text
D_PP → Discover

D_PC → Localize

D_CC → Organize / Evolve
```

---

# 7. Canonical Application Case

## CASE-001 — Stock-Market Structural Folding

**File**

`cases/CASE-001-Stock-Market-Structural-Folding.md`

**Purpose**

Demonstrates how CSFR maps into the Stock-Market Structural Folding problem.

Mapping:

| CSFR                         | SMSF                               |
| ---------------------------- | ---------------------------------- |
| Object                       | Stock Pattern                      |
| Generic Structural Container | Market Pattern Representation      |
| \(D_{PP}\)                   | Stock Pattern Distance             |
| Metric Cluster               | Historical Pattern Cluster         |
| Structural Merge             | Aligned Sequence Merge             |
| Cluster CCC                  | Stock-Regime CCC                   |
| \(D_{PC}\)                   | Current Pattern ↔ Regime CCC       |
| Structural Localization      | Current Market-Regime Localization |
| Per-Node Intelligence        | Local Historical Outcome / Policy  |

SMSF is the canonical application.

CSFR is the reusable runtime.

$$
\boxed{
SMSF = Application
}
$$

$$
\boxed{
CSFR = Runtime\ Infrastructure
}
$$

---

# 8. Figure Set

See:

`FIGURE-INDEX.md`

The planned five core figures are:

### Fig-001 — CCC Structural Folding Runtime Grand Map

Overall architecture:

```text
Representation
→ Metric
→ Cluster
→ Folding
→ CCC
→ Localization
```

---

### Fig-002 — Pattern-to-Pattern vs Pattern-to-CCC Metric

Focus:

$$
D_{PP}
$$

versus:

$$
D_{PC}.
$$

Shows the transition from:

```text
value ↔ value
```

to:

```text
value ↔ structural possibility set
```

---

### Fig-003 — Sequence Claw-Dragon Merge

Shows:

```text
General Structural Merge
        ↓
Equal Length + Strict Alignment
        ↓
Per-Position Distribution Merge
        ↓
Cluster CCC
```

This is the key structural folding figure.

---

### Fig-004 — Cluster CCC as Structural Possibility Set

Shows:

$$
Cluster\ CCC
\neq
Centroid.
$$

Focuses on:

```text
multiple retained alternatives
weights
policy filtering
Core + Delta
selected uncertainty
```

---

### Fig-005 — Two-Way CCC Runtime

Shows:

```text
CCC DNA
→ Reverse Index
→ Candidate Retrieval
→ D_PC Verification
→ Localization
```

and the relationship between:

```text
forward metric dispatch
```

and:

```text
reverse structural retrieval.
```

---

# 9. Supporting Documents

## `FIGURE-INDEX.md`

Purpose:

* figure titles;
* figure descriptions;
* recommended insertion locations;
* relationships between figures and core papers.

---

## `GLOSSARY.md`

Purpose:

Defines the main CSFR terms, including:

```text
CCC
Cluster CCC
Structural Folding
Claw-Dragon Merge
D_PP
D_PC
D_CC
Structural Localization
CCC DNA
Two-Way CCC
Two-Phase Search
Per-Node Intelligence
UNKNOWN
Core + Delta
```

---

## `FUTURE-DIRECTIONS.md`

Purpose:

Tracks research directions beyond the initial CSFR runtime.

Expected topics include:

```text
general non-aligned Claw-Dragon Merge
D_CC
CCC hierarchy construction
adaptive folding policies
learned metric policies
structural novelty
continual CCC growth
approximate structural search
hardware acceleration
cross-domain CCC reuse
```

---

## `CHANGELOG.md`

Purpose:

Tracks repository evolution and release milestones.

---

## `CITATION.cff`

Purpose:

Machine-readable citation metadata for GitHub and scholarly reuse.

---

## `.zenodo.json`

Purpose:

Zenodo release metadata for DOI publication.

---

# 10. Reading Paths by Interest

## Theory / Conceptual Architecture

```text
README
→ START-HERE
→ CSFR-001
→ CSFR-003
→ CSFR-004
```

---

## Metric Engineering

```text
CSFR-002
→ CSFR-003
→ CSFR-004
```

Focus:

```text
representation
D_PP
folding compatibility
D_PC
```

---

## Structural Folding

```text
CSFR-001
→ CSFR-003
→ CSFR-004
```

Focus:

$$
Cluster
\rightarrow
CCC
\rightarrow
Runtime.
$$

---

## Runtime / Dispatch

```text
CSFR-004
→ CSFR-005
```

Focus:

```text
D_PC
dispatch policy
localization
UNKNOWN
reverse retrieval
Two-Phase search
```

---

## Large-Scale Search

```text
CSFR-005
```

Focus:

```text
CCC DNA
reverse index
candidate reduction
candidate recall
Two-Way CCC
metric verification
```

---

## Stock-Market Application

```text
START-HERE
→ CSFR-003
→ CSFR-004
→ CASE-001
```

---

# 11. Minimal Implementation Path

A minimal CSFR prototype can be built in four stages.

## Stage 1 — Metric Layer

Implement:

```text
Generic Structural Object
D_PP
basic sequence distance
```

Read:

`CSFR-002`

---

## Stage 2 — Folding Layer

Implement:

```text
aligned sequence cluster
per-position counting
normalization
policy filtering
Sequence Cluster CCC
```

Read:

`CSFR-003`

---

## Stage 3 — Runtime Layer

Implement:

```text
D_PC
Top-1 dispatch
threshold
UNKNOWN
localization path
```

Read:

`CSFR-004`

---

## Stage 4 — Search Layer

Implement:

```text
CCC DNA
reverse index
Top-K candidate retrieval
D_PC verification
```

Read:

`CSFR-005`

---

# 12. Core Architecture in One View

```text
OFFLINE
────────────────────────────────────────

Objects
  ↓
Structural Representation
  ↓
D_PP
  ↓
Metric-Space Clustering
  ↓
Structural Merge
  ↓
Cluster CCC
  ↓
CCC DNA
  ↓
Reverse Index


ONLINE
────────────────────────────────────────

Incoming Object
  ↓
Structural Encoding
  ↓
Object DNA
  ↓
Candidate Retrieval
  ↓
D_PC Verification
  ↓
Dispatch
  ↓
Structural Localization
  ↓
Per-Node Intelligence
```

---

# 13. The Five Core Ideas

The repository can be reduced to five ideas.

### 1. Cluster is not yet runtime structure.

$$
Cluster
\neq
Runtime\ Structure.
$$

### 2. Structural merge creates Cluster CCC.

$$
Cluster
\rightarrow
CCC.
$$

### 3. Cluster CCC can preserve structural alternatives.

$$
CCC
=
Policy\text{-}Compressed\ Structural\ Possibility\ Set.
$$

### 4. \(D_{PC}\) turns CCC into a runtime dispatch interface.

$$
CCC
+
D_{PC}
\rightarrow
Localization.
$$

### 5. CCC DNA makes localization scalable.

$$
DNA
\rightarrow
Retrieve
\rightarrow
Verify.
$$

---

# 14. One-Line Repository Map

$$
\boxed{
CSFR\text{-}001
\rightarrow
CSFR\text{-}002
\rightarrow
CSFR\text{-}003
\rightarrow
CSFR\text{-}004
\rightarrow
CSFR\text{-}005
}
$$

means:

$$
\boxed{
Why
\rightarrow
Metric
\rightarrow
Fold
\rightarrow
Run
\rightarrow
Scale
}
$$

---

# 15. Final Navigation Summary

If you are new:

**Start with `README.md` and `START-HERE.md`.**

If you want the main theoretical argument:

**Read `CSFR-001`.**

If you want the core folding algorithm:

**Read `CSFR-003`.**

If you want the runtime:

**Read `CSFR-004`.**

If you want scalable reverse structural search:

**Read `CSFR-005`.**

If you want implementation details for representation and metric construction:

**Read `CSFR-002`.**

If you want the canonical application:

**Read `cases/CASE-001-Stock-Market-Structural-Folding.md`.**

---

**CCC Structural Folding Runtime (CSFR)**
*From Metric-Space Objects to Runtime Localization*
