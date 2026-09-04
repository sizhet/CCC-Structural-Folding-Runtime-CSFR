# CSFR-002 — Metric Representation and Composite Structural Distance

## Heterogeneous Structural Representation for CCC Folding and Runtime Localization

**CCC Structural Folding Runtime (CSFR)**
**CSFR-002**

---

## Abstract

CCC Structural Folding Runtime (CSFR) depends on a metric layer capable of comparing structurally rich objects before clustering, folding, and runtime localization can occur.

Real-world objects are rarely represented by one homogeneous vector.

They may contain:

* named numeric attributes;
* named categorical attributes;
* numeric sequences;
* categorical sequences;
* bucketed values;
* local sequence transitions;
* bigrams and trigrams;
* directional motifs;
* domain-specific structural descriptors.

This paper defines a generic structural metric model for CSFR based on heterogeneous named measures and a composite scoring architecture.

The central representation can be written as:

$$
x =
\{
A^{num},
A^{cat},
S^{num},
S^{cat},
F
\},
$$

where numeric attributes, categorical attributes, numeric sequences, categorical sequences, and derived structural features coexist within one object.

Each measure may use its own local similarity or distance function.

The results are then combined through a weighted composite metric:

$$
D_{PP}(x,y) =
\sum_{r=1}^{R}
w_rD_r(x,y).
$$

For normalized similarity channels, an equivalent structural similarity formulation is:

$$
Sim_{PP}(x,y) =
\sum_{r=1}^{R}
w_rSim_r(x,y).
$$

CSFR further introduces numeric bucketing, multi-resolution n-gram sequence descriptors, forward and reverse sequence channels, position-sensitive weighting, and hierarchical scoring trees.

The result is a flexible **Object-to-Object Structural Distance**, denoted \(D_{PP}\), suitable for:

* nearest-pattern discovery;
* metric-space clustering;
* cluster initialization;
* candidate \(K\) estimation;
* structural organization before CCC folding.

The objective is not to define one universal metric.

It is to define a reusable structural metric architecture in which heterogeneous evidence can coexist without forcing every domain into one feature geometry.

---

# 1. Metric Representation Is the Entrance to CSFR

The CSFR pipeline begins with objects:

$$
X=\{x_1,x_2,\ldots,x_n\}.
$$

Before clustering or folding, the runtime must answer:

> How can two structurally rich objects be compared?

A conventional vector distance assumes that every object is mapped into something like:

$$
x=(x_1,x_2,\ldots,x_d).
$$

That model is useful but often too restrictive.

A real structural object may instead look like:

```text
PE_RATIO            = 23.12
STRENGTH            = STRONG
PRICE_CURVE         = [12.1, 12.5, 12.8, 12.4]
TREND_SEQUENCE      = [UP, UP, FLAT, DOWN]
VOLATILITY_STATE    = HIGH
PATTERN_PHASE       = BREAKOUT
```

These measures do not naturally share one primitive distance function.

Some are numeric.

Some are categorical.

Some are sequential.

Some encode local trajectory structure.

CSFR therefore treats representation as a **heterogeneous structural container** rather than a flat vector.

---

# 2. Generic Structural Container

A useful generic object representation is:

$$
x =
\{
M_1,M_2,\ldots,M_k
\},
$$

where each \(M_i\) is a named measure.

A measure may be one of several broad types.

```text
Named Double
Named String
Named Double Sequence
Named String Sequence
Derived Structural Feature
```

For example:

```text
Object X
├── PE_RATIO              : Double
├── STRENGTH              : String
├── PRICE_CURVE           : DoubleSequence
├── TREND_SEQUENCE        : StringSequence
├── PRICE_BIGRAMS         : DerivedSequenceFeature
└── VOLATILITY_BUCKET     : DerivedCategoricalFeature
```

This representation is closely aligned with a generic `GenericContainerStarmap` style abstraction.

The design principle is:

> **Different structural dimensions should coexist without being prematurely flattened into one representation.**

---

# 3. Four Primitive Measure Types

CSFR can cover a large class of structural objects using four primitive measure categories.

## 3.1 Named Numeric Value

Example:

```text
PE_RATIO = 23.12
```

Formally:

$$
M^{num}=(name,value).
$$

Possible distance functions include:

