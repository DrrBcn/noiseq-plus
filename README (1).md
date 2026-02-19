# NoiseQ+ — Road Traffic Noise Health Impact Assessment Tool

**Version 3.0** · February 2026

NoiseQ+ is a free, open-source web tool for estimating the population health burden of road traffic noise. It applies the WHO comparative risk assessment methodology — the same framework used by AirQ+ for air pollution — to environmental noise.

## Quick Start

1. Download `index.html`
2. Open it in any modern browser (Chrome, Firefox, Safari, Edge)
3. Follow the 6-step guided workflow

No installation, server, or dependencies required. The entire tool runs in a single HTML file.

## Live Demo

Visit: **https://drojas-rueda.github.io/noiseq-plus/**

## What It Does

NoiseQ+ estimates the number of health cases attributable to road traffic noise exposure in a defined population, including:

| Health Outcome | Method | Evidence Source |
|---|---|---|
| Ischemic heart disease | PAF (RR 1.08/10 dB) | van Kempen et al. 2018 (WHO ENG, HIGH quality) |
| Stroke | PAF (RR 1.025/10 dB) | Pershagen et al. 2025 |
| Heart failure | PAF (RR 1.04/10 dB) | Sørensen et al. 2024 (Umbrella+ Review) |
| High annoyance | ERF polynomial | Guski et al. 2017 (WHO ENG) |
| High sleep disturbance | ERF polynomial | Miedema & Vos 2007 (EU Directive 2020/367) |

The tool produces:

- Attributable cases per year with 95% uncertainty intervals
- Population Attributable Fractions (PAF)
- Disability-Adjusted Life Years (DALYs) using WHO 2024 disability weights
- Built-in sensitivity analysis (counterfactual levels, disability weight sets, IHD relative risk alternatives)
- CSV data export

## Required Inputs

At minimum, users need:

- **Population size** (adults ≥30 for CVD, ≥18 for annoyance/sleep)
- **Noise exposure distribution** — percentage of population in each 5 dB Lden band from 45 to 75+ dB (available from strategic noise mapping under the EU Environmental Noise Directive or local noise studies)

Optional inputs allow customization of baseline disease rates, counterfactual noise level, and Lden-to-Lnight conversion offset.

## Methodology

NoiseQ+ implements two standard HIA calculation approaches:

**For cardiovascular outcomes (PAF method):**

```
RR(Lden) = RR_per10dB ^ ((Lden_midpoint − counterfactual) / 10)
PAF = Σ[Pi × (RRi − 1)] / {Σ[Pi × (RRi − 1)] + 1}
Attributable Cases = PAF × Baseline Incidence Rate × Population / 100,000
```

**For annoyance and sleep disturbance (ERF method):**

```
%HA = 78.9270 − 3.1162 × Lden + 0.0342 × Lden²   (Lden 45–75 dB)
%HSD = 20.8 − 1.05 × Lnight + 0.01486 × Lnight²   (Lnight 40–65 dB)
```

DALYs are calculated using WHO 2024 empirically derived disability weights (Charalampous et al., BMJ Public Health, 2024). CVD DALYs represent YLD only (years lived with disability); premature mortality (YLL) is not included in this version.

Full methodological details, including all formulas, parameter sources, dose-response curves, and limitations, are presented on the tool's Methods page.

## Key Features

- **Single HTML file** — no server, no build step, no dependencies to install
- **Guided 6-step workflow** — designed for urban planners and public health practitioners, not just epidemiologists
- **Built-in sensitivity analysis** — tests counterfactual levels (45–55 dB), disability weight generations (WHO 2024, RIVM 2018, WHO 2011), and IHD relative risk alternatives (WHO 2018 vs. Pershagen 2025)
- **Transparent methodology** — all formulas, sources, and limitations visible within the tool
- **CSV export** — download results for further analysis
- **Print-ready** — clean print layout for PDF reports

## Limitations

- Dose-response functions are derived primarily from European populations. Applicability to other regions has not been fully established.
- CVD DALYs are YLD-only (conservative lower bound). A YLL module for premature mortality is planned.
- Cardiovascular studies did not fully adjust for air pollution co-exposure.
- Road traffic noise only. Railway, aircraft, and industrial noise require source-specific functions.
- When Lnight data are not available, a fixed Lden-to-Lnight offset is applied (default −9 dB), which may not reflect local traffic patterns.

## Deploying on GitHub Pages

1. Create a new repository (e.g., `noiseq-plus`)
2. Upload `index.html` to the repository root
3. Go to Settings → Pages → Source: Deploy from branch → Branch: `main`, folder: `/ (root)`
4. Your tool will be live at `https://yourusername.github.io/noiseq-plus/`

## Citation

Rojas-Rueda D. NoiseQ+: Road Traffic Noise Health Impact Assessment Tool, version 3.0. Colorado State University / Habitat Analytics LLC; 2026. Available at: https://github.com/drojas-rueda/noiseq-plus

## Related Publications

- **Methods paper** (in preparation): "NoiseQ+: A standardized web-based tool for quantifying the population health burden of road traffic noise — Methods and validation"
- **Application paper** (planned): Multi-city application across income levels

## Author

**David Rojas-Rueda, MD, PhD, MPH**
Associate Professor, Department of Environmental and Radiological Health Sciences
Colorado State University
Principal, Habitat Analytics LLC

## License

This tool is provided under the MIT License. You are free to use, modify, and distribute it with attribution.

## Version History

| Version | Date | Changes |
|---|---|---|
| v3.0 | 2026-02-18 | Corrected sleep ERF source attribution (Miedema & Vos 2007). Added outcome-specific CVD disability weights. Added heart failure as default outcome. Added IHD RR sensitivity analysis. Added Lnight offset control. Added CSV export. Fixed sleep DW lower bound. Corrected all citations. |
| v2.2 | 2025 | Added DW preset selector, sensitivity analysis page, improved UI. |
| v2.1 | 2025 | Added stroke and heart failure outcomes, updated to Pershagen 2025 and Sørensen 2024. |
| v1.0 | 2025 | Initial prototype with IHD, annoyance, sleep disturbance. |
