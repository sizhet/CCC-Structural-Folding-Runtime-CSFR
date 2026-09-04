# FIGURE INDEX — CCC Structural Folding Runtime (CSFR)

## Core Figure Set and Recommended Placement

**CCC Structural Folding Runtime (CSFR)**
**From Metric-Space Objects to Runtime Localization**

---

# 1. Figure Set Overview

CSFR uses five core figures.

Together they follow the same progression as the five core papers:

```text
Fig-001
Overall Runtime Architecture
        ↓
Fig-002
Metric Transition
        ↓
Fig-003
Structural Folding
        ↓
Fig-004
Cluster CCC Semantics
        ↓
Fig-005
Scalable Two-Way Runtime
```

The complete visual narrative is:

$$
\boxed{
Representation
\rightarrow
Metric
\rightarrow
Cluster
\rightarrow
Fold
\rightarrow
CCC
\rightarrow
Retrieve
\rightarrow
Verify
\rightarrow
Localization
}
$$

---

# 2. Recommended File Names

```text
figures/
├── Fig-001-CSFR-Grand-Map.png
├── Fig-002-Pattern-to-Pattern-vs-Pattern-to-CCC-Metric.png
├── Fig-003-Sequence-Claw-Dragon-Merge.png
├── Fig-004-Cluster-CCC-Structural-Possibility-Set.png
└── Fig-005-Two-Way-CCC-Runtime.png
```

If the current generated artwork uses longer names, these concise repository names are recommended for consistency.

---

# 3. Fig-001 — CCC Structural Folding Runtime Grand Map

**Recommended file**

`figures/Fig-001-CSFR-Grand-Map.png`

## Purpose

This is the canonical overview figure for the entire repository.

It should communicate the end-to-end transformation:

```text
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
D_PC
  ↓
Runtime Dispatch
  ↓
Structural Localization
  ↓
Per-Node Intelligence
```

The scalable branch should also show:

```text
Cluster CCC
  ↓
CCC DNA
  ↓
Reverse Index
  ↓
Candidate Retrieval
  ↓
Metric Verification
```

## Main Message

> **CSFR transforms metric-space object collections into folded, searchable, runtime-localizable CCC structures.**

## Primary Paper

`CSFR-001-From-Metric-Clusters-to-Structural-Folding-Runtime.md`

## Recommended Insertion Position

Insert after the introductory explanation of the canonical CSFR transformation:

```text
Objects
→ Metric Space
→ Clusters
→ Structural Merge
→ Cluster CCCs
→ CCC Metric
→ Runtime Localization
```

A strong location is immediately after the early section that establishes:

$$
Cluster \neq Runtime\ Structure.
$$

## Secondary Placement

Also suitable near the top of:

`README.md`

Recommended placement:

* after the title/subtitle;
* before the first detailed conceptual section.

Avoid placing all five figures in README.

Fig-001 alone is sufficient as the repository hero diagram.

## Caption

**Fig-001 — CCC Structural Folding Runtime Grand Map.**
The complete CSFR pipeline transforms heterogeneous metric-space objects into clusters, folds those clusters into reusable CCC structures, and uses CCC metrics, structural DNA, reverse indexing, and runtime dispatch to support scalable structural localization and Per-Node Intelligence.

---

# 4. Fig-002 — Pattern-to-Pattern vs Pattern-to-CCC Metric

**Recommended file**

`figures/Fig-002-Pattern-to-Pattern-vs-Pattern-to-CCC-Metric.png`

## Purpose

This figure explains the most important metric transition in CSFR:

$$
D_{PP}
\rightarrow
D_{PC}.
$$

It should distinguish:

### Pattern-to-Pattern

$$
D_{PP}
:
Object
\leftrightarrow
Object
$$

used for:

```text
clustering
nearest-pair analysis
metric-space organization
```

from:

### Pattern-to-CCC

$$
D_{PC}
:
Object
\leftrightarrow
Cluster\ CCC
$$

used for:

```text
runtime dispatch
candidate verification
structural localization
```

## Main Message

> **The target changes from a concrete object to a folded structural possibility set.**

The figure should visually contrast:

```text
value ↔ value
```

with:

```text
value ↔ weighted possibility set
```

## Primary Paper

`CSFR-004-CCC-Metric-and-Runtime-Structural-Localization.md`

