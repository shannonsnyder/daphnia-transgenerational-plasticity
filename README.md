# daphnia-transgenerational-plasticity
Predator-induced morphological defenses persist across four generations in genetically identical Daphnia lumholtzi

# Predator-Induced Transgenerational Plasticity in *Daphnia lumholtzi*

[![DOI](https://zenodo.org/badge/DOI/10.5061/dryad.your-doi.svg)](https://doi.org/10.5061/dryad.your-doi)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

## Overview

This repository contains data, code, and analyses for the manuscript "Predator induced phenotypes are inherited over four generations in genetically identical *Daphnia lumholtzi*" by Shannon N. Snyder.

**Abstract:** Predator-induced morphological defenses in *Daphnia lumholtzi* can persist across multiple generations through non-genetic mechanisms. Using clonal lineages exposed to fish-conditioned medium only in the F0 generation, we tracked headspine and tailspine morphology through F5. Induced traits persisted through F4 before regressing in F5, highlighting the transient nature of transgenerational plasticity.

## Repository Contents

- **`data/`** - Raw and processed morphometric measurements
- **`scripts/`** - R scripts for data analysis and visualization  
- **`manuscript/`** - Quarto manuscript and supplementary materials
- **`output/`** - Generated figures, tables, and model objects
- **`docs/`** - Documentation and protocols

## Key Findings

- Predator-induced headspine and tailspine defenses persist for 4 generations
- Transgenerational effects diminish by F5 generation
- No evidence of size-selective mortality confounding results
- Bayesian and frequentist analyses yield consistent results

## Reproducibility

### Requirements

- R version 4.3+
- Key packages: `brms`, `lme4`, `ggplot2`, `dplyr`, `quarto`

### Running the Analysis

1. Clone this repository:
   ```bash
   git clone https://github.com/shannonsnyder/daphnia-transgenerational-plasticity.git
   cd daphnia-transgenerational-plasticity