$$
d(a,b)=|a-b|,
$$

normalized absolute difference,

$$
d(a,b) =
\frac{|a-b|}{R},
$$

or domain-specific transformations.

---

## 3.2 Named Categorical Value

Example:

```text
STRENGTH = STRONG
```

A simple distance may be:

$$
d(a,b)=
\begin{cases}
0,&a=b\\
1,&a\neq b
\end{cases}
$$

but richer semantic distances may also be defined.

For ordered categories:

```text
VERY_WEAK
WEAK
NEUTRAL
STRONG
VERY_STRONG
```

one may define ordinal distance:

$$
d(a,b) =
\frac{|rank(a)-rank(b)|}{R}.
$$

Thus categorical values need not be purely binary.

---

## 3.3 Named Numeric Sequence

Example:

```text
PRICE_CURVE = [12.1, 12.5, 12.8, 12.4]
```

Possible comparisons include:

* aligned point distance;
* normalized Euclidean distance;
* cosine distance;
* correlation distance;
* slope similarity;
* bucketed-state comparison;
* local motif comparison;
* n-gram comparison after discretization.

The metric should reflect the structural semantics of the sequence.

---

## 3.4 Named Categorical Sequence

Example:

```text
TREND_SEQUENCE = [UP, UP, FLAT, DOWN]
```

Possible comparisons include:

* positional match;
* Hamming distance;
* weighted positional distance;
* bigram similarity;
* trigram similarity;
* transition-distribution similarity;
* directional motif comparison.

Categorical sequences are particularly important because they expose trajectory structure without requiring exact numeric equality.

---

# 4. Derived Structural Features

Primitive measures can be transformed into derived measures.

For example:

```text
PRICE_CURVE
    ↓
Slope Sequence
    ↓
[UP, UP, DOWN]
```

or:

```text
TREND_SEQUENCE
    ↓
Bigrams
    ↓
UP→UP
UP→FLAT
FLAT→DOWN
```

Derived features may include:

```text
numeric buckets
categorical buckets
bigrams
trigrams
transition counts
local motifs
slope classes
volatility classes
shape signatures
turning points
relative-position descriptors
domain-specific structural tokens
```

This allows CSFR to compare not only values, but also **relations between values**.

---

# 5. Numeric Bucketing as Structural Folding

Raw numeric distance is often too literal.

Suppose:

```text
PE = 21.8
PE = 22.3
PE = 23.1
```

These values differ numerically.

But a structural policy may classify all of them as:

```text
PE_BUCKET = MEDIUM_HIGH
```

Thus:

$$
21.8,22.3,23.1
\rightarrow
MEDIUM\_HIGH.
$$

Bucketing converts:

$$
Continuous\ Metric\ Space
\rightarrow
Structural\ Symbol\ Space.
$$

This can be interpreted as a local folding operation.

It removes unnecessary precision while preserving policy-relevant structure.

---

# 6. Bucket Design

A bucket function can be written as:

$$
B(x) =
b_j
\quad
\text{if}
\quad
x\in I_j,
$$

where \(I_j\) is a numeric interval.

Example:

```text
PE < 10        → VERY_LOW
10 ≤ PE < 15   → LOW
15 ≤ PE < 25   → MEDIUM
25 ≤ PE < 40   → HIGH
PE ≥ 40        → VERY_HIGH
```

A bucket distance may then use:

$$
d(B(a),B(b)).
$$

This may be binary:

$$
d=
\begin{cases}
0,&same\ bucket\\
1,&different\ bucket
\end{cases}
$$

or ordinal:

$$
d =
\frac{|rank(B(a))-rank(B(b))|}{R}.
$$

Bucket resolution therefore becomes a structural-resolution parameter.

---

# 7. Multi-Resolution Representation

A useful CSFR design may preserve both raw and bucketed versions.

```text
PE_RAW      = 23.12
PE_BUCKET   = MEDIUM
```

The composite metric can then combine:

$$
D_{PE} =
w_rD_{raw}
+
w_bD_{bucket}.
$$

This allows the system to retain:

* fine numeric difference;
* coarse structural category.

The two representations answer different questions.

Raw values answer:

> How numerically close are these objects?

Buckets answer:

> Are these objects in the same structural regime?

---