## Recommended Insertion Position

Insert shortly after the section:

**Why D_PC Is Not D_PP**

and before the detailed weighted-consensus equations.

This lets the visual distinction appear before the formal metric definition.

## Secondary Paper

`CSFR-002-Metric-Representation-and-Composite-Structural-Distance.md`

A secondary placement may be near the closing transition:

```text
Objects
→ D_PP
→ Cluster
→ CCC
→ D_PC
```

However, avoid duplicating the same figure in both papers unless desired.

Preferred primary home:

**CSFR-004**.

## Caption

**Fig-002 — Pattern-to-Pattern vs Pattern-to-CCC Metric.**
CSFR separates object-to-object distance \(D_{PP}\), used for metric-space organization and clustering, from object-to-CCC distance \(D_{PC}\), used for runtime comparison against folded structural possibility sets and subsequent localization.

---

# 5. Fig-003 — Sequence Claw-Dragon Merge

**Recommended file**

`figures/Fig-003-Sequence-Claw-Dragon-Merge.png`

## Full Conceptual Title

**Sequence Claw-Dragon Merge: General Form → Aligned Sequence Degeneration**

## Purpose

This is the core algorithmic figure of CSFR.

It should show the transition from the general sequence structural merge problem:

```text
different lengths
different alignments
branching
correspondence uncertainty
many interacting structural paths
```

to the favorable special case:

$$
Equal\ Length
+
Strict\ Positional\ Alignment.
$$

Under these constraints:

```text
General Claw-Dragon Merge
        ↓
Alignment Is Already Known
        ↓
Collect Values Per Position
        ↓
Count / Weight
        ↓
Policy Filter
        ↓
Position CCCs
        ↓
Sequence Cluster CCC
```

## Main Message

> **When sequence length and positional meaning are fixed, a difficult general structural merge collapses into a simple per-position distribution merge.**

This is one of the most distinctive CSFR algorithmic results.

## Primary Paper

`CSFR-003-Sequence-Claw-Dragon-Merge-and-Cluster-CCC.md`

## Recommended Insertion Position

Insert after the sections:

* **The Claw-Dragon Metaphor**
* **The Equal-Length Aligned Special Case**

and before the detailed per-position counting example.

The figure should visually bridge:

```text
general problem
```

and:

```text
engineering reduction.
```

## Secondary Placement

Also appropriate in:

`cases/CASE-001-Stock-Market-Structural-Folding.md`

Specifically after the section:

**Why Stock Patterns Provide a Favorable Merge Case**

However, primary placement should remain in CSFR-003.

## Caption

**Fig-003 — Sequence Claw-Dragon Merge: General Form to Aligned-Sequence Reduction.**
General sequence structural merge may require alignment, correspondence, and branching resolution. When all sequences have equal length and strict positional alignment, the problem reduces to independent per-position aggregation followed by policy-driven filtering and Sequence Cluster CCC construction.

---

# 6. Fig-004 — Cluster CCC as Structural Possibility Set

**Recommended file**

`figures/Fig-004-Cluster-CCC-Structural-Possibility-Set.png`

## Purpose

This figure explains the semantic difference between:

$$
Centroid
$$

and:

$$
Cluster\ CCC.
$$

It should show a cluster position such as:

```text
UP      0.51
DOWN    0.45
FLAT    0.04
```

and contrast two folds.

### Centroid / Winner-Take-All

```text
UP
```

versus:

### Cluster CCC

```text
UP      0.51
DOWN    0.45
```

after policy filtering.

## Main Message

$$
\boxed{
Cluster\ CCC \neq Centroid
}
$$

and:

> **A Cluster CCC is a policy-compressed structural possibility set.**

The figure should make clear that CCC folding can preserve:

```text
multimodality
selected uncertainty
Core + Delta
structural alternatives
```

without preserving all raw cluster members.

## Primary Paper

`CSFR-003-Sequence-Claw-Dragon-Merge-and-Cluster-CCC.md`

## Recommended Insertion Position

Insert immediately after the section:

**Cluster CCC Is Not a Centroid**

or after:

**Structural Possibility Set**

This figure should appear before the later entropy, Core + Delta, and fold-quality discussion.

## Secondary Placement

Also suitable in:

`CSFR-001-From-Metric-Clusters-to-Structural-Folding-Runtime.md`

