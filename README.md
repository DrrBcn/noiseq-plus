# NoiseQ+ — Road Traffic Noise Health Impact Assessment Tool

**Version 4.0** · June 2026

NoiseQ+ is a free, open-source web tool for estimating the population health burden of road traffic noise. It applies the WHO comparative risk assessment methodology — the same framework used by AirQ+ for air pollution — to environmental noise.

Version 4.0 aligns the tool's parameters with the published national assessment: Rojas-Rueda D. *Health burden of transportation noise in the United States: a national assessment with equity analysis.* Environmental Research, 2026. doi:[10.1016/j.envres.2026.124921](https://doi.org/10.1016/j.envres.2026.124921).

## Quick Start

1. Download `index.html`
2. Open it in any modern browser (Chrome, Firefox, Safari, Edge)
3. Follow the 6-step guided workflow

No installation, server, or dependencies required. The entire tool runs in a single HTML file.

## Live Demo

Visit: **[https://drrbcn.github.io/noiseq-plus/](https://drrbcn.github.io/noiseq-plus/)**

## What It Does

NoiseQ+ estimates the number of health cases and deaths attributable to road traffic noise exposure in a defined population, including:

| Health Outcome | Method | Evidence Source |
|---|---|---|
| Ischemic heart disease | PAF (RR 1.08/10 dB) | van Kempen et al. 2018 (WHO ENG, HIGH quality) |
| Stroke | PAF (RR 1.025/10 dB) | Pershagen et al. 2025 |
| Heart failure | PAF (RR 1.04/10 dB) | Engelmann et al. 2023 (ETC/HE Report 2023/11, Umbrella+ review) |
| Type 2 diabetes | PAF (RR 1.07/10 dB) | Vienneau et al. 2024 |
| Cardiovascular mortality (YLL) | PAF (RR 1.05/10 dB) | Münzel et al. 2024 |
| High annoyance | ERF polynomial | Guski et al. 2017 (WHO ENG) |
| High sleep disturbance | ERF polynomial | Smith et al. 2022 (updates Basner & McGuire 2018) |

The tool produces:

- Attributable cases and deaths per year with 95% uncertainty intervals
- Population Attributable Fractions (PAF)
- Disability-Adjusted Life Years (DALYs), split into years lived with disability (YLD) for morbidity and years of life lost (YLL) for cardiovascular mortality
- Built-in sensitivity analysis (counterfactual levels, disability weight sets, IHD relative risk alternatives)
- CSV data export

## Required Inputs

At minimum, users need:

- **Population size** (adults ≥30 for cardiovascular and diabetes outcomes, ≥18 for annoyance/sleep)
- **Noise exposure distribution** — percentage of population in each 5 dB Lden band from 45 to 75+ dB (available from strategic noise mapping under the EU Environmental Noise Directive or local noise studies)

Optional inputs allow customization of baseline disease and mortality rates, counterfactual noise level, and Lden-to-Lnight conversion offset.

## Methodology

NoiseQ+ implements two standard HIA calculation approaches:

**For cardiovascular, metabolic, and mortality outcomes (PAF method):**

```
RR(Lden) = RR_per10dB ^ ((Lden_midpoint − counterfactual) / 10)
PAF = Σ[Pi × (RRi − 1)] / {Σ[Pi × (RRi − 1)] + 1}
Attributable Cases = PAF × Baseline Rate × Population / 100,000
```

**For annoyance and sleep disturbance (ERF method):**

```
%HA  = 78.9270 − 3.1162 × Lden + 0.0342 × Lden²       (Lden 45–75 dB)
%HSD = 31.18323 − 1.47351 × Lnight + 0.01851 × Lnight²  (Lnight 40–65 dB)
```

The sleep function is from Smith et al. 2022, which updates the Basner & McGuire 2018 WHO function (adopted in EU Directive 2020/367 Annex III) with 11 additional studies.

DALYs use WHO 2024 empirically derived disability weights (Charalampous et al., BMJ Public Health, 2024). Morbidity outcomes contribute YLD (attributable cases × disability weight × duration). Cardiovascular mortality contributes YLL (attributable deaths × 14.5 years remaining life expectancy).

Full methodological details, including all formulas, parameter sources, dose-response curves, and limitations, are presented on the tool's Methods page.

## Default Baseline Rates

Baseline rates for ischemic heart disease, stroke, and heart failure are approximate global GBD estimates. Default rates for **type 2 diabetes (735/100,000)** and **cardiovascular mortality (480/100,000)** are US national means from the published assessment and should be replaced with local rates for non-US settings. All baseline rates are user-editable in the tool.

## Key Features

- **Single HTML file** — no server, no build step, no dependencies to install
- **Guided 6-step workflow** — designed for urban planners and public health practitioners, not just epidemiologists
- **Mortality (YLL) module** — cardiovascular mortality now contributes years of life lost, alongside morbidity YLD
- **Built-in sensitivity analysis** — tests counterfactual levels (45–55 dB), disability weight generations (WHO 2024, RIVM 2018, WHO 2011), and IHD relative risk alternatives (WHO 2018 vs. Pershagen 2025)
- **Transparent methodology** — all formulas, sources, and limitations visible within the tool
- **CSV export** — download results for further analysis
- **Print-ready** — clean print layout for PDF reports

## Limitations

- Dose-response functions are derived primarily from European populations. Applicability to other regions has not been fully established.
- Heart failure is estimated from a cardiomyopathy-based relative risk used as a conservative proxy, which underestimates clinical heart failure incidence.
- Most cardiovascular studies did not fully adjust for air pollution co-exposure.
- Road traffic noise only. Railway, aircraft, and industrial noise require source-specific functions.
- When Lnight data are not available, a fixed Lden-to-Lnight offset is applied (default −9 dB), which may not reflect local traffic patterns.

## Deploying on GitHub Pages

1. Create a new repository (e.g., `noiseq-plus`)
2. Upload `index.html` to the repository root
3. Go to Settings → Pages → Source: Deploy from branch → Branch: `main`, folder: `/ (root)`
4. Your tool will be live at `https://yourusername.github.io/noiseq-plus/`

## Citation

Rojas-Rueda D. NoiseQ+: Road Traffic Noise Health Impact Assessment Tool, version 4.0. Colorado State University / Habitat Analytics LLC; 2026. Available at: https://github.com/DrrBcn/noiseq-plus

Parameters aligned with: Rojas-Rueda D. Health burden of transportation noise in the United States: a national assessment with equity analysis. *Environmental Research.* 2026. doi:10.1016/j.envres.2026.124921

## Author

**David Rojas-Rueda, MD, PhD, MPH**
Associate Professor, Department of Environmental and Radiological Health Sciences
Colorado State University
Principal, Habitat Analytics LLC

## License

This tool is provided under the MIT License. You are free to use, modify, and distribute it with attribution.


