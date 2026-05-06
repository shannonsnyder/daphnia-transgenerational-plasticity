# Non-genetic inheritance of induced defense morphologies across multiple unexposed generations of *Daphnia lumholtzi*

**Authors:** Shannon N. Snyder, Walker C. Meyer, Shanie L. Jorgenson, Ethan B. Contreras, Tea Bland, William A. Cresko
**Journal:** Journal of Evolutionary Biology
**Corresponding:** ssnyder3@uoregon.edu | wcresko@uoregon.edu

---

## Overview

This repository contains the data, analysis code, and raw microscopy images for a study examining transgenerational phenotypic plasticity in the clonal water flea *Daphnia lumholtzi*. We exposed a single clonal lineage to fish-conditioned medium in the G0 generation and tracked predator-induced morphological defenses (headspine, tailspine) through G5, measuring whether induced morphologies persist in generations with no direct predator exposure.

**Key finding:** Predator-induced morphological defenses (elongated headspine and tailspine) persisted through G4 — four generations after initial exposure — before regressing to baseline in G5, demonstrating finite-duration non-genetic transgenerational inheritance.

---

## Repository Contents

```
daphnia-transgenerational-plasticity/
├── README.md
├── CITATION.cff
├── LICENSE
├── .gitignore
├── analysis/
│   ├── daphnia-transgenerational-plasticity_analysis.qmd   # Full statistical analysis (Quarto/R)
│   ├── compile_supplementary_pdf.qmd                       # Supplementary materials compilation
│   └── convert_figures_to_jpeg.qmd                         # Figure format conversion
├── data/
│   └── spines_clean_final.csv           # Processed morphometric measurements
├── raw_images/
│   └── *.jpg                            # Raw microscopy photographs (Olympus DP74)
├── figures/
│   ├── Figure1@4x.png                   # Experimental design schematic
│   ├── Figure2.pdf                      # Life-history diagram
│   ├── Figure3–7*.png                   # Main text figures
│   └── FigureS1–S7*.png                # Supplementary figures
├── tables/
│   ├── Table1–4*.docx                   # Main text tables
│   └── SuppTable1–5*.docx              # Supplementary tables
├── docs/
│   ├── ImageJ_instructions.pdf          # Morphometric measurement protocol
│   ├── methods_protocol.md              # Experimental methods
│   └── session_info.txt                 # R session info for reproducibility
└── scripts/
    └── Daphnia-transgenerational-plasticity-analysis.qmd  # Original analysis (pre-revision)
```

---

## Data Description

### Processed data (`data/spines_clean_final.csv`)

| Column | Description |
|--------|-------------|
| `sample` | Individual Daphnia identifier |
| `treatment` | `induced` (fish-conditioned G0) or `control` |
| `age` | Age in days at measurement |
| `generation` | Generation (1=G0, 4=G3, 5=G4, 6=G5) |
| `lifestage` | Developmental stage |
| `headspine` | Headspine length (µm) |
| `bodylength` | Body length (µm) |
| `tailspine` | Tailspine length (µm) |
| `totalbodysize` | Sum of headspine + tailspine + bodylength (µm) |
| `eyediameter` | Eye diameter (µm) |
| `line` | Founding lineage (odd = induced, even = control) |
| `ID` | Unique individual ID |

### Raw microscopy images (`raw_images/`)

Digital photographs of individual *Daphnia lumholtzi* captured using an Olympus DP74 camera mounted on a dissecting microscope. Images were analyzed in ImageJ to obtain morphometric measurements (headspine, tailspine, body length, eye diameter). See `docs/ImageJ_instructions.pdf` for the measurement protocol.

**File naming convention:** `{line}.{sample}_day{N}.jpg`

- `line`: Founding lineage number (odd = induced treatment, even = control)
- `sample`: Individual identifier within lineage
- `day{N}`: Age in days at time of photograph

Example: `001.001_day5.jpg` = Lineage 1, individual 1, photographed on day 5.

Files prefixed `000.000_` are calibration/reference images.

---

## Reproducing the Analysis

### Requirements

- R ≥ 4.3
- Quarto ≥ 1.4
- Key R packages: `brms`, `lme4`, `lmerTest`, `tidyverse`, `ggplot2`, `patchwork`, `ggpubr`, `kableExtra`, `flextable`, `officer`, `emmeans`, `mgcv`, `bayesplot`, `performance`, `pwr`

### Running

```r
# Install required packages if needed
install.packages(c("brms", "lme4", "lmerTest", "broom.mixed", "performance",
                   "ggpubr", "RColorBrewer", "patchwork", "knitr", "kableExtra",
                   "emmeans", "multcomp", "flextable", "officer", "tidyverse",
                   "mgcv", "bayesplot", "Rmisc", "pwr"))
```

```bash
cd analysis/
quarto render daphnia-transgenerational-plasticity_analysis.qmd
```

Bayesian models are cached in `models/` after first run (excluded from version control due to file size). Delete `.rds` files to force re-fitting.

---

## Experimental Design

- **Clone:** Single *D. lumholtzi* genetic background (Saguaro Lake, AZ, collected 2019)
- **G0 treatment:** 5 lineages exposed to fish-conditioned medium; 4 control lineages
- **G1–G5:** All reared in control medium (no predator cue)
- **Generations measured:** G0, G3, G4, G5
- **Morphometrics:** Headspine, tailspine, body length (µm), measured every other day via ImageJ from digital photographs (Olympus DP74 microscope camera)

G3 is the first generation with no embryonic or germline exposure, making G3–G5 the critical window for detecting true transgenerational (non-genetic) inheritance.

---

## Statistical Approach

**Primary analysis:** Bayesian hierarchical models (`brms`) fit per generation:
- Spines: `spine ~ treatment + bodylength + (1|sample)`
- Body length: `bodylength ~ treatment + headspine + tailspine + (1|sample)`

**Validation:** Frequentist linear mixed-effects models (`lme4`) with identical structure.

**Secondary analyses:** Growth rate trajectories (Δ per timepoint), survivorship (binomial GLM), size-selective mortality (LOESS trajectories by survival status), retrospective power analysis for G5 (Cohen's d from linear model estimates with `pwr`).

---

## Data Availability

All data and code are archived on Zenodo with a persistent DOI (see CITATION.cff). The raw microscopy images used for ImageJ measurements are included in `raw_images/`. This GitHub repository is linked to Zenodo for long-term archival access.

---

## Citation

Snyder SN, Meyer WC, Jorgenson SL, Contreras EB, Bland T, Cresko WA. Non-genetic inheritance of induced defense morphologies across multiple unexposed generations of *Daphnia lumholtzi*. *Journal of Experimental Biology*.

---

## License

Data and code are made available for reproducibility of the associated manuscript. Please cite the paper if you use these materials.
