# Architectural Security Analysis of Electro-Mechanical Braking Systems and AI-Based Threat Vectors

**Supplementary material:** data, prompts, raw model outputs and extended results.

> 📄 **Paper:** _[venue / preprint link — TBD]_ · **Authors:** _TBD_ · **Status:** under review

This repository holds everything behind the paper that did not fit in the page limit:
the ANSYS Medini Analyze TARA models, the exact prompt given to each AI model, all 15 AI
responses, five repeated runs per model and their intersection, the full TARA tables, and the
complete set of comparison figures and matrices.

---

## Abstract

Electro-mechanical brakes (EMB) are a key technology for brake-by-wire vehicles, but their
reliance on electronic controllers, sensors, wheel-end actuators (WEAs) and communication
networks opens new cybersecurity attack surfaces. We perform an ISO/SAE 21434 Threat Analysis
and Risk Assessment (TARA) using the STRIDE threat model on three candidate EMB architectures
(**MCU + Axle ECU**, **MCU + Pedal-direct**, **MCU + Auxiliary ECU**), derived from Peng et al. (2024).
Each architecture is modeled in ANSYS Medini Analyze (reference analysis) and analyzed
independently by five AI models using the same prompt and architecture image. We compare
threat coverage, STRIDE category distribution, severity ratings and tool-specific findings,
and find that AI models are architecture-dependent, complementary to tool-based TARA, and
require expert validation.

---

## Repository structure

The folders follow the methodology workflow of the paper (Fig. 7):
**architectures → reference TARA (Medini) + AI TARA → normalization → comparison.**

```
emb-tara-ai/
├── paper/                  Paper PDF and the full-length draft
├── references/             Bibliography (.bib) and list of cited papers
├── architectures/          The three EMB architectures (diagram given to the AI models)
│   ├── pedal-direct/       Arch. 1: MCU + Pedal-direct
│   ├── aux-ecu/            Arch. 2: MCU + Auxiliary ECU
│   └── axle-ecu/           Arch. 3: MCU + Axle ECU
├── medini/                 Reference TARA in ANSYS Medini Analyze
│   └── exports/<arch>/     Threat reports (raw + with risk levels) and architecture model
├── ai-analysis/            AI-assisted STRIDE analysis
│   ├── prompt/             The exact prompt used (paper Appendix A)
│   ├── responses/<arch>/   Response of each model used in the paper (5 models × 3 architectures)
│   ├── runs/<arch>/<model>/  Five repeated runs of the same prompt (run1–run5)
│   └── intersection/       Threats found in all five runs, per architecture + the prompt used
├── common-threats/         Threats common to all three architectures + their TARA (per source)
│   └── prompts/            Prompts for Medini and for the AI models
├── results/
│   ├── tara/               Full ISO/SAE 21434 TARA per architecture + cross-reference of all tools
│   ├── comparison/         Threat detection comparison matrices
│   ├── figures/            Result figures, including those cut from the paper
│   └── tables/             Summary tables
├── scripts/                Code used to generate the figures
└── supplementary/          Extended text cut from the paper
```
Each folder has its own `README.md` describing its contents and file conventions.

---

## Architectures

| ID              | No.     | Architecture         | Controllers         | Power layout | Comm. layout | Redundancy | Medini threats |
|-----------------|---------|----------------------|---------------------|--------------|--------------|------------|----------------|
| `pedal-direct`  | Arch. 1 | MCU + Pedal-direct   | Single MCU          | Full red.    | "X"-circuit  | Low        | 192 |
| `aux-ecu`       | Arch. 2 | MCU + Auxiliary ECU  | MCU + Aux ECU       | "X"-circuit  | "H"-circuit  | Medium     | 228 |
| `axle-ecu`      | Arch. 3 | MCU + Axle ECU       | MCU + 2 Axle ECUs   | "H"-circuit  | "H"-circuit  | High       | 243 |

The IDs are used in every folder and file name. Some spreadsheets and figures use the numbers (Arch. 1–3, A1–A3).

## Tools analyzed

| ID           | Tool                      | Type           | Native severity |
|--------------|---------------------------|----------------|-----------------|
| `medini`     | ANSYS Medini Analyze      | Reference TARA | ✔ |
| `perplexity` | Perplexity Sonar          | AI model       | ✔ |
| `gemini`     | Gemini 3.8 Flash          | AI model       | ✘ (estimated) |
| `deepseek`   | DeepSeek-V3               | AI model       | ✘ (estimated) |
| `claude`     | Claude Sonnet 5           | AI model       | ✔ |
| `chatgpt`    | GPT-5.6 Luna              | AI model       | ✔ |
| `qwen`       | Qwen 3.7 Plus             | AI model (extra, not in the paper) | ✔ |

