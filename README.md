# LLM Behavioral Analysis Through Domain-Specific Engineering Benchmarks

**A systematic study of how 22 large language models reason, fail, and produce convincing wrong answers — using wastewater treatment plant engineering as the testing domain.**

This repository documents 13 benchmarks, 22 models, and 13 individual behavioral analysis reports. The focus is not on which model scores highest. It is on how models think, where they fail, and why their failures become harder to detect as their knowledge increases.

[![Kaggle Benchmarks](https://img.shields.io/badge/Platform-Kaggle%20Benchmarks-20BEFF?logo=kaggle)](https://www.kaggle.com/benchmarks/mehmetisik/wwtp-engineering-benchmark)
[![Reports](https://img.shields.io/badge/Reports-13%20Published-1B4F72)]()
[![Models](https://img.shields.io/badge/Models%20Tested-22-2E86C1)]()
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

---

## Why This Repository Exists

Standard LLM evaluations measure correctness: did the model get the right answer? This project goes further. Each benchmark is designed with a specific cognitive trap — a plausible wrong answer that exploits a known reasoning shortcut. The analysis focuses on *how* models arrive at wrong answers, what patterns emerge across model families, and whether failures become more dangerous as models become more knowledgeable.

Wastewater treatment plant (WWTP) engineering serves as the vehicle, not the destination. The domain was chosen because it requires integrating safety protocols, material science, process chemistry, and operational judgment — areas where training data is thin and textbook answers are often insufficient. The behavioral findings, however, generalize beyond this domain.

This work is intended for LLM evaluators, AI safety researchers, and engineers assessing LLM reliability for domain-critical decisions.

---

## Key Findings Across 13 Benchmarks

### The Failure Mode Spectrum

Across the series, LLM failures organize into a three-level spectrum where detectability decreases as model knowledge increases:

| Failure Mode | Description | Example | Detectability |
|:---|:---|:---|:---|
| **Hazard Blindness** | Model does not identify the relevant risk | Tool Selection (#8): models ignored explosion risk in confined space | Easy — absence of relevant reasoning |
| **Partial Knowledge** | Model identifies the problem but applies the wrong solution | SCADA Cabling (#10): models identified EMI risk but chose same-conduit routing | Moderate — correct problem, wrong fix |
| **Judgment Error** | Model identifies the problem, evaluates it, and makes the wrong call | Odor Pipe (#11): 12 models discussed UV degradation then chose UV-vulnerable FRP | Hard — reasoning sounds complete and authoritative |

This is the series' central finding: **as models' knowledge increases, their wrong answers become more convincing and harder to identify as errors.**

### The Cumulative Funnel

Every benchmark narrows the pool of models that have passed all questions so far:

```
22 → 17 → 15 → 2 → 0 → 0 → 0 → 0 → 0 → 0 → 0 → 0 → 0
```

The funnel reached zero at benchmark #5 and has remained there through eight additional benchmarks of varying difficulty — from 95.5% pass rate to 14% pass rate. **No model has passed all 13 questions.** This closure appears structural, not coincidental.

### No Family Is Reliable

Every model family has experienced significant failure:

- **Claude** maintained a perfect record for 9 consecutive benchmarks, then fell to 40% on SCADA Cabling (#10) and 40% on Odor Pipe (#11).
- **Gemini** collapsed to 33% on Walkway Material (#5), recovered to 100% on SCADA Cabling (#10), then collapsed again to 33% on Odor Pipe (#11).
- **Qwen** scored 0/4 on Odor Pipe (#11) — its first complete family failure — then returned to 100% on the next benchmark.
- **Gemma** oscillated between 0% and 100% across consecutive benchmarks.
- **DeepSeek R1** encountered formatting-related parsing issues in 10 of 13 benchmarks (77%), losing correct answers to `<think>` block artifacts.

Family performance is question-dependent, not inherent. Past consistency does not predict future reliability.

### The Trap Taxonomy

Each benchmark exploits a different cognitive shortcut. Thirteen benchmarks have produced thirteen distinct trap types:

| # | Benchmark | Trap | Pass Rate |
|:--|:----------|:-----|----------:|
| 1 | Equipment Material Selection | *(no trap — baseline)* | 100% |
| 2 | Pump Root Cause Analysis | Electrical Trap | 77% |
| 3 | Dewatering System Root Cause | Local Trap | 68% |
| 4 | Biogas Desulfurization | Aerobic Trap | 14% |
| 5 | Digester Walkway Material | Corrosion Trap (FRP — Structural) | 36% |
| 6 | Confined Space Emergency Response | "Almost Safe" Trap | 68% |
| 7 | Sample Preservation Protocol | Acid Trap | 95.5% |
| 8 | Confined Space Tool Selection | "False Safe" Trap | 68.2% |
| 9 | Activated Sludge Emergency Flocculation | Coagulant Trap | 68.2% |
| 10 | SCADA Cabling Standards | Cost-Reliability Trap | 63.6% |
| 11 | Odor Collection Pipe Material Selection | UV Anchoring (FRP — UV) | 27.3% |
| 12 | Primary Clarifier Design Criteria | Shape Trap | 86.4% |
| 13 | Emergency Response Sequencing | Urgency Trap | 77.3% |

All traps exploit the same fundamental pattern: **anchoring on the most salient feature** while underweighting context-specific criteria that determine the correct answer.

### Additional Behavioral Patterns

- **"Newer ≠ Better"**: Across three benchmarks with Gemini generational splits, older models (2.0) outperformed newer models (2.5, 3.x) with a 2:1 advantage. The "newer is better" assumption does not hold.
- **"Bigger ≠ Better"**: Gemma 4B outperformed Gemma 27B on multiple benchmarks. Qwen Coder 480B failed where Qwen Next 80B Instruct passed. Specialization and parameter count do not guarantee domain expertise.
- **Thinking Paradox**: On Emergency Flocculation (#9), Qwen Thinking spent 4,722 tokens and arrived at the wrong answer. Qwen 235B spent 254 tokens and was correct. When the initial framework is wrong, longer deliberation deepens the error rather than correcting it.
- **R1 Parsing Saga**: DeepSeek R1's `<think>` block caused parsing failures in 10 of 13 benchmarks. In 7 cases, the correct answer was lost to formatting. On benchmarks #11 and #13, R1 produced genuine wrong answers — ending the "correct reasoning, lost to formatting" narrative.

---

## The Benchmark Series

### Difficulty Tiers

The 13 benchmarks fall into three tiers based on observed pass rates:

- **Easy (>85%)**: Questions where the answer is well-represented in training data and the logical chain is direct.
- **Mid-range (63–77%)**: Questions requiring domain-specific knowledge beyond common training data. Six benchmarks cluster in this range, suggesting a natural difficulty ceiling for current-generation LLMs.
- **Hard (<40%)**: Questions requiring simultaneous multi-criteria evaluation where the most salient criterion is not the decisive one.

### Reports

Each benchmark has a dedicated behavioral analysis report. Reports follow a consistent structure: executive summary, question analysis, complete results for all 22 models, LLM behavior analysis (3–6 subsections), cross-benchmark comparison, and methodology notes.

| # | Report | Tier | Pass Rate | PDF | Kaggle |
|:--|:-------|:-----|----------:|:----|:-------|
| 1 | Equipment Material Selection | Easy | 100% | [Report](report/WWTP%20Equipment%20Material%20Selection.pdf) | [Benchmark](https://www.kaggle.com/benchmarks/tasks/mehmetisik/wwtp-equipment-material-selection) |
| 2 | Pump Root Cause Analysis | Mid | 77% | [Report](report/WWTP%20Root%20Cause%20Analysis.pdf) | [Benchmark](https://www.kaggle.com/benchmarks/tasks/mehmetisik/wwtp-root-cause-analysis) |
| 3 | Dewatering System Root Cause | Mid | 68% | [Report](report/WWTP%20Dewatering%20System%20Root%20Cause.pdf) | [Benchmark](https://www.kaggle.com/benchmarks/tasks/mehmetisik/wwtp-dewatering-system-root-cause) |
| 4 | Biogas Desulfurization Recovery | Hard | 14% | [Report](report/WWTP%20Biogas%20Desulfurization%20Recovery.pdf) | [Benchmark](https://www.kaggle.com/benchmarks/tasks/mehmetisik/wwtp-biogas-desulfurization-recovery) |
| 5 | Digester Walkway Material Selection | Hard | 36% | [Report](report/WWTP%20Digester%20Walkway%20Material%20Selection.pdf) | [Benchmark](https://www.kaggle.com/benchmarks/tasks/mehmetisik/wwtp-digester-walkway-material-selection) |
| 6 | Confined Space Emergency Response | Mid | 68% | [Report](report/WWTP%20Confined%20Space%20Emergency%20Response.pdf) | [Benchmark](https://www.kaggle.com/benchmarks/tasks/mehmetisik/wwtp-confined-space-emergency-response) |
| 7 | Sample Preservation Protocol | Easy | 95.5% | [Report](report/WWTP%20Sample%20Preservation%20Protocol.pdf) | [Benchmark](https://www.kaggle.com/benchmarks/tasks/mehmetisik/wwtp-sample-preservation-protocol) |
| 8 | Confined Space Tool Selection | Mid | 68.2% | [Report](report/WWTP%20Confined%20Space%20Tool%20Selection.pdf) | [Benchmark](https://www.kaggle.com/benchmarks/tasks/mehmetisik/wwtp-confined-space-tool-selection) |
| 9 | Activated Sludge Emergency Flocculation | Mid | 68.2% | [Report](report/WWTP%20Activated%20Sludge%20Emergency%20Flocculation.pdf) | [Benchmark](https://www.kaggle.com/benchmarks/tasks/mehmetisik/wwtp-activated-sludge-emergency-flocculation) |
| 10 | SCADA Cabling Standards | Mid | 63.6% | [Report](report/WWTP%20SCADA%20Cabling%20Standards.pdf) | [Benchmark](https://www.kaggle.com/benchmarks/tasks/mehmetisik/wwtp-scada-cabling-standards) |
| 11 | Odor Collection Pipe Material Selection | Hard | 27.3% | [Report](report/WWTP%20Odor%20Collection%20Pipe%20Material%20Selection.pdf) | [Benchmark](https://www.kaggle.com/benchmarks/tasks/mehmetisik/wwtp-odor-collection-pipe-material-selection) |
| 12 | Primary Clarifier Design Criteria | Easy | 86.4% | [Report](report/WWTP%20Primary%20Clarifier%20Design%20Criteria.pdf) | [Benchmark](https://www.kaggle.com/benchmarks/tasks/mehmetisik/wwtp-primary-clarifier-design-criteria) |
| 13 | Emergency Response Sequencing | Mid | 77.3% | [Report](report/WWTP_Sludge_Bulking_LLM_Behavior_Analysis.pdf) | [Benchmark](https://www.kaggle.com/benchmarks/tasks/mehmetisik/wwtp-emergency-response-sequencing-sludge-bulking-crisis) |

---

## Models Tested

22 models across 5 families, tested on the [Kaggle Benchmarks](https://www.kaggle.com/benchmarks/mehmetisik/wwtp-engineering-benchmark) platform with default temperature settings.

| Family | Models |
|:-------|:-------|
| **Claude** (Anthropic) | Haiku 4.5, Sonnet 4, Sonnet 4.5, Opus 4.1, Opus 4.5 |
| **Gemini** (Google) | 2.0 Flash, 2.0 Flash Lite, 2.5 Flash, 2.5 Pro, 3 Flash Preview, 3 Pro Preview |
| **Gemma** (Google) | 3 1B, 3 4B, 3 12B, 3 27B |
| **DeepSeek** | V3.1, V3.2, R1 (Chain-of-Thought) |
| **Qwen** (Alibaba) | 3 235B A22B Instruct, 3 Coder 480B, 3 Next 80B Instruct, 3 Next 80B Thinking |

---

## Methodology

Each benchmark follows the same protocol:

- **Single question, single run per model.** Results are indicative, not absolute.
- **Binary evaluation.** The Kaggle Benchmarks platform extracts the first alphabetic character from each response. Pass or fail, no partial credit.
- **Hedged language throughout.** All reports use phrasing such as "suggests that," "on this task," and "indicative rather than absolute." No definitive claims about model quality are made.
- **Observations, not conclusions.** A single question tested once cannot characterize a model. It can reveal a behavioral pattern worth noting.
- **Platform consistency.** All 13 benchmarks use the same Kaggle Benchmarks platform, the same parser, and the same default temperature settings.

The domain content (wastewater treatment engineering) comprises approximately 10–15% of each report. The remaining 85–90% focuses on LLM behavioral analysis: reasoning patterns, failure modes, family-level trends, and cross-benchmark comparisons.

---

## Repository Structure

```
wwtp-engineering-benchmark/
├── report/                    # 13 individual behavioral analysis reports (PDF)
├── README.md                  # This file
├── CONTRIBUTING.md            # Contribution guidelines
└── LICENSE                    # MIT License
```

---

## Citation

If you reference this work in your research:

```bibtex
@misc{isik2026wwtp-llm-behavioral-analysis,
  author       = {Mehmet ISIK},
  title        = {LLM Behavioral Analysis Through Domain-Specific Engineering Benchmarks: 
                  A 13-Benchmark Study of Reasoning Failures in 22 Large Language Models},
  year         = {2026},
  publisher    = {Kaggle Benchmarks},
  url          = {https://github.com/mmehmetisik/wwtp-engineering-benchmark},
  note         = {13 benchmarks, 22 models, 13 behavioral analysis reports}
}
```

---

## Author

**Mehmet ISIK**

Kaggle Grandmaster | WWTP Operations Engineer | Ceyhan WWTP, Adana, Turkey

- Website: [mehmetisik.dev](https://mehmetisik.dev/)
- LinkedIn: [in/mehmetisik4601](https://www.linkedin.com/in/mehmetisik4601/)
- Kaggle: [@mehmetisik](https://www.kaggle.com/mehmetisik)
- Medium: [@mmehmetisik](https://medium.com/@mmehmetisik)

---

## License

This project is licensed under the MIT License. See [LICENSE](LICENSE) for details.
