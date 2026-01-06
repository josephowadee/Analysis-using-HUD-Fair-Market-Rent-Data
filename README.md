# Analysis-using-HUD-Fair-Market-Rent-Data

Housing Affordability, Income, and Evictions

A Lakehouse Analysis using HUD Fair Market Rent Data

⸻

Table of Contents
	•	Introduction￼
	•	Research Question￼
	•	Data Sources￼
	•	Methodology￼
	•	Story: Income, Rent Burden, and Evictions￼
	•	Findings￼
	•	Limitations and Future Work￼
	•	Conclusion￼
	•	References￼

⸻

Introduction

Housing affordability has become a growing policy concern across the United States. Rising rents, stagnant wages, and uneven economic recovery have increased housing insecurity for low-income households. One of the most severe outcomes of housing instability is eviction, which has long-term consequences for individuals, families, and communities.

This project explores the relationship between income, housing costs, and eviction pressure by integrating multiple public datasets into a Databricks-based lakehouse architecture. The goal is to determine whether areas with lower income — particularly when benchmark rents are high relative to earnings — experience higher eviction risk.

The analysis mirrors real-world workflows used by housing agencies and public policy teams: ingesting authoritative datasets, enforcing data quality rules, and producing analytics-ready outputs for decision-making.

⸻

Research Question

Is there a relationship between income and evictions, and how does rent burden (as measured by HUD Fair Market Rent) influence that relationship?

More specifically:
	•	Do lower-income areas experience higher eviction rates?
	•	Does high Fair Market Rent relative to income correlate with greater eviction pressure?

⸻

Data Sources

All datasets used in this project are publicly available and widely used by housing researchers and government agencies.

HUD Fair Market Rent (FMR)
	•	Source: U.S. Department of Housing and Urban Development
	•	Description: Annual Fair Market Rent estimates used for housing assistance programs
	•	URL:
https://www.huduser.gov/portal/dataset/fmr-api.html

⸻

Eviction Data
	•	Source: NYC Open Data (or equivalent local eviction filings dataset)
	•	Description: Court-ordered residential eviction records
	•	URL:
https://data.cityofnewyork.us/City-Government/Evictions/6z8x-wfk4

⸻

Income Data
	•	Source: U.S. Census Bureau, American Community Survey (ACS)
	•	Description: Median household income estimates
	•	ACS API Documentation:
https://www.census.gov/data/developers/data-sets/acs-5year.html
	•	Census API Guide:
https://www.census.gov/data/developers/guidance/api-user-guide.html

⸻

Geographic Reference Data
	•	Source: Census ZIP Code Tabulation Areas (ZCTA)
	•	Description: Geographic boundaries used to align income and eviction data
	•	URL:
https://www.census.gov/programs-surveys/geography/guidance/geo-areas/zctas.html

⸻

Methodology

This project was implemented using a Bronze / Silver / Gold lakehouse architecture in Databricks.

Bronze Layer
	•	Raw ingestion of HUD FMR API responses
	•	Raw eviction records
	•	Raw ACS income estimates
	•	No transformations; original schema preserved

Silver Layer
	•	Parsed JSON structures
	•	Standardized geography identifiers
	•	Normalized rent values by bedroom type
	•	Data quality rules applied (nulls, invalid values quarantined)

Gold Layer
	•	Analytics-ready fact tables
	•	Joined income, rent, and eviction metrics by geography
	•	Designed for dashboards, SQL analysis, and notebook visualization

⸻

Story: Income, Rent Burden, and Evictions

To understand eviction risk, it is not sufficient to look at eviction counts alone. Housing affordability must be evaluated in the context of income and expected rent levels.

HUD’s Fair Market Rent provides a standardized benchmark for typical rents in a given area. When FMR consumes a large share of median household income, households are more vulnerable to economic shocks, missed payments, and eventual eviction.

The analysis proceeds in three steps:
	1.	Examine eviction patterns across geographic areas
	2.	Compare median household income by the same geography
	3.	Evaluate rent burden by comparing FMR to income

By layering these metrics together, we can observe whether eviction pressure aligns more closely with income levels, rent levels, or the interaction between the two.

⸻

Findings

Key observations from the analysis include:
	•	Areas with lower median household income tend to experience higher eviction counts
	•	Regions where Fair Market Rent represents a large share of income show elevated eviction pressure
	•	A negative correlation is observed between income and eviction activity, consistent with prior housing research
	•	Rent burden appears to amplify eviction risk beyond income alone

These results suggest that eviction is not simply a function of housing supply or tenant behavior, but is closely tied to economic capacity relative to rent benchmarks.

⸻

Limitations and Future Work

This analysis has several limitations:
	•	Eviction data availability varies by jurisdiction
	•	Income estimates are derived from survey data and may lag current conditions
	•	Causal inference is not established; correlation does not imply causation

Future work could include:
	•	Normalizing eviction counts by renter population
	•	Incorporating multiple years of data to analyze trends
	•	Evaluating the impact of eviction moratoria and rental assistance programs

⸻

Conclusion

The findings support the hypothesis that income and housing costs are strongly associated with eviction outcomes. When rents rise faster than incomes, eviction risk increases, particularly in economically vulnerable communities.

By integrating HUD Fair Market Rent, income data, and eviction records into a unified lakehouse platform, this project demonstrates how public data can be transformed into actionable insight for housing policy and resource allocation.

⸻

References
	•	HUD Fair Market Rent API
https://www.huduser.gov/portal/dataset/fmr-api.html
	•	NYC Open Data – Evictions
https://data.cityofnewyork.us/City-Government/Evictions/6z8x-wfk4
	•	U.S. Census Bureau – American Community Survey
https://www.census.gov/programs-surveys/acs
	•	Census API User Guide
https://www.census.gov/data/developers/guidance/api-user-guide.html
	•	HUD Housing Affordability Research
https://www.huduser.gov/portal/pdredge/pdr_edge_housing_market.html

⸻
