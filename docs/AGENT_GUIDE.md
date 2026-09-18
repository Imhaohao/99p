# Agent Guide: 99P Labs / Honda Workspace

> **Notice to Incoming Agents**: This document is the primary onboarding interface for autonomous agents and LLM assistants operating in this repository. Read this document first to understand the team context, operational rules, system architecture, and current task priorities.

---

## 1. Project Identity & Team Context

- **Course & Institution**: UC Berkeley CDSS 170 (Fall 2026) — Data Discovery Project.
- **Industry Partner**: [99P Labs](https://99plabs.com/) / **Honda Research Institute, US** (HRI-US).
- **Project Lead & Industry Mentor**: **Ryan Lingo** (Applied AI Research Engineer, Honda Research Institute).
- **Student Research Team**:
  - **Jerry Yan (Zihao Yan)** (`imhaohao@berkeley.edu`) — Research Investigator / Architecture & Repository Lead.
  - **Chris** — Failure Probing & Policy Scenarios.
  - **Catherine Wang** (`cattayw@berkeley.edu`) — Evaluation Metrics, Baseline Benchmarking & Rigor.
  - **Hiram Lannes** (`hiram_lannes@berkeley.edu`) — Mentoring Agreements, Pipeline Scaffolding & Integration.
  - **Jason** (`jhe08@berkeley.edu`) — Data Engineering & Holdout Design.
- **GitHub Repository**: `Imhaohao/99p`
- **Local Workspace Path**: `/Users/yanzihao/Documents/honda`

---

## 2. Executive Research Mission

> **Core Objective**: Build an AI system that develops layered abstractions over its domain, critiques its own internal representations, and discovers **unsupervised failure axes and open knowledge gaps** without requiring human engineers to pre-specify the taxonomy of failures in advance.

### The Dual-Track Formulation
The project bridges two complementary paradigms:
1. **Track A (Text Knowledge System - Course Spec)**:
   Extracts layered conceptual abstractions from a synthetic corpus, performs automated self-critique, and identifies high-priority open scientific questions evaluated against planted holdout gaps or historical backtesting.
2. **Track B (Robotics / Driving Policy Failure Discovery - Honda Interp Spec)**:
   Extracts internal activations and Sparse Autoencoder (SAE) latent features across policy rollouts (e.g., OpenVLA, trajectory planners) to discover previously unknown failure axes. Evaluated with planted data holdouts (precision/recall on discovered axes) and closed-loop sim-retraining (e.g., CARLA / MetaDrive).

---

## 3. Repository Directory Structure

```
/Users/yanzihao/Documents/honda/
├── README.md                     # High-level overview and landing page for researchers
├── references.bib                # Standard BibTeX database of relevant literature
└── docs/
    ├── AGENT_GUIDE.md            # [THIS FILE] Operational handbook for autonomous agents
    ├── RESEARCH_PURPOSE.md       # Comprehensive problem formulation, motivation, and course requirements
    ├── LITERATURE_REVIEW.md      # Deep academic literature review, taxonomy, and research gap matrix
    ├── CURRENT_IDEAS.md          # Brainstormed application domains and baseline requirements
    ├── PUBLISHABLE_PROPOSALS.md  # 5 publication-ready conference proposals (NeurIPS, CVPR, ICRA, ACL)
    ├── refined proposals.md      # TL;DR pitches, exigence, and prior research gap mappings
    ├── PROJECT_BRIEF_DIFF_AND_IMPROVEMENTS.md # Diff report & tactical improvements on Chris's brief
    ├── FEEDBACK_FOR_CHRIS.md     # Peer review & strategic recommendations to send to Chris
    ├── FUTURE_PLANS.md           # 12-week semester roadmap, baseline specs, compute, and deliverables
    └── domain-candidates.md      # Initial exploratory notes on candidate grids (sensors, fictional laws)
```

---

## 4. Compute Resources & Tooling Environment

1. **UC Berkeley CDSS Nautilus NRP LLM API**:
   - OpenAI-compatible endpoint: `https://ellm.nrp-nautilus.io/v1`
   - Authorization: Bearer token provided by course infrastructure.
   - Intended use: High-throughput synthetic text generation, structured claim extraction, and LLM-as-a-judge self-critique.
2. **Robotics / Driving Environments**:
   - `OpenVLA` (7B parameter open vision-language-action model based on Llama-2 / Prismatic).
   - Simulators: `CARLA`, `MetaDrive`, or lightweight 2D kinematics (`HighwayEnv` / `Gym-Duckietown`).
3. **Core Python Stack**:
   - PyTorch, Hugging Face `transformers`, `accelerate`.
   - Interpretability: `sae_lens`, `transformer_lens`, linear probing via `scikit-learn`.
   - Unsupervised Clustering: HDBSCAN, UMAP, Gaussian Mixture Models.
   - Text Processing & Embeddings: `sentence-transformers`, `faiss-cpu`, `spacy`.

---

## 5. Non-Negotiable Research Constraints & Baselines

When developing methods or running experiments in this repository, agents MUST respect the baseline controls formulated during team discussions:

1. **Failure Discovery vs. Failure Detection**:
   - *Do NOT* build another runtime anomaly detector that flags "this episode will crash" (saturated area).
   - *Build* an engine that discovers the **axis / category of failure** (e.g., "low-sun angle glare behind large vehicles causing distance underestimation").
2. **Catherine's Required Baselines**:
   Any discovered failure axis or open question must be benchmarked against:
   - **Baseline 1 (Random Selection)**: Uniformly sampling candidate data slices / questions.
   - **Baseline 2 (Human Predefined Taxonomy)**: Standard heuristic splits (e.g., weather = rain/fog/night).
   - **Baseline 3 (Behavioral / Output-Only Clustering)**: Clustering trajectory errors or loss without looking at internal model activations.
3. **Planted Gap Evaluation Metric**:
   Every dataset or rollout collection must maintain a controlled holdout split $\mathcal{G}^*$:
   $$\text{Precision} = \frac{|\mathcal{A}_{\text{discovered}} \cap \mathcal{G}^*|}{|\mathcal{A}_{\text{discovered}}|}, \quad \text{Recall} = \frac{|\mathcal{A}_{\text{discovered}} \cap \mathcal{G}^*|}{|\mathcal{G}^*|}$$

---

## 6. Current Implementation State

- **Stage**: Scaffolding & Conceptual Design (Weeks 1–3).
- **Next Immediate Tasks**:
  - Implement synthetic data generation pipeline for the chosen domain with planted holdout gaps.
  - Implement activation extraction hooks for policy rollout episodes.
  - Set up baseline clustering algorithms (HDBSCAN on activations vs. HDBSCAN on output actions).