# 8. Sequence Comparison Beyond Point Matching

A sequence:

$$
S=[x_0,x_1,\ldots,x_n]
$$

contains more information than the set of its individual elements.

Consider:

```text
UP, UP, DOWN, UP
```

Point-level comparison sees:

```text
UP
UP
DOWN
UP
```

But trajectory structure also contains transitions:

```text
UP→UP
UP→DOWN
DOWN→UP
```

and three-step motifs:

```text
UP→UP→DOWN
UP→DOWN→UP
```

Thus sequence comparison should support multiple resolutions.

---

# 9. Bigrams as Local Structural Transitions

For sequence:

$$
S=[x_0,x_1,\ldots,x_n],
$$

the forward bigram set is:

$$
B_f(S) =
\{
(x_0,x_1),
(x_1,x_2),
\ldots,
(x_{n-1},x_n)
\}.
$$

Bigrams encode local transition structure.

For example:

```text
UP, UP, DOWN, FLAT
```

produces:

```text
UP→UP
UP→DOWN
DOWN→FLAT
```

This distinguishes sequences that contain similar states but different trajectories.

---

# 10. Trigrams as Higher-Resolution Local Structure

The forward trigram set is:

$$
T_f(S) =
\{
(x_0,x_1,x_2),
(x_1,x_2,x_3),
\ldots
\}.
$$

Trigrams preserve more local context than bigrams.

For example:

```text
UP→UP→DOWN
UP→DOWN→FLAT
```

contains information not recoverable from isolated values alone.

Thus:

$$
Point <
Bigram <
Trigram
$$

in structural resolution.

However, larger n-grams are not automatically superior.

---

# 11. N-Gram Length as Structural Resolution

As \(n\) increases:

* local structural specificity increases;
* exact matching becomes harder;
* sparsity increases;
* tolerance decreases.

Therefore:

$$
n
$$

should be treated as a policy parameter.

A practical metric may combine multiple resolutions:

$$
D_{seq} =
w_1D_{point}
+
w_2D_{bigram}
+
w_3D_{trigram}.
$$

This allows broad and fine structural evidence to coexist.

---

# 12. Forward and Reverse N-Grams

A sequence naturally has a forward reading direction.

For:

$$
S=[x_0,x_1,x_2,x_3],
$$

forward bigrams are:

```text
x0→x1
x1→x2
x2→x3
```

Reverse bigrams are:

```text
x3→x2
x2→x1
x1→x0
```

Using both channels can reduce representation bias toward one sequence end.

It can also give both leading and trailing local structures explicit opportunities to contribute to similarity.

---

# 13. Preserve Temporal Direction

Forward and reverse descriptors should normally remain separate.

They should not be collapsed into one undirected bag.

For example:

```text
UP → UP → CRASH
```

is structurally different from:

```text
CRASH → UP → UP
```

Therefore define:

$$
D_{ngram} =
w_fD_{forward}
+
w_rD_{reverse}.
$$

Often:

$$
w_f>w_r
$$

when temporal direction is semantically important.

This provides head-tail fairness without destroying causality or temporal orientation.

---

# 14. Sequence Position Weighting

Not all sequence positions need equal importance.

Let:

$$
S=[x_0,x_1,\ldots,x_n].
$$

Define positional weights:

$$
p_0,p_1,\ldots,p_n.
$$

Then aligned sequence distance may be:

$$
D_{pos}(S,T) =
\frac{
\sum_{j=0}^{n}
p_jd(x_j,t_j)
}{
\sum_{j=0}^{n}p_j
}.
$$

This is useful when later positions contain more recent or more decision-relevant information.

For example:

```text
early context      weight = 0.5
formation region   weight = 1.0
recent trigger      weight = 1.8
```

The weighting is explicit and policy-driven.

---

# 15. Dimension Weighting

Different structural dimensions may also have different importance.

Suppose an object contains:

```text
valuation
trend
volume
volatility
market regime
sequence shape
```

Then:

$$
D(x,y) =
w_vD_v
+
w_tD_t
+
w_{vol}D_{vol}
+
w_rD_r
+
w_sD_s.
$$

The weights may be:

* fixed;
* learned;
* domain-defined;
* node-specific;
* regime-specific.

