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

Fair Market Rents (FMRs) are estimates produced annually by the U.S. Department of Housing and Urban Development (HUD) that represent typical rents for standard-quality rental housing units within a specified metropolitan or non-metropolitan area. FMRs are defined as the rent level below which 40% of gross rents fall, measured using recent rental data across local markets. These benchmarks are used in multiple federal housing programs, including Section 8 housing assistance payment standards and rent ceilings for assisted units.  [oai_citation:0‡huduser.gov](https://www.huduser.gov/portal/datasets/fmr.html)

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
- **Description:** Annual estimates of gross rents (rent + utilities) for standard quality units by bedroom size in metropolitan and non-metropolitan areas. FMRs are calculated at the 40th percentile of gross rent distribution in a given geography.  [oai_citation:1‡huduser.gov](https://www.huduser.gov/portal/datasets/fmr.html)  
- **API Documentation:** https://www.huduser.gov/portal/dataset/fmr-api.html  [oai_citation:2‡huduser.gov](https://www.huduser.gov/portal/dataset/fmr-api.html)

---

## Key Visuals & Insights

These visuals illustrate core patterns in HUD Fair Market Rent benchmarks:

### 1. **Rent Distribution by Bedroom Size**

A  plot showing distributions of FMR values by bedroom count reveals:
- Median rent increases with unit size
- Variability grows with larger units
This highlights where rental market pressure is most pronounced.

<img width="410" height="242" alt="Screenshot 2026-01-06 at 1 57 35 AM" src="https://github.com/user-attachments/assets/426650e3-c434-4497-bc49-3bc8fe409f61" />

<img width="714" height="462" alt="Screenshot 2026-01-06 at 1 57 23 AM" src="https://github.com/user-attachments/assets/0b639dd4-d803-4b09-b517-a8a65faa8432" />

**Interpretation:** Rental cost variability alone, before considering income, signals differences in housing pressure across unit types and metros.

---

### 2. **Top-Tier Markets for 2-Bedroom Rents**

To highlight markets with the highest rental pressure, we examine the top decile of metropolitan areas by Fair Market Rent for 2-bedroom units. Focusing on the 75th percentile and above reveals metros where benchmark rents are most elevated relative to the national distribution.

<img width="759" height="456" alt="Screenshot 2026-01-06 at 3 42 25 AM" src="https://github.com/user-attachments/assets/f4139812-2b63-414e-8172-c63c696eafb8" />



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
- Enhance spatial precision using Small Area FMR (SAFMR) by ZIP code.  [oai_citation:3‡huduser.gov](https://www.huduser.gov/portal/datasets/fmr/smallarea/index.html)

---

## Conclusion

This project builds an analytics foundation for understanding rental market pressure through HUD Fair Market Rent benchmarks. With a structured lakehouse approach, it provides clean, interpretable datasets and visual summaries of how rents vary by geography and unit type.

These outputs can support housing market monitoring and inform program discussions, even without income or eviction data.

---

## References

- HUD Fair Market Rents dataset documentation  
  https://www.huduser.gov/portal/datasets/fmr.html  [oai_citation:4‡huduser.gov](https://www.huduser.gov/portal/datasets/fmr.html)

- HUD Fair Market Rent explanation (HUD Exchange)  
  https://www.hudexchange.info/homelessness-assistance/coc-esg-virtual-binders/coc-leasing-rental-assistance-requirements/fmr/  [oai_citation:5‡HUD Exchange](https://www.hudexchange.info/homelessness-assistance/coc-esg-virtual-binders/coc-leasing-rental-assistance-requirements/fmr/)

- HUD FMR calculation methodology  
  https://www.huduser.gov/portal/datasets/fmr/fmr2026/FY26-Public-FMR-Methodology.pdf  [oai_citation:6‡huduser.gov](https://www.huduser.gov/portal/datasets/fmr/fmr2026/FY26-Public-FMR-Methodology.pdf?utm)

- HUD FMR API documentation  
  https://www.huduser.gov/portal/dataset/fmr-api.html  [oai_citation:7‡huduser.gov](https://www.huduser.gov/portal/dataset/fmr-api.html)

- Small Area Fair Market Rents (SAFMR) system  
  https://www.huduser.gov/portal/datasets/fmr/smallarea/index.html  [oai_citation:8‡huduser.gov](https://www.huduser.gov/portal/datasets/fmr/smallarea/index.html)
