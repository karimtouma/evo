# Evo

> **Evolving Structural Representations for Robust Chain‑of‑Thought Prompting in Large Language Models**

[![License: Apache‑2.0](https://img.shields.io/badge/license-Apache--2.0-green.svg)](LICENSE)  [![Build](https://github.com/your-org/EvoStruct-CoT/actions/workflows/ci.yml/badge.svg)](https://github.com/your-org/EvoStruct-CoT/actions/workflows/ci.yml)

---

### Abstract
*EvoStruct‑CoT* is an open research effort that investigates whether **genetically‑optimised reasoning structures** can serve as superior scaffolds for Chain‑of‑Thought (CoT) prompting. We combine **structure induction**, **genetic programming (GP)** and **LLM‑to‑LLM translation** to generate evolved CoTs that aim to outperform Zero‑Shot, Few‑Shot and state‑of‑the‑art hierarchical prompting baselines (Tree‑of‑Thought, Least‑to‑Most, ReAct).

### Why this matters
Current LLMs frequently stumble on multi‑step reasoning, producing brittle or hallucinated CoTs. By evolving an *intermediate graph‑of‑thought*—rather than handicrafting exemplars—we seek to:
1. Reduce logical errors and hallucinations.
2. Quantify and optimise reasoning quality as an explicit fitness signal.
3. Offer a transparent artefact (the structure) for downstream verification and auditing.

### Key Contributions
* **GoT Schema** — A lightweight, type‑annotated graph representation of reasoning steps.
* **EvoPrompt Engine** — A DEAP‑based GP engine that evolves GoTs with multi‑objective fitness (accuracy, coherence, cost).
* **Translator‑LM** — A wrapper that converts optimised GoTs into natural‑language CoTs consumable by any LLM back‑end.
* **Benchmark Suite** — Automated pipelines for GSM8K, StrategyQA and LogiQA with reproducible baselines.

### Repository Layout
```
.
├── evo_struct            # Core GP engine & representation utils
├── translators           # Structure‑>CoT converters
├── baselines             # Zero‑Shot, Few‑Shot, ToT, L2M, ReAct
├── datasets              # Download & preprocessing scripts
├── experiments           # Config‑driven experiment runner (Hydra)
├── evaluation            # Metrics & statistical tests
├── docs                  # Sphinx documentation
└── ci                    # GitHub Actions workflows
```

### Quick‑Start
```bash
# 1. Clone & install
$ git clone https://github.com/your‑org/EvoStruct‑CoT.git && cd EvoStruct‑CoT
$ make install   # poetry + pre‑commit hooks

# 2. Pull demo data & run a smoke test on 10 GSM8K problems
$ make demo

# 3. Launch a full experiment (configurable via YAML)
$ python -m experiments.run +exp=gsm8k_evo_struct
```

### Datasets
| Benchmark | Domain | License |
|-----------|--------|---------|
| GSM8K     | Grade‑school maths | CC BY‑SA‑4.0 |
| StrategyQA| Multi‑hop commonsense | MIT |
| LogiQA    | Logical reading | CC BY‑SA‑4.0 |

Use `make data` to download and checksum all corpora.

### Configuration
We rely on **Hydra 1.4** for experiment configuration. All configs live under `conf/` and support composable overrides:
```bash
python -m experiments.run +model=gpt4 +gp.population=64 +gp.generations=30
```

### Reproducing Paper Results
1. Ensure access to the required model endpoints (see `docs/models.md`).
2. Run `make paper` to execute the three canonical experiments.
3. Tables and plots are exported to `artifacts/paper‑results/`.

### Contributing
We welcome pull requests that improve code quality, add baselines or extend the evaluation suite. Please read `CONTRIBUTING.md` and sign the CLA to get started.

### Building in Public
Progress is tracked via the **Public Milestones** and the **Project Board** on GitHub. Weekly research updates are posted under **Discussions ▸ #build‑log**.

### Citation
If you use this work, please cite:
```bibtex
@misc{evoStructCoT2025,
  title        = {EvoStruct‑CoT: Evolving Structural Representations for Chain‑of‑Thought Prompting},
  author       = {Touma, K. and Contributors},
  year         = {2025},
  url          = {https://github.com/your‑org/EvoStruct‑CoT}
}
```

### License
Apache 2.0 — see `LICENSE` for details.

---
*Maintainers:* [@ktouma](https://github.com/ktouma) & community.

