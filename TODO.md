# Project TODO
> A granular task list aligned with the six‑month roadmap (v0.1 ➜ v1.0‑paper‑release)

## 0️⃣ Foundations
- [ ] **Repo bootstrap** – create `devcontainer.json`, Poetry config, pre‑commit hooks
- [ ] **CI pipeline** – lint, type‑check, unit tests (GitHub Actions)
- [ ] **Code Style Guide** – adopt *ruff* + *black* + *mypy*

## 1️⃣ Data Layer
- [ ] Script to download & verify GSM8K
- [ ] Script to download & verify StrategyQA
- [ ] Script to download & verify LogiQA
- [ ] Unified dataset interface (`datasets/base.py`)

## 2️⃣ Representation & Validation
- [ ] Design JSON Schema for GoT (Graph‑of‑Thought)
- [ ] Implement `evo_struct/schema.py` with pydantic validation
- [ ] Unit tests: 100 valid & 100 invalid graphs

## 3️⃣ Inference Pipeline (H2)
- [ ] Wrapper for open‑source LLM (Mixtral 8x22B) via vLLM
- [ ] `infer_struct.py` – generate N candidate structures per prompt
- [ ] Deduplication & diversity filter (Jaccard < 0.8)

## 4️⃣ Genetic Programming Engine (H3)
- [ ] Integrate DEAP framework
- [ ] Custom crossover (type‑preserving) & mutation (step insertion / swap)
- [ ] Proxy fitness using GPT‑3.5 Turbo (configurable)
- [ ] Early‑stopping based on proxy‑ground‑truth correlation

## 5️⃣ Structure → CoT Translator (H4)
- [ ] Prompt templates (`translators/prompts.yaml`)
- [ ] Translator wrapper with retry & rate‑limit handling
- [ ] Coherence checker (LLM‑based)

## 6️⃣ Baselines
- [ ] Zero‑Shot‑CoT implementation
- [ ] Few‑Shot‑CoT (K=8 exemplars)
- [ ] Tree‑of‑Thought (official code port)
- [ ] Least‑to‑Most Prompting
- [ ] ReAct / Algorithm‑of‑Thought

## 7️⃣ Experiment Runner
- [ ] Hydra configs (`conf/`)
- [ ] `run_experiment.py` orchestrator
- [ ] WANDB sweeps integration

## 8️⃣ Evaluation & Stats
- [ ] Accuracy & F1 metrics per dataset
- [ ] Self‑consistency evaluation (3× sampling)
- [ ] Cost tracking (USD / prompt)
- [ ] Paired t‑test & Cliff’s Delta utilities

## 9️⃣ Reproducibility
- [ ] Dockerfile (CPU & GPU variants)
- [ ] CI workflow to run smoke tests on PRs
- [ ] Cached models via HuggingFace Hub

## 🔟 Documentation & Community
- [ ] Sphinx docs scaffold (`docs/`)
- [ ] Tutorial notebook (Colab) – “Evolving a single GSM8K example”
- [ ] Weekly build‑log template (GitHub Discussions)

## 1️⃣1️⃣ Paper & Release
- [ ] LaTeX template (neurips‑style)
- [ ] Generate tables/figures automatically from `artifacts/`
- [ ] Draft v1.0 pre‑print and submit to arXiv
- [ ] Tag `v1.0` release & Zenodo DOI

