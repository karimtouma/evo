# Evo
## EvoStruct‑CoT

> **Evolving Structural Representations for Robust Chain‑of‑Thought Prompting in Large Language Models**

[![License: Unlicense](https://img.shields.io/badge/license-Unlicense-blue.svg)](LICENSE)  [![Build](https://github.com/your-org/EvoStruct-CoT/actions/workflows/ci.yml/badge.svg)](https://github.com/your-org/EvoStruct-CoT/actions/workflows/ci.yml)

---

## 1 | Abstract
*EvoStruct‑CoT* is an **open‑science project** that studies whether *genetically‑optimised structural graphs of reasoning* can act as higher‑quality scaffolds for Chain‑of‑Thought (CoT) prompting.  
We fuse three ideas:

1. **Structure induction via LLMs** to obtain an initial *Graph‑of‑Thought* (GoT) [6].
2. **Genetic programming (GP)**, inspired by evolutionary prompt search [5], to optimise GoTs under a multi‑objective fitness function (accuracy, coherence, cost).
3. **LLM‑to‑LLM translation** to render the optimised GoT into a natural‑language CoT consumable by any target LLM.

Our hypothesis: these *Evolved CoTs* will surpass Zero‑Shot CoT [1], Few‑Shot CoT, and hierarchical prompting baselines such as Tree‑of‑Thought [2], Least‑to‑Most [3] and ReAct.

---

## 2 | Scientific Motivation
Large Language Models excel at pattern completion yet still fail on deliberate, multi‑step reasoning.  
Typical remedies—manual exemplars or *think‑step‑by‑step* heuristics—suffer from brittleness and limited coverage.  
We argue that **reasoning should be an explicit, evolvable artefact**: by treating the reasoning structure as a first‑class citizen, we can (i) *measure* its quality, (ii) *optimise* it algorithmically, and (iii) *audit* it post‑hoc.

---

## 3 | Novel Contributions
* **GoT Schema** – A type‑annotated, JSON‑serialisable representation of reasoning steps (§ `evo_struct/schema.py`).
* **EvoPrompt Engine** – A DEAP‑based GP engine for evolving GoTs with Pareto optimisation over **Accuracy**, **Self‑Consistency** [7] and **Token‑Cost**.
* **Translator‑LM** – A modular component that converts any GoT into a coherent CoT using templating or an auxiliary LLM.
* **Cost‑Aware Benchmarking** – Every experiment logs \$‑per‑correct‑answer, enabling realistic trade‑off analysis.

---

## 4 | Background & Related Work
| Topic | Key Papers |
|-------|------------|
| Chain‑of‑Thought Prompting | Wei *et al.* (2022) [1] |
| Hierarchical Reasoning | Yao *et al.* – Tree‑of‑Thought (2023) [2]; Arora *et al.* – Graph‑of‑Thought (2025) [6] |
| Prompt Evolution | Guo *et al.* – PromptBreeder (2023) [5] |
| Decomposition & Planning | Zhou *et al.* – Least‑to‑Most (2022) [3]; Gao *et al.* – PAL (2023) [4] |
| Self‑Consistency | Zhang *et al.* (2023) [7] |

Our work is the **first to unify** LLM‑based structure induction **and** GP‑driven optimisation within a single, reproducible framework.

---

## 5 | Repository Layout
```text
.
├── evo_struct            # Core GP engine & GoT utilities
├── translators           # GoT → CoT converters
├── baselines             # Zero‑Shot, Few‑Shot, ToT, L2M, ReAct
├── datasets              # Download & preprocessing scripts
├── experiments           # Hydra‑driven runner
├── evaluation            # Metrics & statistical tests
├── docs                  # Sphinx documentation
└── ci                    # GitHub Actions workflows
```

---

## 6 | Quick‑Start
```bash
# Clone & install (Poetry + pre‑commit)
$ git clone https://github.com/your‑org/EvoStruct‑CoT.git && cd EvoStruct‑CoT
$ make install

# Smoke test on 10 GSM8K problems
$ make demo

# Full experiment with custom params
$ python -m experiments.run +exp=gsm8k_evo_struct \
      +model=gpt4 +gp.population=64 +gp.generations=30
```

---

## 7 | Datasets
| Benchmark  | Domain                   | License      |
|------------|--------------------------|--------------|
| GSM8K      | Grade‑school mathematics | CC BY‑SA 4.0 |
| StrategyQA | Multi‑hop commonsense    | MIT          |
| LogiQA     | Logical reading          | CC BY‑SA 4.0 |

Run `make data` to fetch and checksum all corpora.

---

## 8 | Reproducing the Paper
```bash
# 1. Ensure API keys / local models are configured (docs/models.md)
# 2. Execute the three canonical experiments
$ make paper
# 3. Results (CSV + plots) will appear under artifacts/paper‑results/
```

---

## 9 | Building in Public
* 🗓 **Weekly Research Logs** – posted under *GitHub Discussions ▸ #build‑log* every Friday.
* 📊 **Project Board** – Kanban tracking of TODO.md.
* 🔖 **Public Milestones** – semantic versioning (`v0.1`, `v0.2‑beta`, `v1.0‑paper`).

---

## 10 | Contributing
Pull requests that introduce new baselines, improve evaluation, or harden infrastructure are welcome.  
Please read `CONTRIBUTING.md` and sign the CLA.

---

## 11 | Citation
```bibtex
@misc{touma2025evostruct,
  title  = {EvoStruct‑CoT: Evolving Structural Representations for Chain‑of‑Thought Prompting},
  author = {Touma, Karim},
  year   = {2025},
  howpublished = {GitHub repository},
  url    = {https://github.com/karimtouma/evo}
}
```

---

## 12 | License
This project is released under **The Unlicense** – see `LICENSE` for details.  
*"This is free and unencumbered software released into the public domain."*

---

## 13 | Bibliography
[1] Wei et al., *Chain‑of‑Thought Prompting Elicits Reasoning in Large Language Models*, 2022.  
[2] Yao et al., *Tree‑of‑Thought Deliberate Reasoning*, 2023.  
[3] Zhou et al., *Least‑to‑Most Prompting Enables Complex Reasoning in LLMs*, 2022.  
[4] Gao et al., *PAL: Program‑Aided Language Models*, 2023.  
[5] Guo et al., *PromptBreeder: Gradient‑Free Prompt Evolution for LLMs*, 2023.  
[6] Arora et al., *Graph‑of‑Thought: Unifying Structured Reasoning for LLMs*, 2025.  
[7] Zhang et al., *Automatic Chain‑of‑Thought Prompting via Self‑Consistency*, 2023.

---
*Maintainers:* [@karimtouma](https://github.com/karimtouma).

