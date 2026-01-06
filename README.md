# Analysis Using HUD Fair Market Rent Data

**Housing Affordability, Income, and Evictions**  
*A Lakehouse Analysis Using HUD Fair Market Rent (FMR) Data*

---

## Table of Contents
- [Introduction](#introduction)
- [Research Question](#research-question)
- [Data Sources](#data-sources)
- [Methodology](#methodology)
- [Income, Rent Burden, and Evictions](#income-rent-burden-and-evictions)
- [Findings](#findings)
- [Limitations and Future Work](#limitations-and-future-work)
- [Conclusion](#conclusion)
- [References](#references)

---

## Introduction

Housing affordability has become a central policy challenge across the United States. Rising rents, stagnant wages, and uneven economic recovery have increased housing insecurity for low-income households. One of the most severe outcomes of housing instability is eviction, which carries long-term consequences for individuals, families, and communities.

This project examines the relationship between income, housing costs, and eviction pressure by integrating multiple public datasets into a Databricks-style lakehouse architecture. The goal is to evaluate whether areas with lower income, particularly where benchmark rents are high relative to earnings, experience higher eviction risk.

The workflow mirrors how housing agencies and public-sector analytics teams operate in practice: ingesting authoritative data sources, enforcing data quality rules, and producing analytics-ready datasets for policy analysis and decision-making.

---

## Research Question

Is there a relationship between income and evictions, and how does rent burden, measured using HUD Fair Market Rent, influence that relationship?

More specifically:
- Do lower-income areas experience higher eviction rates?
- Does high Fair Market Rent relative to income correlate with increased eviction pressure?

---

## Data Sources

All datasets used in this project are publicly available and widely used by housing researchers and government agencies.

### HUD Fair Market Rent (FMR)
- Source: U.S. Department of Housing and Urban Development
- Description: Annual Fair Market Rent estimates used to administer federal housing assistance programs
- API: https://www.huduser.gov/portal/dataset/fmr-api.html

### Eviction Data
- Source: NYC Open Data (or comparable local eviction filings dataset)
- Description: Court-ordered residential eviction records
- Dataset: https://data.cityofnewyork.us/City-Government/Evictions/6z8x-wfk4

### Income Data
- Source: U.S. Census Bureau, American Community Survey (ACS)
- Description: Median household income estimates
- ACS API Documentation: https://www.census.gov/data/developers/data-sets/acs-5year.html
- Census API Guide: https://www.census.gov/data/developers/guidance/api-user-guide.html

### Geographic Reference Data
- Source: Census ZIP Code Tabulation Areas (ZCTA)
- Description: Geographic boundaries used to align income and eviction data
- Reference: https://www.census.gov/programs-surveys/geography/guidance/geo-areas/zctas.html

---

## Methodology

The project is implemented using a **Bronze / Silver / Gold** lakehouse architecture in Databricks.

### Bronze Layer
- Raw ingestion of HUD FMR API responses
- Raw eviction filing records
- Raw ACS income estimates
- No transformations applied; original schemas preserved

### Silver Layer
- Parsed and flattened JSON structures
- Standardized geographic identifiers
- Normalized rent values by bedroom type
- Data quality checks applied (null handling, invalid values quarantined)

### Gold Layer
- Analytics-ready fact tables
- Joined income, rent, and eviction metrics by geography
- Optimized for SQL analysis, dashboards, and notebook-based visualization

---

## Income, Rent Burden, and Evictions

Eviction risk cannot be understood through eviction counts alone. Housing affordability depends on the relationship between income and expected rent levels.

HUD Fair Market Rent provides a standardized benchmark for typical rents within a given geography. When FMR consumes a large share of median household income, households become more vulnerable to economic shocks, missed payments, and eventual eviction.

The analysis follows three steps:
1. Analyze eviction patterns across geographic areas
2. Compare median household income across the same geographies
3. Measure rent burden by evaluating FMR relative to income

Bringing these measures together allows eviction pressure to be evaluated as a function of income, rent levels, and their interaction.

---

## Findings

Key observations from the analysis include:
- Areas with lower median household income tend to experience higher eviction counts
- Regions where Fair Market Rent represents a larger share of income show elevated eviction pressure
- A negative correlation is observed between income and eviction activity, consistent with prior housing research
- Rent burden appears to amplify eviction risk beyond income alone

---

## Limitations and Future Work

### Limitations
- Eviction data availability and completeness vary by jurisdiction
- Income estimates are survey-based and may lag current economic conditions
- The analysis identifies correlation, not causation

### Future Work
- Normalize eviction counts by renter population
- Incorporate multi-year data to evaluate trends over time
- Analyze the effects of eviction moratoria and rental assistance programs

---

## Conclusion

The analysis supports the conclusion that income and housing costs are strongly associated with eviction outcomes. When rents increase faster than incomes, eviction risk rises, particularly in economically vulnerable communities.

By integrating HUD Fair Market Rent, Census income data, and eviction records into a unified lakehouse platform, this project demonstrates how public data can be transformed into actionable insights for housing policy, program design, and resource allocation.

---

## References
- HUD Fair Market Rent API  
  https://www.huduser.gov/portal/dataset/fmr-api.html
- NYC Open Data – Evictions  
  https://data.cityofnewyork.us/City-Government/Evictions/6z8x-wfk4
- U.S. Census Bureau – American Community Survey  
  https://www.census.gov/programs-surveys/acs
- Census API User Guide  
  https://www.census.gov/data/developers/guidance/api-user-guide.html
- HUD Housing Affordability Research  
  https://www.huduser.gov/portal/pdredge/pdr_edge_housing_market.html