This flexibility is essential because structural importance is rarely uniform.

---

# 16. Three Levels of Weighting

A mature CSFR metric should distinguish at least three different weighting levels.

## 16.1 Dimension Weight

Controls the importance of a measure family.

$$
w_{dimension}
$$

---

## 16.2 Position Weight

Controls the importance of sequence locations.

$$
w_{position}
$$

---

## 16.3 Feature Weight

Controls the importance of derived representations such as bigrams or trigrams.

$$
w_{feature}
$$

A composite contribution may therefore look like:

$$
w_d
\cdot
w_p
\cdot
w_f
\cdot
d.
$$

This makes the metric policy explicit rather than hidden inside preprocessing.

---

# 17. Structural Similarity vs Structural Distance

CSFR may operate in either similarity or distance form.

Similarity:

$$
Sim(x,y)\in[0,1]
$$

with:

$$
1
$$

representing maximal similarity.

Distance:

$$
D(x,y)\in[0,1]
$$

with:

$$
0
$$

representing maximal similarity.

A simple conversion is:

$$
D(x,y) =
1-Sim(x,y).
$$

The framework does not require one orientation.

Consistency is more important than convention.

---

# 18. Cosine Similarity Scoring Tree

When each structural channel produces a normalized similarity score, CSFR can organize those scores as a hierarchical scoring tree.

Example:

```text
Total Similarity
├── Scalar Attributes
│   ├── Numeric Similarity
│   └── Categorical Similarity
│
├── Sequence Similarity
│   ├── Point Similarity
│   ├── Bigram Similarity
│   ├── Trigram Similarity
│   └── Reverse-Sequence Similarity
│
└── Domain Structure
    ├── Regime Similarity
    ├── Shape Similarity
    └── Derived Motif Similarity
```

A node may combine its children using normalized weights.

For node \(N\):

$$
Score(N) =
\frac{
\sum_iw_iScore(C_i)
}{
\sum_iw_i
}.
$$

This produces a **composite structural scoring tree**.

---

# 19. Why a Scoring Tree Is Useful

A flat weighted sum can compute the same final score.

But a tree provides additional engineering value.

It exposes:

* decomposition;
* auditability;
* policy boundaries;
* reusable submetrics;
* node-specific tuning;
* explainable score contributions.

For example:

```text
Total Similarity = 0.82

Scalar Attributes = 0.91
Sequence Structure = 0.76
Regime Features = 0.84
```

The system can then explain why two objects are considered similar.

---

# 20. Cosine Similarity for Feature Bags

Some derived structural representations can naturally be expressed as sparse count vectors.

For example, bigram frequencies:

```text
UP→UP       3
UP→DOWN     1
DOWN→UP     2
FLAT→UP     0
```

Let two bigram vectors be:

$$
u=(u_1,\ldots,u_m)
$$

and

$$
v=(v_1,\ldots,v_m).
$$

Cosine similarity is:

$$
Sim_{cos}(u,v) =
\frac{
u\cdot v
}{
\|u\|\|v\|
}.
$$

This is useful when pattern magnitude is less important than structural composition.

---

# 21. N-Gram Frequency Representation

A sequence can be converted into a sparse n-gram vector.

For bigrams:

$$
V_2(S) =
[
count(g_1),
count(g_2),
\ldots
].
$$

For trigrams:

$$
V_3(S) =
[
count(h_1),
count(h_2),
\ldots
].
$$

Then:

$$
Sim_{2}(S,T) =
Cosine(V_2(S),V_2(T))
$$

and:

$$
Sim_{3}(S,T) =
Cosine(V_3(S),V_3(T)).
$$

These channels may be combined with positional comparison.

---

# 22. Exact Position and Motif Similarity Are Complementary

Two sequences can have similar motifs but different positions.

Example:

```text
A = [UP, UP, DOWN, FLAT]
B = [FLAT, UP, UP, DOWN]
```

Their local transition motifs may overlap strongly.

But positional structure differs.

Therefore sequence comparison may use both:

$$
D_{sequence} =
w_pD_{position}
+
w_mD_{motif}.
$$

The two channels answer different questions:

> Are the same states occurring at the same positions?

and:

> Are similar local structural transitions present anywhere in the sequence?

---

# 23. Relative Rather Than Absolute Numeric Sequences