near the claim:

> A Cluster CCC is a policy-compressed structural possibility set.

But primary placement should remain in CSFR-003.

## Caption

**Fig-004 — Cluster CCC as a Structural Possibility Set.**
Unlike a centroid or winner-take-all representative, a Cluster CCC may preserve several structurally significant alternatives with weights. Policy-driven folding removes weak variation while retaining the Core and meaningful Delta required for future runtime comparison.

---

# 7. Fig-005 — Two-Way CCC Runtime

**Recommended file**

`figures/Fig-005-Two-Way-CCC-Runtime.png`

## Full Conceptual Title

**Two-Way CCC Runtime: DNA Retrieval → Metric Verification → Localization**

## Purpose

This figure completes the CSFR runtime architecture.

It should show two complementary access directions.

### Forward Metric Direction

$$
Object
\rightarrow
D_{PC}
\rightarrow
CCC.
$$

### Reverse Structural Direction

$$
Object\ DNA
\rightarrow
Reverse\ Index
\rightarrow
Candidate\ CCCs.
$$

These converge in:

```text
Candidate CCCs
      ↓
Full D_PC Verification
      ↓
Dispatch Policy
      ↓
Structural Localization
```

## Main Message

> **CCC DNA accelerates search; the full CCC metric remains the final structural verifier.**

The figure should clearly convey:

$$
Retrieve\ First,
Verify\ Second.
$$

## Primary Paper

`CSFR-005-CCC-DNA-Two-Way-Dispatch-and-Two-Phase-Structural-Search.md`

## Recommended Insertion Position

Insert after the sections:

* **Two-Way CCC**
* **Two-Phase Structural Search**

and before detailed candidate-scoring or index-implementation sections.

This allows the reader to see the complete architecture before entering implementation details.

## Secondary Placement

Also appropriate near the end of:

`CSFR-004-CCC-Metric-and-Runtime-Structural-Localization.md`

as a preview of scalable search.

However, preferred primary placement is CSFR-005.

## Caption

**Fig-005 — Two-Way CCC Runtime: DNA Retrieval, Metric Verification, and Localization.**
CSFR combines forward object-to-CCC metric dispatch with reverse CCC-DNA indexing. Cheap structural retrieval generates candidate CCCs, while full \(D_{PC}\) verification determines final runtime localization, enabling scalable Two-Phase structural search.

---

# 8. Figure-to-Paper Mapping

| Figure  | Primary Paper | Main Role                   |
| ------- | ------------- | --------------------------- |
| Fig-001 | CSFR-001      | Complete CSFR architecture  |
| Fig-002 | CSFR-004      | \(D_{PP}\) vs \(D_{PC}\)    |
| Fig-003 | CSFR-003      | Claw-Dragon merge reduction |
| Fig-004 | CSFR-003      | CCC vs centroid             |
| Fig-005 | CSFR-005      | Two-Way / Two-Phase runtime |

---

# 9. Recommended Article Placement Summary

## CSFR-001

Insert:

```text
Fig-001
```

Recommended location:

after the initial canonical transformation and the statement:

$$
Cluster \neq Runtime\ Structure.
$$

---

## CSFR-002

No figure is strictly required.

This paper is intentionally metric-focused.

If desired, reference:

```text
Fig-002
```

near the closing transition from \(D_{PP}\) toward \(D_{PC}\).

---

## CSFR-003

Insert:

```text
Fig-003
```

after introducing the aligned sequence special case.

Then insert:

```text
Fig-004
```

after explaining why Cluster CCC is not a centroid.

This paper appropriately receives two figures because it contains the central folding mechanism.

---

## CSFR-004

Insert:

```text
Fig-002
```

after:

**Why D_PC Is Not D_PP**

and before detailed consensus-distance formulas.

---

## CSFR-005

Insert:

```text
Fig-005
```

after:

**Two-Way CCC**

and:

**Two-Phase Structural Search**

before detailed reverse-index implementation.

---

# 10. CASE-001 Placement

For:

`cases/CASE-001-Stock-Market-Structural-Folding.md`

the preferred approach is to reference the core figures rather than duplicate all of them.

Most useful references are:

```text
Fig-003
Aligned Sequence Claw-Dragon Merge

Fig-004
Stock-Regime CCC as Structural Possibility Set

Fig-005
Two-Way Market CCC Runtime
```

