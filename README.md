# CS-886---Learning-Theory-for-Modern-AI
This is the repository for maintaining notes and material for CS 886 (Fall 2026)  
Course Website: https://watcl-lab.github.io/cs886-learning-theory/   
List of content across 12 weeks:   

- Week 1: Biases and Optimization of Self Attention
- Week 2: Trainability, Expressivity, and Approximation
- Week 3: Formal Languages, Logic, and Circuit Complexity
- Week 4: Computational Limits and Programmable Transformers
- Week 5: Length Generalization and Infinite-Limit Theory
- Week 6: Memory and Bayesian Theories of In-Context Learning
- Week 7: In-Context Learning as Optimization 
- Week 8: Generalization and Algorithm Selection in In-Context Learning
- Week 9: Optimal In-Context Learning and Chain-of-Thought Theory
- Week 10: Reasoning Generalization and Misspecified Next-Token Prediction
- Week 11: Parameter-Efficient Adaptation and Preference Learning
- Week 12: RLHF Exploration, Hallucination, and Watermarking


# PreReq 1: Linear algebra & matrix analysis

Scope. Spectral theory, singular values, matrix/operator norms, rank and low-rank structure, positive-definiteness, eigenvalue perturbation (Weyl, Davis–Kahan). This is the language of rank collapse, Lipschitz bounds, and linear-attention analysis. 

Weeks: 1 (rank collapse, Lipschitz constant), 5 (positional expressivity, kernels), 7 (linear self-attention optimum), and background everywhere. Books:

Horn & Johnson, Matrix Analysis — the reference; you'll use the perturbation and norm chapters.
Trefethen & Bau, Numerical Linear Algebra — best for spectral/SVD intuition, fast read.
Bhatia, Matrix Analysis — if you want the perturbation-theory depth behind Davis–Kahan. Practice:
Prove the operator-norm submultiplicativity bounds and derive a Lipschitz constant for a composition of affine + softmax maps (this is exactly the Kim et al. Week 1 setup — reproduce their "dot-product attention is not globally Lipschitz" argument).
Reproduce the doubly-exponential rank-collapse bound for depth-
L
L pure attention (Dong et al., Week 1) on a 2×2 toy and confirm the residual branch breaks it.
Pillar B — High-dimensional probability & concentration

Scope. Sub-Gaussian / sub-exponential tails, Hoeffding / Bernstein / Azuma–Hoeffding, matrix Bernstein, ε-nets and covering numbers, Gaussian and Rademacher complexity as random quantities. This is the connective tissue: almost every generalization bound and training-dynamics proof in the course runs through a concentration step. Weeks: underpins 1, 5, 7, 8, 9, 10, 12 — effectively all of them. Books:

Vershynin, High-Dimensional Probability (free PDF) — do this first. Chapters 1–4 (sub-Gaussian, sub-exponential, random vectors, matrix concentration) and Chapter 8 (ε-nets, covering).
Wainwright, High-Dimensional Statistics — Chapters 2–5 for the statistics-flavored versions you'll meet in the ICL-generalization weeks.
Boucheron, Lugosi & Massart, Concentration Inequalities — reference for the sharp/entropy-method versions. Practice:
The Vershynin exercises on sub-Gaussian tails, covering numbers of the sphere, and matrix Bernstein.
Derive a uniform-convergence bound for a linear class via an ε-net argument end to end — this is the template Week 8 (Li et al., Wies et al.) reuses.
Pillar C — Convex optimization & optimization dynamics / implicit bias

Scope. GD/SGD convergence (smooth, strongly convex, PL), gradient flow, margin maximization, implicit bias of GD on separable data, mirror descent. The recurring move in this course is "trained transformer converges in direction to a max-margin / specific-algorithm solution." Weeks: 1 (implicit bias, max-margin token selection), 2 (LayerNorm/init gradient behavior), 6–7 (training forms memories; forward pass implements an update; convergence of linear-attention training), 9 (in-context convergence). Books:

Boyd & Vandenberghe, Convex Optimization (free) — foundations, if rusty. Skim; you need duality and first-order conditions.
Bubeck, Convex Optimization: Algorithms and Complexity (free monograph) — tight, proof-first treatment of GD rates.
Telgarsky, Deep Learning Theory lecture notes (free, U. Illinois) — the single best source for implicit bias, margin maximization, and NTK in one place; maps most directly onto this course. Practice:
Reproduce Soudry et al. (Week 1, paper 3) yourself: prove GD on logistic loss over linearly separable data converges in direction to the hard-margin SVM solution, with the 
log⁡t
logt rate. This is the template the attention papers (Tarzanagh, Week 1) rebuild — do it before the term and Weeks 1/7 become easy.
Prove GD converges linearly under smoothness + strong convexity; then under PL only.
Gradient flow on a quadratic: solve it in closed form, connect to preconditioning (sets up von Oswald / Ahn "transformers do preconditioned GD," Week 7).
Pillar D — Statistical learning theory

Scope. PAC learning, ERM, VC dimension, Rademacher complexity, uniform convergence, algorithmic stability, minimax and nonparametric rates, statistical-query (SQ) lower bounds. This is the biggest single gap for a systems background and the backbone of the ICL-generalization block. Weeks: 8 (stability, PAC learnability of ICL, algorithm selection), 9 (minimax-optimal nonparametric ICL; VC-based CoT learning), 10 (SQ lower bounds for compositional learning; comp-stat tradeoffs), plus 6 (PFN frequentist consistency), 12 (calibration). Books:

Shalev-Shwartz & Ben-David, Understanding Machine Learning (free) — the core. Parts I–II (PAC, uniform convergence, VC, Rademacher) are mandatory; Chapter 13 (regularization & stability) sets up Week 8.
Mohri, Rostamizadeh & Talwalkar, Foundations of Machine Learning — parallel treatment, better on Rademacher and margin bounds.
Bousquet & Elisseeff, "Stability and Generalization" (JMLR 2002 paper) — read directly; Week 8's Li et al. is built on this.
Wainwright (again) — Chapters 13–15 for minimax lower bounds (Le Cam, Fano, Assouad), which you need for Week 9 (Kim et al.). Practice:
Compute VC dimension for halfspaces and thresholds; derive the corresponding PAC sample complexity (Shalev-Shwartz exercises).
Prove a stability-based generalization bound (uniform stability ⇒ generalization) — directly reusable for Week 8.
Work one minimax lower bound via Le Cam's two-point method and one via Fano — this is the proof mechanism in Week 9.
Sketch an SQ lower bound (parity-style) — this is the mechanism in Week 10 (Wang et al.).
Pillar E — Theory of computation, circuit complexity, formal languages, logic

Scope. Regular and star-free languages, first-order logic / LTL, descriptive complexity (logic ↔ circuit classes), the circuit hierarchy AC⁰ ⊂ ACC⁰ ⊂ TC⁰ ⊂ NC¹, uniformity, and fine-grained complexity (SETH, Orthogonal Vectors) for the attention lower bounds. Your strongest area — treat this as targeted brush-up, not ground-up learning. Weeks: 3 (self-attention limits, star-free = LTL = B-RASP, saturated = TC⁰, log-precision limits), 4 (fine-grained lower bounds for attention, RASP), and 9 (CoT and serial computation, i.e. escaping TC⁰). Books:

Sipser, Introduction to the Theory of Computation — baseline; you likely have it.
Arora & Barak, Computational Complexity: A Modern Approach (draft free) — the circuit-complexity chapters (AC⁰, TC⁰, the switching lemma).
Straubing, Finite Automata, Formal Logic, and Circuit Complexity — the key text for the star-free ↔ FO ↔ AC⁰ correspondences that Week 3 (Yang–Chiang–Angluin, Merrill) depends on. Nothing else covers this as directly.
Vollmer, Introduction to Circuit Complexity — threshold circuits / TC⁰ specifically.
Strobl, Merrill, Weiss, Chiang & Angluin, "What Formal Languages Can Transformers Express? A Survey," TACL 2024 — read this before Weeks 3–4. It unifies the assumptions across every transformer-expressivity paper on the syllabus and is the single highest-leverage companion document for this block. (arXiv 2311.00208)
For fine-grained complexity: Virginia Vassilevska Williams' survey / lecture notes on SETH-based lower bounds (free). Practice:
Prove parity ∉ AC⁰ via the switching lemma (Håstad) — this is the mechanism behind Hahn's Week 3 limitation results.
Do the FO ↔ AC⁰ and LTL ↔ star-free correspondence exercises from Straubing — you'll recognize them one-to-one in Week 3.
Reduce Orthogonal Vectors to a problem to obtain a conditional quadratic lower bound — this is the mechanism in Week 4 (Keles et al., Alman–Song).
Implement a RASP program (Weiss et al., Week 4; there's a public interpreter) — e.g., sort, histogram, or a Dyck-language checker. Doing this makes the "transformers as programs" constructions concrete and is genuinely fun given your systems bent.
Pillar F — Kernels, Gaussian processes, and infinite-width theory (NTK / NNGP)

Scope. RKHS and kernel ridge regression, Gaussian processes, the NNGP (infinite-width prior) and NTK (infinite-width training) limits, signal propagation / mean-field analysis of depth. Contained but genuinely new for most systems people. Weeks: 5 (infinite attention NNGP/NTK, signal propagation and rank collapse), 11 (kernel view of fine-tuning). Books:

Rasmussen & Williams, Gaussian Processes for Machine Learning (free) — Chapters 2, 4, 6 for GP regression, kernels, and the NNGP connection.
Schölkopf & Smola, Learning with Kernels — RKHS and the representer theorem, if you want the functional-analysis grounding.
Jacot, Gabriel & Hongler, "Neural Tangent Kernel" (NeurIPS 2018) — read the original; there's no textbook that beats it for the NTK definition.
Roberts, Yaida & Hanin, The Principles of Deep Learning Theory (free) — for the signal-propagation / depthwise-covariance machinery in Week 5 (Noci et al., Hron et al.). Dense; read selectively.
Telgarsky notes (again) have a compact NTK section if you want the short version. Practice:
Derive the NNGP kernel for a one-hidden-layer network from the CLT over random weights.
Compute the NTK for a linear network and for a one-layer ReLU network; show training stays in the kernel regime under the infinite-width scaling.
Derive the kernel-ridge risk bound — connects Week 11 (Malladi et al., "fine-tuning as a kernel method").
Pillar G — RL theory, bandits, and preference optimization

Scope. MDPs, contextual bandits and regret, exploration, coverage coefficients, KL-regularized RL, the DPO/RLHF reduction to a KL-regularized bandit, 
Q∗
Q
∗
-approximation. You have the applied side; this pillar is purely about acquiring the proof formalism for what you've already implemented. Weeks: 11 (iterative RLHF under KL constraint, exploratory preference optimization), 12 (base-model coverage governs exploration; online vs offline coverage separation). Books:

Sutton & Barto, Reinforcement Learning: An Introduction (free) — baseline only.
Agarwal, Jiang, Kakade & Sun, Reinforcement Learning: Theory and Algorithms (free) — the theory text; the exploration, coverage, and regret chapters are exactly the Week 12 toolkit.
Lattimore & Szepesvári, Bandit Algorithms (free) — contextual bandits and regret, the framework Weeks 11–12 build on. Read the UCB and linear-bandit chapters.
Rafailov et al., "Direct Preference Optimization" (2023) — read directly; it's the object Xiong et al. (Week 11) generalizes. Practice:
Derive the UCB regret bound (Lattimore–Szepesvári) — the canonical regret argument you'll see specialized in Weeks 11–12.
Prove the DPO ↔ reward-model equivalence (the closed-form policy under the reverse-KL constraint). Connect it to your own work: the KL term you compute across TRL trainers (GRPO/RLOO/PPO) is the reverse-KL regularizer in Xiong et al.; your VinePPO-style branching and per-turn Bellman decomposition on KramaBench are the practical instantiation of the coverage/exploration question Foster et al. (Week 12) formalizes. Reading these two weeks against your own codebase is your highest-leverage study move in the whole course.
Work through one coverage-coefficient argument (concentrability) to see why offline data is provably insufficient without coverage (Song et al., Week 12).


