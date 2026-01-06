# Analysis of HUD Fair Market Rent Benchmarks

**Rental Market Pressure Across U.S. Metropolitan Areas**  
*An Analytics-Ready Lakehouse Pipeline Using HUD FMR Data*

---

## Table of Contents
- [Introduction](#introduction)
- [Research Focus](#research-focus)
- [Data Source](#data-source)
- [Key Visuals & Insights](#key-visuals--insights)
- [Methodology](#methodology)
- [Findings](#findings)
- [Limitations and Future Extensions](#limitations-and-future-extensions)
- [Conclusion](#conclusion)
- [References](#references)

---

## Introduction

Fair Market Rents (FMRs) are estimates produced annually by the U.S. Department of Housing and Urban Development (HUD) that represent typical rents for standard-quality rental housing units within a specified metropolitan or non-metropolitan area. FMRs are defined as the rent level below which 40% of gross rents fall, measured using recent rental data across local markets. These benchmarks are used in multiple federal housing programs, including Section 8 housing assistance payment standards and rent ceilings for assisted units.  [oai_citation:0‡huduser.gov](https://www.huduser.gov/portal/datasets/fmr.html?utm_source=chatgpt.com)

This project ingests HUD FMR data via API, structures it through a bronze–silver–gold lakehouse, and produces analytics-ready datasets. Instead of focusing on household income or eviction outcomes, it examines **variation in rental benchmarks across unit types and metropolitan areas** as a measure of rental market pressure.

---

## Research Focus

This analysis addresses:

- How do HUD Fair Market Rent benchmarks vary across metropolitan areas?
- How does rent pressure differ by bedroom category?
- Which regions exhibit unusually high or widely dispersed rents?

The focus on rent benchmarks alone reflects what the available data can support directly without household income or eviction records.

---

## Data Source

### HUD Fair Market Rent (FMR)
- **Agency:** U.S. Department of Housing and Urban Development  
- **Description:** Annual estimates of gross rents (rent + utilities) for standard quality units by bedroom size in metropolitan and non-metropolitan areas. FMRs are calculated at the 40th percentile of gross rent distribution in a given geography.  [oai_citation:1‡huduser.gov](https://www.huduser.gov/portal/datasets/fmr.html?utm_source=chatgpt.com)  
- **API Documentation:** https://www.huduser.gov/portal/dataset/fmr-api.html  [oai_citation:2‡huduser.gov](https://www.huduser.gov/portal/dataset/fmr-api.html?utm_source=chatgpt.com)

---

## Key Visuals & Insights

These visuals illustrate core patterns in HUD Fair Market Rent benchmarks:

### 1. **Rent Distribution by Bedroom Size**

A box plot showing distributions of FMR values by bedroom count reveals:
- Median rent increases with unit size
- Variability grows with larger units
This highlights where rental market pressure is most pronounced.

**Interpretation:** Rental cost variability alone, before considering income, signals differences in housing pressure across unit types and metros.

---

### 2. **Top-Tier Markets for 2-Bedroom Rents**

Listing metropolitan areas with the highest 2-bedroom FMRs helps identify markets where benchmark rents are most elevated. For example, metros in high-cost regions appear in the upper tail of the distribution.

---

### 3. **State-Level Average FMRs**

Aggregating FMRs by state for a given bedroom category (e.g., 2BR) reveals broad geographic differences in rental markets, offering insight into regional rent pressures.

---

## Methodology

This project uses a **bronze–silver–gold** data architecture in Databricks:

### Bronze Layer
- Raw ingestion from HUD FMR API
- JSON payloads stored as-is with ingestion metadata

### Silver Layer
- Parsed JSON into structured fields
- Normalized rent benchmarks for each bedroom type
- Quarantined rows with invalid or missing rents

### Gold Layer
- Star schema with:
  - Geography dimension (metro, state)
  - Bedroom dimension (0–4 bedrooms)
  - Time dimension (program year)
  - Fact table of FMR values
- Dashboard-ready serving table for visual analysis

This approach reflects common practice in housing analytics workflows.

---

## Findings

- **Rent benchmarks increase with bedroom size.** Median and upper values of FMR rise as unit size grows, indicating larger units command higher rents on average.
- **Greater variability for larger units.** Dispersion in FMR values is wider for 3BR and 4BR units compared with studios and 1BR units.
- **Geographic variation is substantial.** Average FMR values differ significantly across metropolitan areas and states, suggesting uneven rent pressure nationwide.

These findings describe how rental benchmarks vary across space and unit type; they do not make claims about individual affordability or eviction risk absent income data.

---

## Limitations and Future Extensions

### Limitations
- The analysis does not incorporate household income or affordability measures.
- Eviction outcomes are not linked to rent benchmarks.
- FMRs are annual benchmarks and may lag rapid rent changes.

### Future Extensions
- Incorporate American Community Survey income estimates for rent-to-income comparisons.
- Join eviction filing records for outcome analysis.
- Enhance spatial precision using Small Area FMR (SAFMR) by ZIP code.  [oai_citation:3‡huduser.gov](https://www.huduser.gov/portal/datasets/fmr/smallarea/index.html?utm_source=chatgpt.com)

---

## Conclusion

This project builds an analytics foundation for understanding rental market pressure through HUD Fair Market Rent benchmarks. With a structured lakehouse approach, it provides clean, interpretable datasets and visual summaries of how rents vary by geography and unit type.

These outputs can support housing market monitoring and inform program discussions, even without income or eviction data.

---

## References

- HUD Fair Market Rents dataset documentation  
  https://www.huduser.gov/portal/datasets/fmr.html  [oai_citation:4‡huduser.gov](https://www.huduser.gov/portal/datasets/fmr.html?utm_source=chatgpt.com)

- HUD Fair Market Rent explanation (HUD Exchange)  
  https://www.hudexchange.info/homelessness-assistance/coc-esg-virtual-binders/coc-leasing-rental-assistance-requirements/fmr/  [oai_citation:5‡HUD Exchange](https://www.hudexchange.info/homelessness-assistance/coc-esg-virtual-binders/coc-leasing-rental-assistance-requirements/fmr/?utm_source=chatgpt.com)

- HUD FMR calculation methodology  
  https://www.huduser.gov/portal/datasets/fmr/fmr2026/FY26-Public-FMR-Methodology.pdf  [oai_citation:6‡huduser.gov](https://www.huduser.gov/portal/datasets/fmr/fmr2026/FY26-Public-FMR-Methodology.pdf?utm_source=chatgpt.com)

- HUD FMR API documentation  
  https://www.huduser.gov/portal/dataset/fmr-api.html  [oai_citation:7‡huduser.gov](https://www.huduser.gov/portal/dataset/fmr-api.html?utm_source=chatgpt.com)

- Small Area Fair Market Rents (SAFMR) system  
  https://www.huduser.gov/portal/datasets/fmr/smallarea/index.html  [oai_citation:8‡huduser.gov](https://www.huduser.gov/portal/datasets/fmr/smallarea/index.html?utm_source=chatgpt.com)
