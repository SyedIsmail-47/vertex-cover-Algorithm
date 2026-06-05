# 🔵 VertexCoverLab — Interactive Vertex Cover Problem Visualizer

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![HTML](https://img.shields.io/badge/Built%20With-HTML%2FTailwind%2FJS-indigo.svg)]()
[![No Backend](https://img.shields.io/badge/Backend-None-brightgreen.svg)]()
[![Algorithms](https://img.shields.io/badge/Algorithms-4-purple.svg)]()
[![NP-Complete](https://img.shields.io/badge/Problem-NP--Complete-red.svg)]()

> A zero-backend, single-file interactive sandbox for learning the **Vertex Cover Problem** — one of the classic NP-complete problems in computer science. Build your own graphs, then watch 4 different algorithms solve it step by step on a live animated canvas.

---

## 📌 Table of Contents

- [What Is This?](#-what-is-this)
- [What Is the Vertex Cover Problem?](#-what-is-the-vertex-cover-problem)
- [Live Demo](#-live-demo)
- [Algorithms Covered](#-algorithms-covered)
- [Features](#-features)
- [How to Use](#-how-to-use)
- [Algorithm Deep Dive](#-algorithm-deep-dive)
- [Complexity Summary](#-complexity-summary)
- [Project Structure](#-project-structure)
- [Learning Outcomes](#-learning-outcomes)
- [Contributing](#-contributing)
- [License](#-license)

---

## 🧠 What Is This?

**VertexCoverLab** is an interactive, browser-based teaching tool that visualizes 4 different approaches to solving the Vertex Cover Problem — from exhaustive brute force to a provably bounded approximation — on a live canvas graph you build yourself.

Every algorithm runs in a **manual step-by-step mode** (click *Next Step* once per decision) or an **auto-complete mode**, so you can trace exactly what each algorithm is doing at every moment.

**Built for:**
- 🎓 Students studying NP-completeness, graph theory, and algorithm design
- 👨‍🏫 Educators presenting combinatorial optimization in lectures
- 🧑‍💻 Developers who prefer animated visual learning over pseudocode on paper
- 📚 Anyone preparing for technical interviews involving graph algorithms

---

## ❓ What Is the Vertex Cover Problem?

Given an undirected graph `G = (V, E)`, a **Vertex Cover** is a subset `S ⊆ V` such that for every edge `(u, v) ∈ E`, at least one of `u` or `v` is in `S`.

The **Minimum Vertex Cover** problem asks: *find the smallest such subset S.*

```
Example graph:       A — B
                     |   |
                     C — D

Minimum vertex cover: {B, C}
Both endpoints of every edge have at least one member in {B, C}.
```

This problem is **NP-complete** — no polynomial-time exact algorithm is known, and it appears on Karp's original list of 21 NP-complete problems (1972). It has direct applications in:

- 🔐 Network security (minimum sensor placement)
- 🧬 Bioinformatics (protein interaction networks)
- 📡 Wireless network design
- 🛡️ Intrusion detection systems

---

## 🌐 Live Demo

> **Just open `index.html` in any modern browser. No install, no server, no npm.**

```bash
git clone https://github.com/YOUR-USERNAME/vertex-cover-lab.git
cd vertex-cover-lab
open index.html        # macOS
start index.html       # Windows
xdg-open index.html    # Linux
```

Or simply drag and drop `index.html` into your browser tab.

---

## ⚙️ Algorithms Covered

| # | Algorithm | Class | Time Complexity | Space | Optimal? |
|---|-----------|-------|----------------|-------|----------|
| 1 | **Brute Force** | Exact / Exhaustive | O(2ᵛ · E) | O(V) | ✓ |
| 2 | **Backtracking** | Exact / Pruning DFS | O(2ᵛ) worst | O(V) | ✓ |
| 3 | **Greedy Heuristic** | Heuristic | O(V·E) or O(E log V) | O(V+E) | ✗ |
| 4 | **2-Approximation** | PTAS / Polynomial | O(V + E) | O(V) | ✗ (≤ 2× opt) |

---

## ✨ Features

### 🏗️ Graph Builder
- **Add vertices** — type any 1–2 character label and click Add
- **Add edges** — specify two node labels to link them
- **Drop vertices** — remove a node and all its incident edges
- **Generate Demo Graph** — instantly load a randomized test graph with one click
- All graph changes reflect immediately on the canvas

### 🎬 Animation Controls
- **⏭ Next Step** — advance exactly one algorithm decision at a time, manually
- **⏩ Auto Complete** — run remaining steps automatically at 400ms intervals
- **↺ Reset** — restore graph to its initial state and clear the cover selection
- Tab switching automatically resets and re-initializes for the new algorithm

### 📊 Live Canvas Visualization
- Nodes highlighted as they are added to the vertex cover
- Edges color-coded by state: normal → active → covered
- Overlay message panel explains every single decision as it happens
- Canvas resizes responsively with the browser window

### 📐 Metrics Dashboard
- **Cover Size** — live count of vertices in the current cover
- **Steps Executed** — operation counter incrementing per step
- **Optimality Status** — labeled badge showing algorithm phase and result quality

### 📋 Algorithm Info Panel (right sidebar)
- Algorithm name, class badge (NP-Complete / Heuristic / PTAS)
- Plain-English description of the strategy
- Time and space complexity display
- Numbered step-by-step execution strategy breakdown — updates when you switch tabs

---

## 🚀 How to Use

### Quick Start

1. Open `index.html` in your browser
2. Click **Generate Demo Graph** to load a sample graph instantly
3. Select an algorithm tab (Brute Force / Backtracking / Greedy / Approximation)
4. Click **⏭ Next Step** repeatedly to trace the algorithm one decision at a time
5. Or click **⏩ Auto Complete** to watch it finish automatically
6. Read the overlay message on the canvas to understand each decision
7. Click **↺ Reset** and switch tabs to compare algorithms on the same graph

### Building a Custom Graph

1. Type a node label (e.g. `A`) in the Vertices input → click **Add**
2. Repeat for all nodes you want
3. Type two labels in the Edges inputs (e.g. `A` and `B`) → click **Link**
4. Repeat for all edges
5. Run any algorithm on your custom graph

### Comparing Algorithms

1. Build or generate a graph
2. Run one algorithm to completion, note the cover size
3. Click **↺ Reset**, switch tab, run the next algorithm
4. Compare cover sizes — exact algorithms (Brute Force, Backtracking) always match; Greedy and 2-Approx may produce larger covers

---

## 🔬 Algorithm Deep Dive

### 1. Brute Force — Power Set Enumeration

```
For mask = 0 to 2^V - 1:
    S = set of nodes where bit i is set in mask
    If every edge (u,v) has u ∈ S or v ∈ S:
        candidate valid cover
Return smallest valid cover found
```

**Idea:** Enumerate every possible subset of vertices using bitmasks. For each subset, check whether it covers all edges. Keep the smallest valid one.

**Visualization:** Each *Next Step* advances the bitmask by 1, showing which subset is being tested and which edges are covered by it.

**Why it matters:** The baseline. Shows exactly why NP-completeness is a problem — 2^V subsets grow faster than any polynomial.

---

### 2. Backtracking — Pruning DFS

```
function bt(edgeIndex, currentCover):
    if edgeIndex == |E|: return currentCover
    edge = E[edgeIndex]
    if edge already covered: return bt(edgeIndex+1, currentCover)

    // Branch 1: include u
    include u, recurse
    // Branch 2: include v
    include v, recurse

    Return the smaller of the two results
```

**Idea:** Build a decision tree where each uncovered edge forces a binary choice — include `u` or include `v`. Prune subtrees whose partial cover size already exceeds the known best.

**Visualization:** Each step replays one node in the pre-computed DFS decision stack, showing which branch is being explored and why.

**Key improvement over brute force:** Pruning can eliminate huge portions of the search tree early, dramatically reducing the actual number of steps in practice.

---

### 3. Greedy Heuristic — Maximum Degree Selection

```
While uncovered edges remain:
    v = vertex with highest degree among remaining edges
    Add v to cover
    Remove all edges incident to v
```

**Idea:** At every step, greedily pick the vertex that covers the most remaining edges. Intuitively sensible, computationally cheap, but not guaranteed to be optimal.

**Visualization:** Each step computes current degrees, highlights the selected node, and removes its incident edges from the active set.

**Limitation:** Can produce covers larger than optimal. Example: a star graph where the greedy picks spokes before the center.

---

### 4. 2-Approximation — Arbitrary Edge Matching

```
While uncovered edges remain:
    Pick any arbitrary edge (u, v)
    Add BOTH u and v to the cover
    Remove all edges incident to u or v
```

**Idea:** Pick any uncovered edge and include *both* its endpoints. This is provably at most **2× the optimal** cover size. The matching selected forms a maximal matching; since every edge in the matching needs at least one endpoint covered, and we include two, we overshoot by at most a factor of 2.

**Visualization:** Each step highlights the chosen edge, adds both endpoints to the cover (colored together), and removes all edges they touch.

**Why it's powerful:** O(V+E) runtime — linear! — with a mathematical guarantee. This is why approximation algorithms matter: when exact algorithms are infeasible, bounded approximations are the practical solution.

---

## 📊 Complexity Summary

```
V = number of vertices, E = number of edges

Algorithm          Time            Space     Optimal   Guarantee
─────────────────────────────────────────────────────────────────
Brute Force        O(2^V · E)      O(V)      Yes       Exact minimum
Backtracking       O(2^V) worst    O(V)      Yes       Exact minimum (pruned)
Greedy             O(V·E)          O(V+E)    No        No bound guaranteed
2-Approximation    O(V + E)        O(V)      No        ≤ 2 × optimal (proven)
```

### Why Approximation Matters

The 2-approximation guarantee comes from a simple argument:

- Let `M` be the matching selected (edges picked)
- Every edge in `M` is vertex-disjoint (no shared endpoints)
- Any valid cover must include at least one endpoint per edge in `M` → `|OPT| ≥ |M|`
- Our cover includes both endpoints per edge → `|our cover| = 2|M| ≤ 2·|OPT|`

This makes the 2-approximation one of the cleanest algorithm proofs in all of combinatorics.

---

## 🗂️ Project Structure

```
vertex-cover-lab/
│
├── index.html      # Complete application — self-contained single file
└── README.md       # This file
```

The entire application is one HTML file using:
- **Tailwind CSS** (via CDN) for layout and styling
- **Font Awesome** (via CDN) for icons
- **Vanilla JavaScript** — no frameworks, no build tools
- **HTML5 Canvas** for graph rendering

---

## 🎓 Learning Outcomes

After working through this visualizer you should be able to:

- Define the Vertex Cover Problem and explain why it is NP-complete
- Trace through a brute force bitmask enumeration by hand
- Explain what pruning is and why backtracking is faster than brute force in practice
- Describe the greedy maximum-degree strategy and give a counterexample where it fails
- Prove the 2× optimality bound for the approximation algorithm
- Compare trade-offs between exact algorithms, heuristics, and approximations
- Read and reason about O(2^V), O(V·E), and O(V+E) complexities in context

---

## 🤝 Contributing

Ideas for extending this project:

- [ ] Add a Linear Programming relaxation solver
- [ ] Add Kernelization (FPT algorithm for parameterized complexity)
- [ ] Show the decision tree visually during backtracking
- [ ] Add export of the found cover as JSON
- [ ] Add side-by-side dual-algorithm view on the same graph
- [ ] Weighted vertex cover variant
- [ ] Show the complement: Independent Set visualization

To contribute:

```bash
# Fork the repo, then:
git checkout -b feature/your-feature-name
# Edit index.html
git commit -m "Add: description of your change"
git push origin feature/your-feature-name
# Open a Pull Request
```

No build pipeline — just edit the HTML file and test in your browser.

---

## 📄 License

MIT License — free to use, share, modify for educational and commercial use. See [LICENSE](LICENSE) for full text.

---

## 🙏 Acknowledgements

- **Richard Karp (1972)** — for establishing Vertex Cover as one of the original 21 NP-complete problems
- **Dinur & Safra (2005)** — for hardness of approximation results showing 1.36× is the limit
- The graph theory and algorithms education community

---

<div align="center">

**Built to make NP-completeness tangible — one vertex at a time.**

⭐ Star this repo if it helped you understand something that felt hard before

</div>
