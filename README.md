# 99p: Unsupervised Failure Axis & Open-Question Discovery

[![Institution: UC Berkeley](https://img.shields.io/badge/Institution-UC%20Berkeley%20CDSS%20170-blue.svg)](https://cdss.berkeley.edu/)
[![Partner: 99P Labs](https://img.shields.io/badge/Partner-99P%20Labs%20%2F%20Honda%20Research%20Institute-red.svg)](https://99plabs.com/)
[![Track: NeurIPS / CVPR / ICRA](https://img.shields.io/badge/Target-NeurIPS%20%7C%20CVPR%20%7C%20ICRA%20%7C%20ACL-purple.svg)](docs/PUBLISHABLE_PROPOSALS.md)

> **Discovering what a system does not know, without having to predefine the taxonomy of ignorance in advance.**

This repository hosts research conducted in collaboration with **99P Labs / Honda Research Institute, US** and **UC Berkeley CDSS 170 (Fall 2026)**, mentored by **Ryan Lingo** (Applied AI Research Engineer, Honda Research Institute).

---

## 1. The Core Research Question

When an autonomous system (such as a driving policy or large language model) fails, the standard engineering workflow relies on human guesswork: engineers draft a discrete list of conditions they expect to be challenging (e.g., rain, night, merges, or keyword topics), test the model across those bins, and collect more data wherever the score is worst.

**The Fatal Flaw**: This process can only locate failure modes somebody thought to name. Whatever is not on the checklist remains invisible. For safety-critical robotics and scientific discovery, the real "hard" situations are compound edge cases that nobody writes down in advance.

**Our Core Hypothesis**:  
**The system's internal latent space (activations, Sparse Autoencoder latents, and layered claim abstractions) already separates the distinct classes of situations it struggles with.** By reading internal representations directly, we can automatically discover unsupervised failure axes and high-value open questions.

---

## 2. Documentation Architecture

For comprehensive details, review the specialized research documents in [`docs/`](docs/):

| Document | Purpose | Target Audience |
| :--- | :--- | :--- |
| [**`docs/AGENT_GUIDE.md`**](docs/AGENT_GUIDE.md) | Operational handbook, constraints, API keys, and execution protocols | Autonomous AI agents & new developers |
| [**`docs/RESEARCH_PURPOSE.md`**](docs/RESEARCH_PURPOSE.md) | Problem formulation, dual tracks (Text vs. Policy), milestones, and deliverables | Academic advisors & research leads |
| [**`docs/LITERATURE_REVIEW.md`**](docs/LITERATURE_REVIEW.md) | Deep literature review across SDM, VLA probing, generative simulation, and research gaps | Researchers writing paper related works |
| [**`docs/CURRENT_IDEAS.md`**](docs/CURRENT_IDEAS.md) | Synthesis of brainstormed domains (Wildfire, E-Waste, Sensor Grid) and team discussions | Team brainstorming & ideation |
| [**`docs/PUBLISHABLE_PROPOSALS.md`**](docs/PUBLISHABLE_PROPOSALS.md) | 5 publication-ready conference proposals (NeurIPS, CVPR, ICRA, IROS, ACL) | Paper authorship & project selection |
| [**`docs/refined proposals.md`**](<docs/refined proposals.md>) | TL;DR pitches, exigence (why now?), and prior research gap mappings | Quick executive pitches & gap review |
| [**`docs/PROJECT_BRIEF_DIFF_AND_IMPROVEMENTS.md`**](docs/PROJECT_BRIEF_DIFF_AND_IMPROVEMENTS.md) | Diff analysis of Chris's project brief & 6 concrete tactical improvements | Strategic review & technical roadmap |
| [**`docs/FEEDBACK_FOR_CHRIS.md`**](docs/FEEDBACK_FOR_CHRIS.md) | Peer review & strategic recommendations to send directly to Chris | Team feedback & consensus document |
| [**`docs/FUTURE_PLANS.md`**](docs/FUTURE_PLANS.md) | 12-week semester roadmap, baseline specs, compute resources, and risk analysis | Project management & sprint planning |
| [**`references.bib`**](references.bib) | Curated BibTeX database of foundational and cutting-edge citations | Citation management & LaTeX drafting |

---

## 3. The 5 Publishable Research Proposals

We have formulated five high-impact, conference-grade research proposals designed for publication in IEEE and top-tier AI venues:

1. [**ActAxis (NeurIPS / CVPR)**](docs/PUBLISHABLE_PROPOSALS.md#proposal-1-actaxis--unsupervised-failure-axis-discovery-in-vision-language-action-policies-via-sparse-autoencoder-latents):  
   - **TL;DR**: Decomposes intermediate VLA activations using overcomplete Sparse Autoencoders (SAEs) to discover monosemantic, steerable failure axes without predefined labels.
   - **Exigence & Gap**: Fleet scaling stalls on unknown unknowns. Solves the scalar-only prediction limitation in [SAFE (2025)](references.bib) and input-space bias in [Domino (ICLR 2022)](references.bib).
2. [**SimLoop (IEEE ICRA / IROS / T-IV)**](docs/PUBLISHABLE_PROPOSALS.md#proposal-2-simloop--closing-the-loop-on-discovered-failure-modes-via-controllable-scenario-diffusion-and-active-fine-tuning):  
   - **TL;DR**: Inverts discovered activation failure clusters into parametric simulation scenarios (CARLA/CTG++) to actively retrain policies and eliminate failure modes ($>80\%$ failure reduction).
   - **Exigence & Gap**: Discovering failure is useless without retraining. Automates the manual query bottleneck in [Mobileye Meteor/Genario (2026)](references.bib) and static gap bounds in [RESample (ICRA 2024)](references.bib).
3. [**SpecGap (ACL / EMNLP / NeurIPS AI for Science)**](docs/PUBLISHABLE_PROPOSALS.md#proposal-3-specgap--contrastive-claim-evidence-provenance-graphs-for-falsifiable-open-question-discovery):  
   - **TL;DR**: Transforms scientific literature into atomic claim-evidence provenance graphs to detect cross-paper tensions and surface falsifiable open research questions.
   - **Exigence & Gap**: AI science suffers from hallucinated, ungrounded ideas. Replaces subjective scoring in [The AI Scientist (2024)](references.bib) with objective planted holdouts and [Evidence-Based Backtesting (2026)](references.bib).
4. [**ConceptProbe-SDM (IEEE T-ITS / CVPR)**](docs/PUBLISHABLE_PROPOSALS.md#proposal-4-conceptprobe-sdm--disentangling-perception-shifts-vs-cognitive-reasoning-bottlenecks-in-autonomous-fleets):  
   - **TL;DR**: Employs dual linear probing across vision tokens vs. action tokens to resolve accident liability: did the sensor fail to perceive the hazard, or did the planner fail to act?
   - **Exigence & Gap**: Monolithic driving models ([DriveVLM (2024)](references.bib)) obscure whether crashes stem from sensor degradation or reasoning collapse across the 80-slot sensor reliability grid.
5. [**AutoCurriculum-VLA (ICLR / CoRL)**](docs/PUBLISHABLE_PROPOSALS.md#proposal-5-autocurriculum-vla--self-critiquing-policy-introspection-for-targeted-counterfactual-edge-case-discovery):  
   - **TL;DR**: Converts passive rollouts into active introspection: surges in epistemic uncertainty trigger an adversarial LLM to apply minimal counterfactual scene mutations, mapping the policy failure frontier.
   - **Exigence & Gap**: Passive fleet testing requires millions of miles per edge case. Upgrades static monitors in [RoboMonkey (IROS 2025)](references.bib) and [ReasonBreak (NeurIPS 2025)](references.bib) into an active self-critique curriculum.

---

## 4. Evaluation Methodology: Planted Gaps & Catherine's Baselines

To eliminate subjective evaluation and circular reasoning, all experiments adhere to strict quantitative protocols:

### 4.1 Planted Gap Ground Truth
Before model training or rollout collection, we deliberately withhold known subsets of data or failure modes to form an objective ground truth $\mathcal{G}^*$. Discovery performance is measured via:
$$\text{Precision} = \frac{|\mathcal{A}_{\text{discovered}} \cap \mathcal{G}^*|}{|\mathcal{A}_{\text{discovered}}|}, \quad \text{Recall} = \frac{|\mathcal{A}_{\text{discovered}} \cap \mathcal{G}^*|}{|\mathcal{G}^*|}$$

### 4.2 Catherine's Three Mandatory Baselines
To prove that internal representations provide genuine signal over superficial heuristics, any proposed method must outperform:
1. **Baseline 1 (Random Data Collection)**: Uniform random sampling of data slices or candidate questions.
2. **Baseline 2 (Predefined Human Taxonomy)**: Standard human heuristic categorization (e.g., Weather $\times$ Lighting $\times$ Maneuver).
3. **Baseline 3 (Behavioral / Output-Only Clustering)**: Clustering scenario failures based solely on output trajectory loss, action deviations, or collision telemetry—**without looking at internal activations**.

---

## 5. Quick Start for Researchers & Agents

```bash
# Clone and enter repository
git clone https://github.com/Imhaohao/99p.git
cd 99p

# View agent guide and operational rules
cat docs/AGENT_GUIDE.md

# Inspect bibliographic citations
cat references.bib
```

### Team Contacts
- **Jerry Yan (Zihao Yan)** (`imhaohao@berkeley.edu`)
- **Chris**
- **Catherine Wang** (`cattayw@berkeley.edu`)
- **Hiram Lannes** (`hiram_lannes@berkeley.edu`)
- **Jason** (`jhe08@berkeley.edu`)
- **Ryan Lingo** (Industry Mentor, Honda Research Institute / 99P Labs)