Qwen 3.7 Plus is included only in `ai-analysis/runs/` and `ai-analysis/intersection/`. It is not
part of the paper's comparison, and its intersection is available for `pedal-direct` only.

---

## Paper ↔ repository map

| Paper element | Where to find it |
|---|---|
| Fig. 3–6: EMB architectures | [`architectures/`](architectures/), [`medini/exports/`](medini/exports/) |
| Table I: Limitations of Peng et al. | [`supplementary/`](supplementary/) |
| Table II: Architecture comparison | [`architectures/README.md`](architectures/README.md) |
| Sec. III-B: Medini reference TARA | [`medini/`](medini/) |
| Sec. III-C / Appendix A: AI prompt | [`ai-analysis/prompt/`](ai-analysis/prompt/) |
| Raw AI outputs (not in paper) | [`ai-analysis/responses/`](ai-analysis/responses/) |
| Repeated runs and their intersection (not in paper) | [`ai-analysis/runs/`](ai-analysis/runs/), [`ai-analysis/intersection/`](ai-analysis/intersection/) |
| Threat totals of the intersection vs. Medini (not in paper) | [`results/figures/`](results/figures/) `threat_totals_intersection_*.png` |
| Full TARA tables (not in paper) | [`results/tara/`](results/tara/) |
| Mitigation tables | [`results/tables/`](results/tables/) `mitigation_tables.docx` |
| Fig. 9–11: Threat totals per tool | [`results/figures/`](results/figures/) `threat_totals_*.png` |
| Fig. 13: Medini STRIDE × risk level per architecture | [`results/figures/`](results/figures/) `medini_stride_by_architecture.png`, [`results/tables/`](results/tables/) |
| Fig. 15–17: Severity analysis | [`results/figures/`](results/figures/) `severity_*.png` |
| Fig. 18–20: Detection comparison matrices | [`results/comparison/`](results/comparison/) `matrix_*.png` |

---

## Reproducing the analysis

1. **Architectures:** take the diagram from `architectures/<arch>/`.
2. **Reference TARA:** the Medini threat reports are in `medini/exports/<arch>/` (ANSYS Medini Analyze
   2025 R1.01, build 25.1.1.250228184338-79474c9; see `medini/medini_version.png`).
3. **AI TARA:** give `ai-analysis/prompt/stride_prompt.md` plus the architecture diagram to each model.
   The paper uses one response per model and architecture (`ai-analysis/responses/`), each obtained
   in a fresh session, on _date TBD_.
   The prompt was also run five times per model (`ai-analysis/runs/`), and the threats found in all
   five runs are in `ai-analysis/intersection/`, produced with `ai-analysis/intersection/prompt.md`
   (see [Repeated runs](#repeated-runs-and-intersection)).
4. **Match:** threats are matched across tools by element + STRIDE category; see the cross-reference
   sheets in `results/tara/`.
5. **Compare:** figures and matrices are in `results/`; generation code in `scripts/`.

## Repeated runs and intersection

Each intersection file keeps the input layout and adds a `Cross-run comparison` sheet (every threat
found in any run, per run). Threats are matched on STRIDE category + target element, and a threat is
kept when it appears in all five runs.

| Model | Threats in all 5 runs (pedal-direct / aux-ecu / axle-ecu) |
|---|---|
| Gemini 3.8 Flash | 27 / 44 / 46 |
| Claude Sonnet 5 | 35 / 48 / 46 |
| Perplexity Sonar | 56 / 74 / 81 |
| GPT-5.6 Luna | 55 / 60 / 54 |
| DeepSeek-V3 | 39 / 57 / 39 |
| Qwen 3.7 Plus (extra) | 35 / – / – |

Notes:
- **Perplexity, pedal-direct:** `run2.xlsx` and `run3.xlsx` are identical, so this intersection is in effect based on four distinct runs.
- **DeepSeek-V3** gives no severity, so only threat IDs are compared.
- **Gemini 3.8 Flash** gives a severity in only some runs, so its intersection files have no Severity column.

## Citation

If you use this material, please cite the paper (see also [`CITATION.cff`](CITATION.cff)):

```bibtex
@inproceedings{emb_tara_ai_2026,
  title     = {Architectural Security Analysis of Electro-Mechanical Braking Systems and AI-Based Threat Vectors},
  author    = {TBD},
  booktitle = {TBD},
  year      = {2026}
}
```

## License

- Code (`scripts/`): MIT, see [`LICENSE`](LICENSE).
- Data, prompts, figures and text: [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/).
- Architecture figures are reprinted from Peng et al., _Actuators_ 13(9):346, 2024 (CC BY 4.0).
- Third-party papers are **not** redistributed; see [`references/`](references/) for links.
