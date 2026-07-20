# GNNV — SAIV 2026 oral presentation (10–12 minutes)

Build (pdfLaTeX only on this machine — no xelatex):

```bash
latexmk -pdf main.tex
```

18 frames + 3 section dividers (34 PDF pages with overlay animations), 11pt base.
Theme: `beamerthemeVanderbilt.sty` (Metropolis + VU gold/black), fixed locally:
frame-title padding via `ht`/`dp` (no clipped ascenders), the gold rule now
bleeds edge to edge (`\hspace*{-\vumargin}`), and section pages no longer print
a `§ N` symbol. The copy in `../poly_enclosures_paper/` still has all three
issues.

Style follows the NeuS 2026 deck: section dividers, definition blocks with
bracketed citations, tiny reference lines at slide bottoms, dark thank-you page.
Gold callout strips carry each slide's takeaway. No em-dashes anywhere in the
body text. Reference lines (`\refline`) are centered and pinned near the bottom
banner on every slide; on RQ3 the CORA citation is folded into the figure caption
so it does not collide with that slide's takeaway strip.

## Structure & timing plan (~11:00)

| # | Slide | Time |
|---|-------|------|
| 1 | Title (no subtitle, SAIV 2026 venue line) | 0:20 |
| 2 | GNN Surrogates Across Application Domains | 0:50 |
| 3 | Graph-Structured Inputs: Node and Edge Feature Matrices | 0:50 |
| 4 | Message Passing: Gather, Aggregate, Update | 1:10 |
| 5 | Graph Convolutional Network (GCN) and Graph Isomorphism Network with Edge Features (GINE) | 0:50 |
| 6 | Verification Gap: No Support for Edge-Aware Architectures | 0:45 |
| 7 | Contributions: GraphStar Sets and the GNNV Module | 1:00 |
| — | *Approach: Lifting Star-Set Reachability from Vectors to Graph-Structured Inputs* | |
| 8 | Background: Star-Set Reachability and Approx-Star in NNV | 0:55 |
| 9 | GraphStar Sets: Star Sets over Node and Edge Feature Matrices (definition + notation) | 0:55 |
| 10 | GNNV Reachability Pipeline (full-size figure) | 0:30 |
| 11 | Pipeline: GraphStar Construction to Specification Check (4 steps) | 0:50 |
| 12 | Soundness and Computational Complexity | 0:45 |
| — | *Experimental Evaluation* | |
| 13 | Experimental Setup: Benchmarks, Models, Specifications | 0:35 |
| 14 | RQ1: Verified Robustness vs. Perturbation Magnitude | 0:45 |
| 15 | RQ2: Joint Node and Edge Perturbations | 0:40 |
| 16 | RQ3: Enclosure Tightness vs. Polynomial Zonotopes | 0:50 |
| — | *Conclusions and Tool Availability* | |
| 17 | Conclusions and Future Work | 0:40 |
| 18 | Tool Availability: GNNV in NNV3 (MATLAB) | 0:40 |
| 19 | Thank You (dark page, single centred stack: contact, paper, QR) | 0:15 |

## Backup slides (after `\appendix`, not numbered in the main count)

1. GraphStar Reachability: How a Layer Transforms the Set (moved out of the main flow)
2. The Verified Models Are Accurate (Test MSE; GINEConv beats GCN/SAGE 25-60x)
3. relax-star: Precision-Speed Trade-off (approx-star vs rho=0.8/0.9)
4. Soundness, Completeness, and Scope (sound-not-complete; feature vs structural perturbations)
5. Why GraphStar Is Tighter Than CORA (and Slower per Graph) (poly-zonotope vs LP mechanism)
6. Why K-hop Subgraph Verification Is Sound (locality + 15-35/118 nodes, with diagram)
7. Where GNNV Sits Among GNN Verifiers (CORA / Hojny-MILP / Liu / Wu comparison table)
8. The Robustness Cliff (IEEE-24 PF) (verified% falls 82.7 -> 0 between eps 0.02 and 0.05)
9. Training and Verification Setup (PyG -> NNV, architectures, seeds, LP/approx-star)

GCN and GINE are introduced in the background (slide 5) so the gap slide and the
contributions can refer to GINE by name. The pipeline's stepped version starts
with **GraphStar construction** before localizing.

## Stage colours (slides 4 and 5 are deliberately aligned)

| Stage | Colour | Macro |
|-------|--------|-------|
| message / edge features | VU gold dark | `\key{}` / `VUgoldDark` |
| aggregate | steel blue `#2E5C8A` | `\aggr{}` |
| combine / update | violet `#6A4C93` | `\comb{}` |

Terminology follows Gilmer et al. (cited): **Message -> Aggregate -> Update**
(Update = the paper's COMBINE). Slide 4 walks these three stages on an irregular
graph (neighbours `u1`-`u3` interconnected, plus `q`, `r`, `w` outside the 1-hop
neighbourhood so it does not read as a feedforward layer); slide 5 shows the same
three stages inside the GCN and GINE layer equations (the "message" stage word
is left black on slide 5; aggregate/combine keep their colours). For
GCN, the equation labels the normalised-adjacency term `aggregate` and the weight
`W` `combine`, and a bullet notes that self-loops (A + I) fold in the node's own
state.

## Slide 8 (GraphStar) figure note

GraphStar generators are **N x d_f matrices**, not vectors. The cartoon draws each
generator as a rows(nodes) x columns(features) grid; per the paper's construction,
a perturbation generator B_i is nonzero only in its perturbed feature column (that
column is shaded). This corrects an earlier version that drew only row dividers,
which read as N x 1 column vectors.

## Domain-slide image credits (Wikimedia Commons)

The application claims cite the GNN papers ([1]-[4] on the slide); the pictures
themselves are openly licensed images, not figures copied out of those papers.
CC0 and Public-Domain images need no attribution; the two CC BY / CC BY-SA
images (traffic map, transmission towers) are legally required to be credited
wherever shown, so their attributions appear directly on the slide's reference
line, not only here.

| Panel | File | Author | License |
|-------|------|--------|---------|
| Molecules | `Caffeine-ball-and-stick.png` | Roger Burger | CC0 |
| Proteins | `Myoglobin.png` | AzaToth | Public domain |
| Traffic | `Manhattan NYC OpenStreetMap 2023-08-21.png` | OpenStreetMap contributors | CC BY 4.0 |
| Power Grids | `Transmission towers at sunset in East Texas.jpg` | Matthew T Rader | CC BY-SA 4.0 |

Slide references: [1] Gilmer et al., ICML 2017. [2] Morris et al., TUDataset
2020. [3] Jiang & Luo, ESWA 2022. [4] Varbella et al., 2024 (PowerGraph).

## Other assets

- `figures/qr_nnv.png` — QR code for `https://github.com/verivital/nnv`,
  generated locally with the Python `qrcode` package.
- `figures/gnn_construction_v5.pdf`, `figures/gnnv_pipeline_v4.pdf`,
  `figures/rq1_*.pdf`, `figures/rq3_*.png` — from the paper source
  (`../gnnv_poster/extracted/figures_v2/`).
- `figures/blackout_*.jpg` — no longer used (the blackout slide was cut).
- `ex_figs/` — reference decks/figures supplied for style, not compiled.