Raw numeric sequences can be dominated by scale.

For example:

```text
[10, 11, 12, 13]
```

and:

```text
[100, 110, 120, 130]
```

have different absolute values but similar shape.

Possible derived representations include:

```text
percentage change
normalized value
z-score
slope sequence
direction state
relative-to-baseline value
rank sequence
```

Thus:

$$
RawSequence
\rightarrow
StructuralSequence.
$$

This is often critical for meaningful metric comparison.

---

# 24. Multiple Representations of the Same Sequence

One sequence may intentionally generate several parallel representations.

```text
Raw Sequence
├── normalized numeric sequence
├── direction sequence
├── bucket sequence
├── bigram vector
├── trigram vector
└── shape descriptor
```

The metric can then combine all channels.

This is not redundant if each representation captures a different structural scale.

---

# 25. Composite Structural Distance

Let object \(x\) contain \(R\) measure groups.

Define local distances:

$$
D_1(x,y),D_2(x,y),\ldots,D_R(x,y).
$$

Then:

$$
D_{PP}(x,y) =
\frac{
\sum_{r=1}^{R}
w_rD_r(x,y)
}{
\sum_{r=1}^{R}w_r
}.
$$

If weights are normalized:

$$
\sum_rw_r=1,
$$

then:

$$
D_{PP}(x,y) =
\sum_rw_rD_r(x,y).
$$

This is the primary object-to-object metric used before CCC folding.

---

# 26. Composite Structural Similarity

An equivalent similarity formulation is:

$$
Sim_{PP}(x,y) =
\sum_{r=1}^{R}
w_rSim_r(x,y).
$$

Then:

$$
D_{PP}(x,y) =
1-Sim_{PP}(x,y)
$$

when all components are normalized to \([0,1]\).

This is particularly convenient when many channels use cosine similarity.

---

# 27. A Canonical Example

Suppose a structural pattern contains:

```text
PE_RATIO
STRENGTH
PRICE_CURVE
TREND_SEQUENCE
```

The total similarity may be:

$$
Sim_{PP} =
0.15Sim_{PE}
+
0.10Sim_{Strength}
+
0.30Sim_{Curve}
+
0.45Sim_{Trend}.
$$

Trend similarity may itself be:

$$
Sim_{Trend} =
0.30Sim_{point}
+
0.35Sim_{bigram}
+
0.25Sim_{trigram}
+
0.10Sim_{reverse}.
$$

Thus the metric is hierarchical.

---

# 28. Hierarchical Metric Example

```text
Pattern Similarity
│
├── Fundamental Features           0.25
│   ├── PE Ratio                   0.10
│   └── Strength                   0.15
│
├── Numeric Sequence Structure     0.30
│   ├── normalized point curve
│   └── shape similarity
│
└── Categorical Trajectory         0.45
    ├── aligned states
    ├── forward bigrams
    ├── forward trigrams
    └── reverse descriptors
```

This form is easy to inspect, tune, and audit.

---

# 29. Missing Measures

Real objects may not contain every measure.

A metric must define missing-value policy.

Possible policies include:

```text
ignore missing dimension
renormalize remaining weights
assign uncertainty penalty
assign maximum distance
use fallback representation
reject comparison if critical feature missing
```

A common policy is:

$$
D(x,y) =
\frac{
\sum_{r\in A}w_rD_r
}{
\sum_{r\in A}w_r
},
$$

where \(A\) is the set of available comparable measures.

This prevents absent noncritical dimensions from automatically dominating the result.

---

# 30. Measure Confidence

A measure may also have confidence:

$$
c_r\in[0,1].
$$

Then effective weight becomes:

$$
w'_r
=
w_rc_r.
$$

The composite distance becomes:

$$
D(x,y) =
\frac{
\sum_rw_rc_rD_r
}{
\sum_rw_rc_r
}.
$$

This allows uncertain measurements to contribute less strongly.

---

# 31. Policy-Driven Metric Configuration

CSFR does not assume that metric weights are universal.

A metric policy may specify:

```text
measure inclusion
measure exclusion
bucket boundaries
dimension weights
position weights
n-gram length
forward/reverse weights
missing-value handling
normalization
confidence handling
distance aggregation
```