If only one figure is inserted into CASE-001, use:

**Fig-003**

because the equal-length aligned stock-window case is the most direct application-specific bridge into CSFR.

---

# 11. README Placement

For a clean repository landing page, use only:

```text
Fig-001 — CSFR Grand Map
```

Recommended placement:

```text
Title
Subtitle
Short Introduction
Fig-001
Core Question
...
```

This keeps the README visually strong without turning it into a figure gallery.

The remaining figures belong in the core papers and `FIGURE-INDEX.md`.

---

# 12. START-HERE Placement

`START-HERE.md` does not require all five figures.

If one figure is used, prefer:

```text
Fig-001
```

after the section:

**The Entire CSFR Pipeline**

If a second figure is desired, use:

```text
Fig-003
```

after:

**The Aligned Sequence Claw-Dragon Reduction**

---

# 13. Visual Narrative Across the Five Figures

The five figures together should answer five questions.

### Fig-001

> What is the complete CSFR runtime?

### Fig-002

> What changes when the system moves from clustering to runtime comparison?

### Fig-003

> How does a sequence cluster become a CCC?

### Fig-004

> What exactly is preserved inside that CCC?

### Fig-005

> How can the resulting CCC space be searched efficiently at runtime?

Together:

$$
\boxed{
What
\rightarrow
Metric
\rightarrow
Fold
\rightarrow
Representation
\rightarrow
Scale
}
$$

---

# 14. Figure Dependency Map

```text
Fig-001
CSFR Grand Map
   │
   ├─────────────┐
   ▼             ▼
Fig-002        Fig-003
Metric         Structural Merge
Transition       │
                 ▼
              Fig-004
              Cluster CCC
                 │
                 ▼
              Fig-005
              Two-Way Runtime
```

This reflects the conceptual dependency among the figures.

---

# 15. Canonical Figure Captions

For easy repository use:

## Fig-001

**CCC Structural Folding Runtime Grand Map.**
End-to-end transformation from heterogeneous structural objects through metric organization, clustering, CCC folding, runtime dispatch, structural localization, and Per-Node Intelligence, with CCC DNA providing scalable reverse structural access.

## Fig-002

**Pattern-to-Pattern vs Pattern-to-CCC Metric.**
CSFR distinguishes \(D_{PP}\), used for object clustering, from \(D_{PC}\), used for comparing incoming objects with folded CCC possibility sets during runtime localization.

## Fig-003

**Sequence Claw-Dragon Merge: General Form to Aligned-Sequence Reduction.**
Equal-length and strictly aligned sequences eliminate the general correspondence problem, reducing structural merge to per-position aggregation, weighting, filtering, and Cluster CCC construction.

## Fig-004

**Cluster CCC as Structural Possibility Set.**
A Cluster CCC preserves policy-selected structural alternatives rather than forcing each cluster dimension into a single centroid or winner.

## Fig-005

**Two-Way CCC Runtime: DNA Retrieval to Metric Verification.**
CCC DNA provides fast reverse candidate retrieval, while full object-to-CCC metric evaluation performs final verification and structural localization.

---

# 16. Figure Naming Principle

The figure names intentionally follow the core CSFR progression:

```text
Grand Map

Metric

Merge

CCC

Runtime
```

This keeps the visual index aligned with the paper series.

---

# 17. Minimal Figure Set Principle

The repository intentionally uses only five core figures.

The goal is:

```text
few figures
high information density
clear conceptual roles
minimal duplication
```

The figure set should act as a visual compression of the entire CSFR argument.

---

# Final Figure Map

```text
Fig-001
CSFR Grand Map
Representation → Metric → Cluster → Fold → Runtime

Fig-002
D_PP vs D_PC
Object↔Object → Object↔CCC

Fig-003
Claw-Dragon Merge
General Merge → Aligned Per-Position Merge

Fig-004
Cluster CCC
Centroid → Structural Possibility Set

Fig-005
Two-Way CCC
DNA Retrieval → D_PC Verification → Localization
```

Together, the five figures visually summarize the complete CSFR runtime:

$$
\boxed{
Metric
\rightarrow
Cluster
\rightarrow
Merge
\rightarrow
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

**CCC Structural Folding Runtime (CSFR)**
*From Metric-Space Objects to Runtime Localization*
