# ATLAS Threshold Detection Rules Analysis
> Detection Rule Calibration via FRR / FAR / EER — Data-Driven Cybersecurity (Mattei, Manning 2025) Ch. 8.4–8.5

Author: Patrick Lefler </br>
Published: 2026-07-16 </br>
Rendered: https://patrick-lefler.github.io/rQuarto_ATLAS_detection_rules_analysis_2026-07-16/

## Project Introduction
> ATLAS-based FRR/FAR/EER threshold calibration for detection rules in R/Quarto, framing SOC alert tuning as a documented risk decision for cybersecurity leaders.

## Overview
This report applies the ATLAS (Alert Threshold Lifecycle Assessment System) methodology from *Data-Driven Cybersecurity* (Mattei, Manning 2025) to three detection rules — Brute Force Login, Lateral Movement, and Data Exfiltration. For each rule it computes the False Rejection Rate (FRR), False Acceptance Rate (FAR), and Equal Error Rate (EER) from the current confusion matrix, models the FRR/FAR trade-off curve with a two-Gaussian signal detection model, and issues a plain-language TIGHTEN, LOOSEN, or HOLD recommendation. The intended outcome is a threshold decision a security engineer can act on the same day, backed by a record a risk committee or auditor can actually evaluate.

## Tech Stack
* **Language:** R
* **Framework:** [Quarto](https://quarto.org/)
* **Primary Libraries:** tidyverse (dplyr, ggplot2, tibble), kableExtra, plotly, scales, sessioninfo, cli
* **Deployment/Output:** Self-contained HTML report (`embed-resources: true`)

## Repository Structure
```
├── data/               # Confusion matrix values by detection rule
├── scripts/            # Helper R scripts or utility functions
├── models/             # Saved model objects (.rds), if any
├── output/             # Rendered HTML output
├── _brand.yml          # Brand configuration
├── _quarto.yml         # Project-level Quarto configuration
├── INSTRUCTIONS.md     # Project instructions
└── atlas_threshold_report.qmd   # Main Quarto entry point
```

## Key Findings
- **Brute Force Login — TIGHTEN.** The rule flags roughly 2.5 benign login attempts for every real brute-force attempt it catches (FAR 22.2% vs. FRR 20.0%); raising the failed-attempt threshold recovers analyst capacity without abandoning the signal.
- **Lateral Movement — LOOSEN.** The rule misses close to half of confirmed lateral-movement events (FRR 45.0%) while its FAR sits at just 2.2%, a conservative tuning that leaves a wide detection gap on one of the highest-consequence stages of an intrusion.
- **Data Exfiltration — HOLD.** FRR and FAR are both 10.0%, putting the rule almost exactly at its EER; further improvement requires better detection signal rather than a threshold move.

## License
This project is licensed under the MIT License. See the LICENSE file for details.

## Contact
Patrick Lefler [https://www.linkedin.com/in/patricklefler/] | [patrick-lefler.github.io] | [https://substack.com/@pflefler]