This turns the metric into an explicit runtime artifact.

---

# 32. Node-Specific Metrics

A particularly important extension is that different dispatch nodes may use different metric policies.

At a high-level node:

```text
market regime
volatility
broad trend
```

may dominate.

At a deeper node:

```text
local shape
recent transitions
fine-grained sequence motifs
```

may dominate.

Thus:

$$
D^{(node)}_{PP}
$$

may vary across the tree.

This naturally supports Per-Node Intelligence.

---

# 33. Global Metric vs Local Metric

A global metric is useful for:

```text
initial clustering
coarse organization
global nearest-pair discovery
```

A local metric may be better for:

```text
fine dispatch
leaf separation
specialized structural discrimination
```

Therefore:

$$
GlobalMetric
\neq
LocalMetric
$$

in general.

CSFR should allow both.

---

# 34. Metric Space and K Discovery

The object-to-object distance \(D_{PP}\) supports cluster discovery.

One possible process is:

```text
Compute / sample pairwise distances
        ↓
Find nearest object pairs
        ↓
Merge nearest candidates
        ↓
Observe merge-distance progression
        ↓
Estimate candidate K
        ↓
Run metric-space K-Means or related clustering
```

The specific method is not mandatory.

The structural metric provides the common substrate.

---

# 35. Nearest-Pair Merge as K Evidence

Suppose pairwise merge distances are:

```text
0.05
0.07
0.08
0.10
0.11
0.38
0.42
```

A large jump may indicate a structural boundary.

This can provide evidence for a candidate cluster count.

Thus:

$$
NearestPairMerge
\rightarrow
Candidate\ K.
$$

The final \(K\) may later be validated using runtime localization quality.

---

# 36. Runtime-Oriented Metric Design

The best metric is not necessarily the one that produces the visually cleanest clusters.

CSFR ultimately cares about:

$$
Metric
\rightarrow
Cluster
\rightarrow
CCC
\rightarrow
Dispatch.
$$

Therefore metric quality may be judged by downstream criteria such as:

```text
cluster stability
CCC stability
dispatch accuracy
localization consistency
leaf purity
unknown-pattern rejection
runtime cost
```

This is an important shift.

---

# 37. Structural Resolution Is a Policy Surface

CSFR exposes several resolution controls:

```text
numeric bucket width
sequence normalization
n-gram length
position weighting
feature inclusion
motif granularity
cluster K
CCC filtering threshold
```

These parameters determine how finely the runtime distinguishes structures.

Thus structural resolution is not one scalar.

It is a policy surface.

---

# 38. Avoiding Overfitting the Metric

A highly detailed metric can become too specific.

For example:

* long n-grams may rarely match;
* very fine numeric buckets may fragment clusters;
* excessive dimensions may dilute strong signals;
* large position weights may overemphasize local noise.

Therefore metric design should balance:

$$
Discrimination
\leftrightarrow
Generalization.
$$

This is analogous to choosing structural granularity.

---

# 39. Avoiding Underfitting the Metric

The opposite failure is excessive compression.

If:

```text
UP, UP, DOWN, UP
```

and:

```text
UP, DOWN, UP, UP
```

are treated only as bags of states, important trajectory information disappears.

Thus:

$$
Too\ Coarse
\rightarrow
Structural\ Collision.
$$

N-grams and positional channels help restore discrimination.

---

# 40. Metric Decomposition for Audit

A composite metric should expose its component contributions.

Example:

```text
Total Distance = 0.214

PE Ratio              0.08
Strength              0.00
Price Curve           0.31
Point Trend           0.20
Bigram Trend          0.18
Trigram Trend         0.27
Reverse Trend         0.23
```

This enables:

* debugging;
* model inspection;
* policy tuning;
* structural explanation.

It also makes CCC dispatch more auditable later.

---

# 41. Metric Signature

A useful implementation concept is a **Metric Signature**.

Example:

```text
MetricSignature
├── dimensions
├── normalizers
├── bucket policies
├── sequence transforms
├── n-gram settings
├── weights
└── aggregation policy
```

Then every cluster and CCC can record which metric policy produced it.

This improves reproducibility.

---

# 42. Metric Versioning

Because metric policy may evolve, the runtime should support versioning.

Example:

```text
CSFR-METRIC-v1.0
CSFR-METRIC-v1.1
CSFR-METRIC-v2.0
```

A cluster generated under one metric policy should not silently be compared using another incompatible policy.

Thus metric version becomes part of structural provenance.

---

# 43. Metric Compatibility

Two CCC structures are metrically compatible only if the required representation assumptions are compatible.

Potential compatibility dimensions include:

```text
feature schema
bucket schema
sequence length
normalization policy
n-gram vocabulary
weight policy
distance version
```

This matters for future \(D_{CC}\) comparisons.

---

# 44. Generic Pseudocode

A generic object-to-object metric can be expressed as:

```java
double calcPatternDistance(
        StructuralPattern a,
        StructuralPattern b,
        MetricPolicy policy) {

    double weightedDistance = 0.0;
    double totalWeight = 0.0;

    for (MetricDimension dimension : policy.getDimensions()) {

        if (!dimension.isComparable(a, b)) {
            continue;
        }

        double localDistance =
                dimension.calcDistance(a, b);

        double weight =
                dimension.getWeight();

        weightedDistance +=
                weight * localDistance;

        totalWeight += weight;
    }

    if (totalWeight == 0.0) {
        return policy.getNoComparableFeatureDistance();
    }

    return weightedDistance / totalWeight;
}
```

The important point is not the exact class structure.

It is the separation between:

```text
representation
local metric
weight
aggregation
policy
```

---

# 45. Sequence Metric Pseudocode

```java
double calcSequenceDistance(
        List<String> a,
        List<String> b,
        SequenceMetricPolicy policy) {

    double pointDistance =
            calcPointDistance(a, b, policy);

    double forwardBigramDistance =
            calcBigramDistance(a, b, false);

    double forwardTrigramDistance =
            calcTrigramDistance(a, b, false);

    double reverseBigramDistance =
            calcBigramDistance(a, b, true);

    return
            policy.pointWeight() * pointDistance
          + policy.bigramWeight() * forwardBigramDistance
          + policy.trigramWeight() * forwardTrigramDistance
          + policy.reverseWeight() * reverseBigramDistance;
}
```

A production implementation may normalize weights explicitly.

---

# 46. Structural Metric Tree Pseudocode

```java
MetricNode root = metricNode("TOTAL")
        .child(
            metricNode("SCALAR")
                .child(doubleMetric("PE_RATIO"))
                .child(stringMetric("STRENGTH"))
        )
        .child(
            metricNode("SEQUENCE")
                .child(pointSequenceMetric("TREND"))
                .child(bigramMetric("TREND"))
                .child(trigramMetric("TREND"))
                .child(reverseBigramMetric("TREND"))
        );
```

This makes the scoring structure explicit.

---

# 47. Canonical D_PP Definition

For CSFR, the primary pre-folding metric is:

$$
\boxed{
D_{PP} :
Pattern/Object
\leftrightarrow
Pattern/Object
}
$$

A canonical hierarchical form is:

$$
D_{PP} =
\sum_d
w_d
D_d,
$$

where each dimension may itself be decomposed:

$$
D_d =
\sum_f
w_{d,f}
D_{d,f}.
$$

For sequence dimensions:

$$
D_{seq} =
w_pD_{point}
+
w_bD_{bigram}
+
w_tD_{trigram}
+
w_rD_{reverse}.
$$

This gives CSFR a flexible composite structural metric.

---

# 48. Relationship to Cluster CCC Construction

The object metric \(D_{PP}\) is used before CCC construction:

$$
Objects
\xrightarrow{D_{PP}}
Metric\ Space
\rightarrow
Clusters.
$$

Then cluster members are folded:

$$
Cluster
\rightarrow
CCC.
$$

A separate metric \(D_{PC}\) is then required:

$$
Object
\leftrightarrow
CCC.
$$

Thus:

$$
D_{PP}
\neq
D_{PC}
$$

even if they share underlying measure primitives.

This distinction is critical to CSFR.

---

# 49. Reuse of Metric Primitives

Although \(D_{PP}\) and \(D_{PC}\) differ, many primitives can be reused.

For example:

```text
numeric bucket distance
categorical distance
sequence point distance
bigram similarity
trigram similarity
position weighting
dimension weighting
```

The difference is the target representation.

