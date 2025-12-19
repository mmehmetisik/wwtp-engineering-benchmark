# 🏭 WWTP Engineering Benchmark

[![Kaggle](https://img.shields.io/badge/Kaggle-Benchmark-20BEFF?logo=kaggle)](https://www.kaggle.com/benchmarks/mehmetisik/wwtp-engineering-benchmark)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Tasks](https://img.shields.io/badge/Tasks-10-blue)]()
[![Models](https://img.shields.io/badge/Models%20Tested-18-green)]()

**Evaluating LLM capabilities in wastewater treatment plant engineering through real-world scenarios requiring domain expertise, safety awareness, and process chain thinking.**

This benchmark tests knowledge that is typically **NOT found in standard training data** — operational insights derived from 10+ years of hands-on WWTP experience.

---

## 📊 Live Leaderboard

| Rank | Model | Score |
|------|-------|-------|
| 🥇 | Claude Sonnet 4 | **90%** |
| 🥈 | Claude Opus 4.5 | 80% |
| 🥈 | Claude Sonnet 4.5 | 80% |
| 🥈 | Deepseek V3.1 | 80% |
| 🥈 | Gemini 2.5 Pro | 80% |

**[→ View Full Leaderboard on Kaggle](https://www.kaggle.com/benchmarks/mehmetisik/wwtp-engineering-benchmark)**

---

## 🎯 Benchmark Tasks

| # | Task | Category | Difficulty | Pass Rate |
|---|------|----------|------------|-----------|
| 1 | [Biogas Desulfurization Recovery](https://www.kaggle.com/datasets/mehmetisik/wwtp-biogas-desulfurization-recovery) | Process Knowledge | 🔴 Expert | 2/18 |
| 2 | [Activated Sludge Emergency Flocculation](https://www.kaggle.com/datasets/mehmetisik/wwtp-activated-sludge-emergency-flocculation) | Emergency Response | 🟠 Hard | 13/18 |
| 3 | [SCADA Cabling Standards](https://www.kaggle.com/datasets/mehmetisik/wwtp-scada-cabling-standards) | Industrial Standards | 🟠 Hard | 10/18 |
| 4 | [Dewatering System Root Cause](https://www.kaggle.com/datasets/mehmetisik/wwtp-dewatering-system-root-cause) | Root Cause Analysis | 🟡 Medium | 13/18 |
| 5 | [Equipment Material Selection](https://www.kaggle.com/datasets/mehmetisik/wwtp-equipment-material-selection) | Material Selection | 🟢 Easy | 18/18 |
| 6 | [Sample Preservation Protocol](https://www.kaggle.com/datasets/mehmetisik/wwtp-sample-preservation-protocol) | Laboratory | 🟢 Easy | 18/18 |
| 7 | [Root Cause Analysis (Pump)](https://www.kaggle.com/datasets/mehmetisik/wwtp-root-cause-analysis) | Root Cause Analysis | 🟡 Medium | 15/18 |
| 8 | [Digester Walkway Material Selection](https://www.kaggle.com/datasets/mehmetisik/wwtp-digester-walkway-material-selection) | Safety Critical | 🔴 Expert | 5/18 |
| 9 | [Confined Space Tool Selection](https://www.kaggle.com/datasets/mehmetisik/wwtp-confined-space-tool-selection) | Safety Protocol | 🟠 Hard | 11/18 |
| 10 | [Confined Space Emergency Response](https://www.kaggle.com/datasets/mehmetisik/wwtp-confined-space-emergency-response) | Safety Protocol | 🟡 Medium | 16/18 |

---

## 🔍 Key Findings

### 1. The Biogas Trap (2/18 Pass Rate)
Most models chose "Activated Sludge" for bacterial re-inoculation, confusing **aerobic vs anaerobic** processes. The correct answer is anaerobic digester sludge — sulfur-oxidizing bacteria exist where H₂S is produced.

### 2. The Safety Blind Spot (5/18 Pass Rate)
On the walkway material selection task, 13/18 models chose FRP for corrosion resistance, ignoring that FRP is **brittle and fails without warning**. At 15m height, this is a fatal design choice. Safety > Chemical resistance.

### 3. Token Count ≠ Accuracy
DeepSeek-R1 used **4x more tokens** than top performers but scored only **10%**. More reasoning doesn't mean better answers.

### 4. Smaller Can Beat Larger
Claude Sonnet 4 (90%) outperformed Claude Opus 4.5 (80%), proving that model size doesn't guarantee domain expertise.

---

## 📄 Report

📥 **[Download Full Analysis Report (PDF)](./report/WWTP_Benchmark_Report.pdf)**

The report includes:
- Complete results matrix (18 models × 10 tasks)
- Detailed trap analysis
- Token efficiency comparison
- Model family benchmarking
- Recommendations for LLM developers

---

## 🤝 Contributing

Contributions are welcome! You can help by:

1. **Proposing new tasks** — Open an issue with your scenario
2. **Testing additional models** — Run the benchmark and share results
3. **Improving existing tasks** — Suggest refinements via pull requests

See [CONTRIBUTING.md](./CONTRIBUTING.md) for guidelines.

---

## 📖 Citation

If you use this benchmark in your research, please cite:
```bibtex
@misc{wwtp-benchmark-2025,
  author = {Mehmet ISIK},
  title = {WWTP Engineering Benchmark: Evaluating LLM Capabilities in Wastewater Treatment},
  year = {2025},
  publisher = {Kaggle},
  url = {https://www.kaggle.com/benchmarks/mehmetisik/wwtp-engineering-benchmark}
}
```

---

## 👤 Author

**Mehmet ISIK**  
Kaggle Grandmaster | WWTP Operations Expert

- 🏆 Kaggle: [@mehmetisik](https://www.kaggle.com/mehmetisik)
- ✍️ Medium: [@mmehmetisik](https://medium.com/@mmehmetisik)
- 💼 LinkedIn: [Connect](https://www.linkedin.com/in/yourprofile)

---

## 📜 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

<p align="center">
  <b>⭐ Star this repo if you find it useful!</b>
</p>