For \(D_{PP}\):

```text
value ↔ value
sequence ↔ sequence
```

For \(D_{PC}\):

```text
value ↔ possibility set
sequence ↔ sequence of possibility sets
```

This reuse is one reason CSFR can maintain a coherent structural language across offline and online phases.

---

# 50. Core Design Principle

The central design principle of CSFR metric representation is:

> **Do not force structurally different evidence into one primitive geometry before you understand what each dimension means.**

Instead:

```text
preserve structural type
        ↓
define local metric
        ↓
derive useful structural features
        ↓
weight explicitly
        ↓
combine through a metric tree
```

This creates a metric architecture rather than a single formula.

---

# 51. Core Claims

### Claim 1 — Structural objects should support heterogeneous named measures.

Numeric, categorical, sequential, and derived structures should coexist.

---

### Claim 2 — Numeric bucketing is a useful structural-resolution mechanism.

It converts continuous values into policy-relevant structural states.

---

### Claim 3 — Sequence similarity should not be limited to pointwise comparison.

Bigrams, trigrams, and local motifs expose trajectory structure.

---

### Claim 4 — Forward and reverse descriptors should remain distinct when direction matters.

Bidirectional descriptors can improve coverage without erasing temporal semantics.

---

### Claim 5 — Structural distance should support explicit dimension, position, and feature weighting.

Metric policy should be inspectable.

---

### Claim 6 — Composite metrics should be decomposable and auditable.

A scoring tree is preferable to an opaque monolithic score.

---

### Claim 7 — The primary pre-folding metric is \(D_{PP}\).

It supports metric organization and clustering before Cluster CCC construction.

---

### Claim 8 — Metric design should ultimately be evaluated by runtime structural quality.

Good clustering geometry is useful, but stable downstream localization is the stronger systems criterion.

---

# 52. What This Paper Does Not Define

This paper does not yet define:

* Cluster CCC construction;
* Claw-Dragon Merge;
* policy filtering of structural possibility sets;
* Object-to-CCC distance \(D_{PC}\);
* CCC-to-CCC distance \(D_{CC}\);
* runtime dispatch;
* Two-Way CCC indexing.

These are developed in later CSFR papers.

---

# 53. Canonical Metric Pipeline

```text
Raw Object
   │
   ▼
Named Structural Measures
   │
   ├── Numeric
   ├── Categorical
   ├── Numeric Sequence
   └── Categorical Sequence
   │
   ▼
Derived Structural Features
   │
   ├── Buckets
   ├── Bigrams
   ├── Trigrams
   ├── Reverse N-Grams
   └── Domain Motifs
   │
   ▼
Local Metric Functions
   │
   ▼
Dimension / Position / Feature Weights
   │
   ▼
Composite Metric Tree
   │
   ▼
D_PP
   │
   ▼
Metric-Space Clustering
   │
   ▼
Cluster Candidates
```

This is the metric entrance to CSFR.

---

# 54. Closing Perspective

Structural folding begins before the cluster merge itself.

It begins when raw observations are transformed into meaningful metric representations.

A useful structural metric does not merely ask:

> How numerically close are two objects?

It asks:

> Which structural dimensions are shared, which differ, at what resolution, and with what importance?

CSFR therefore treats metric representation as a layered process:

$$
Raw\ Values
\rightarrow
Structural\ Measures
\rightarrow
Derived\ Motifs
\rightarrow
Composite\ Distance.
$$

The resulting object-to-object metric:

$$
\boxed{
D_{PP}
}
$$

provides the foundation for metric-space organization.

But the purpose of that organization is not clustering for its own sake.

It is to prepare the next transformation:

$$
\boxed{
Metric\ Cluster
\rightarrow
Structural\ Merge
\rightarrow
Cluster\ CCC
}
$$

That transition is the subject of the next paper.

---

## Next

**CSFR-003 — Sequence Claw-Dragon Merge and Cluster CCC**

The next paper develops the structural folding step itself, including the general Claw-Dragon problem, the equal-length aligned-sequence special case, per-position structural distributions, policy-driven filtering, and the formal distinction between a centroid and a Cluster CCC.

---

**CCC Structural Folding Runtime (CSFR)**
*From Metric-Space Objects to Runtime Localization*
