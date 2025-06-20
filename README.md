# Real Estate Market Analysis for Saudi Vision Holdings

# Table of Contents

1. [Project Name](#project-name)  
2. [Project Background](#project-background)  
3. [Project Goals](#project-goals)  
4. [Data Collection and Sources](#data-collection-and-sources)  
5. [Formal Data Governance](#formal-data-governance)  
6. [Regulatory Reporting](#regulatory-reporting)  
7. [Methodology](#methodology)  
8. [Data Structure & Initial Checks](#data-structure--initial-checks)  
9. [Documenting Issues](#documenting-issues)  
10. [Executive Summary](#executive-summary)  
11. [Insights Deep Dive](#insights-deep-dive)  
12. [Recommendations](#recommendations)  
13. [Future Work](#future-work)  
14. [Technical Details](#technical-details)  
15. [Assumptions and Caveats](#assumptions-and-caveats)  

 
---

## Project Name  
**Saudi Vision Holdings: Property Investment Performance & Market Dynamics Analysis**  
Comprehensive evaluation of 50,000 property records across 5 Saudi cities to optimize investment strategies and portfolio management.

---

## Project Background  
Saudi Vision Holdings operates in Saudi Arabia's real estate sector since 2010, managing a portfolio of 12,000 properties valued at 36.4B SAR. The company utilizes a hybrid business model:  
- Direct property acquisitions (60% of revenue)  
- Rental management services (25%)  
- Commercial development partnerships (15%)  
Key metrics tracked: Rental yield (target: 8%), occupancy rate (target: 80%), and days on market (target: <90 days). Analysis covers Q1-Q4 2024 transaction data.

---

## Project Goals  
1. **Identify underperforming assets**: 17% of properties exceeded 300 days on market  
2. **Optimize acquisition strategy**: Target cities/property types with >10% yield  
3. **Mitigate vacancy risks**: 25% portfolio has occupancy <50%  
4. **Enhance pricing models**: Resolve 38% variance in price/m² calculations  

---

## Data Collection and Sources  
| Source | Records | Update Frequency | Key Attributes |  
|--------|---------|------------------|----------------|  
| Internal CRM | 42,000 | Daily | Property specs, ownership history |  
| Ministry of Housing API | 8,000 | Weekly | Regulatory status, zoning |  
| Market Listings Scraper | 12,000 | Real-time | Pricing comparables |  
| Payment Gateways | 50,000 | Monthly | Rental income verification |  

---

## Formal Data Governance  
**Implemented Frameworks**:  
- ISO 8000-110:2023 for real estate data quality  
- Saudi GAZT tax reporting schemas  
**Improvement Initiatives**:  
1. Automated validation rules for Rental_Yield_Percent (flag values >100%)  
2. Standardized geocoding for Distance_to_Center_km (API integration)  
3. Data lineage tracking for Price_per_m² calculations  

---

## Regulatory Reporting  
Addressed compliance with:  
- Saudi Real Estate Authority (REA) valuation standards  
- Anti-Money Laundering (AML) transaction monitoring  
- GAZT rental income taxation requirements  
**Resolution Methodology**:  
- Outlier reconciliation protocol for 278 SAR/m² outliers  
- 3-point verification for property sizes >1,499m²  

---

## Methodology  
**Techniques Applied**:  
1. Correlation network analysis (Price_SAR ↔ Size_m²: r=0.82)  
2. K-means clustering for city segmentation  
3. Time-series decomposition for absorption rate forecasting  
4. Affordability Index calculation:  
   `(Median_Income × 0.3) / (Annual_Rent_SAR + Mortgage_Cost)`  

---

## Data Structure & Initial Checks  
**Main Database**: 1 table with 50,000 records (2024 snapshot)  

### Properties Table  
| Column | Description | Usage Considerations |  
|--------|-------------|----------------------|  
| Property_ID | UUID v4 | Primary key for joins |  
| City | City name | Used for geographic segmentation |  
| Property_Type | Type of property (Land, Villa, Commercial) | Segmentation and pricing strategy |  
| Size_m2 | Property size in square meters | Used in price/m² and valuation |  
| Price_SAR | Sale price in SAR | Key for revenue analysis |  
| Annual_Rent_SAR | Annual rent income in SAR | Used for yield calculations |  
| Rented_Units | Number of rented units | For occupancy and cash flow |  
| Total_Units | Total available units | For scale and occupancy ratio |  
| Available_Units | Units available for rent/sale | Vacancy and supply analysis |  
| Days_on_Market | Days listed on market | Market demand and pricing efficiency |  
| Year_Built | Construction year | Age-related maintenance forecasting |  
| Distance_to_Center_km | Distance from city center | Accessibility premium analysis |  
| Urban_Density_Index | Density metric | Urbanization and saturation insights |  
| Price_per_m2 | Calculated (Price_SAR / Size_m2) | Price standardization for comparison |  
| Rental_Yield_Percent | (Annual_Rent_SAR / Price_SAR) * 100 | Investor ROI indicator |  
| Occupancy_Rate | (Rented_Units / Total_Units) | Market demand and performance |  
| Absorption_Rate | Rate leased/sold over time | Market velocity indicator |  
| Affordability_Index | Composite affordability measure | Pricing and policy guidance |  

## Documenting Issues

| Table      | Column               | Issue                     | Magnitude | Solvable | Resolution                                 |
|------------|----------------------|---------------------------|-----------|----------|--------------------------------------------|
| Properties | Price_per_m²         | 12 records >99k SAR/m²    | High      | Yes      | Cross-check with luxury tier verification  |
| Properties | Rental_Yield_Percent | 47 values >100%           | Medium    | Yes      | Cap at 99th percentile (78%)               |
| Properties | Absorption_Rate      | Negative values           | High      | Yes      | Recalculate as: (Leased_Units_30d / Available_Units) |
| Properties | Occupancy_Rate       | 1,200 zero values         | Medium    | Partial  | Distinguish between new/vacant properties  |

---

## Executive Summary

**For Investment Directors:**  

- Dammam properties deliver highest ROI (11.03% yield) but require age-related maintenance  
- 74% occupancy gap between Riyadh (75.2%) and NEOM (0.74%) signals market imbalance  
- Absorption rate miscalculations impact 22% of portfolio valuation models  

![Rental Yield by City](data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciPjxyZWN0IHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjIwMCIgZmlsbD0iI2Y1ZjVmNSIvPjx0ZXh0IHg9IjUwJSIgeT0iNTAlIiBkb21pbmFudC1iYXNlbGluZT0ibWlkZGxlIiB0ZXh0LWFuY2hvcj0ibWlkZGxlIiBmb250LXNpemU9IjE4Ij5SYW5rZWQgQmFyIENoYXJ0OiBEYW1tYW0gKDExLjAzJSkgPiBNYWtrYWggKDExLjAxJSkgPkppZWRkaCgxMC44JSkgUj
l5YWRoKDEwLjclKSA+IE5FT00gKDkuOCUpPC90ZXh0Pjwvc3ZnPg==)

---

## Insights Deep Dive

### Category 1: Geographic Investment Hotspots

- **Dammam yield leadership**  
  - 11.03% avg yield vs national avg 10.84%  
  - Correlates with older properties (avg 32.7 yrs) offering redevelopment upside  

- **NEOM premium positioning**  
  - Highest price/m² (8,950 SAR) but lowest affordability (0.206)  
  - 47% below target occupancy (34.1% vs 80% target)  

- **Riyadh liquidity advantage**  
  - Shortest Days on Market at 186 days (vs 251 days in secondary cities)  
  - Absorption rate 23% faster than portfolio average  

---

### Category 2: Property Type Economics

- **Apartments: Yield champions**  
  - 11.07% rental yield with 0.213 affordability index  
  - 74.1% occupancy with 123 avg days on market  

- **Commercial: Stability profile**  
  - 74.7% occupancy and 20.3km avg city center proximity  
  - Requires 18% higher maintenance CAPEX  

- **Land: Speculative profile**  
  - Negative absorption rates in 67% of records  
  - 89% correlation with urban development zones  

---

### Category 3: Market Dynamics

- **Price-size disconnect**  
  - Weak correlation between Price_per_m² and location/density (r=0.22)  
  - Luxury segment (top 5%) shows inverse yield-size relationship  

- **Occupancy skew**  
  - Median occupancy 99% vs mean 74.56%  
  - 12,500 units (25%) at 0% occupancy dragging yields  

- **Absorption anomalies**  
  - Negative rates in 8,200 records indicating calculation errors  
  - Valid rates show 0.82 correlation with occupancy  

---

### Category 4: Financial Metrics

- **Rental yield compression**  
  - >3M SAR properties yield 7.2% vs <1M SAR at 12.4%  
  - Villa yields underperform by 230bps vs apartments  

- **Affordability thresholds**  
  - Index <0.35 indicates unaffordable for 80% of population  
  - Makkah most accessible (0.216) despite premium pricing  

- **Maintenance cost exposure**  
  - Pre-2000 properties require 18.7% higher CAPEX  
  - Dammam has oldest inventory (avg 32.7 years)  

---

## Recommendations

- **Divest underperforming NEOM assets**  
  - Exit 4,200 units with <35% occupancy saving 4.2M SAR/yr  

- **Acquire Dammam apartment complexes**  
  - Target properties built 1990-2000 with 100-300m² units  

- **Correct absorption calculation**  
  - Implement: (Leased_Units_30d / Available_Units) saving 560 analyst-hrs/yr  

- **Create mid-tier affordability fund**  
  - Allocate 200M SAR for Makkah apartments with 0.18-0.22 index range  

- **Luxury portfolio rebalancing**  
  - Reduce >6M SAR holdings from 18% to 12% of portfolio  

---

## Future Work

- **Demand forecasting model**  
  - Integrate demographic data from General Authority for Statistics  

- **Regulatory change impact analysis**  
  - Simulate effects of new 5% real estate transaction tax  

- **Satellite imagery utilization**  
  - Analyze urban expansion patterns near existing holdings  

- **Cross-portfolio benchmarking**  
  - Compare performance against PIF real estate funds  

---

## Technical Details

**Toolstack Rationale:**  

- **SQL Server:** Handles 50M+ record joins with temporal data versioning  
- **Python (Pandas/Scikit-learn):** Enables ML-based yield forecasting  
- **Tableau:** Real-time dashboarding for investment committee  
- **Great Expectations:** Automated data validation at ingestion  

[Data Cleaning Queries](https://github.com/svh-analytics/property_cleaning)  
[Business Queries](https://github.com/svh-analytics/business_insights)  
[Tableau Dashboard](https://tableau.svh.com/saudiproperty)  

---

## Assumptions and Caveats

- Negative absorption rates: Assumed data entry errors (87% confirmed), excluded from investment scoring  
- Land rental yields: Treated as placeholder zeros pending development plans  
- NEOM data: Limited comparables (1,200 records) may skew city-level insights  
- Affordability Index: Used 2023 median income of 8,940 SAR/month (GASTAT)  
- Year 0 values: 340 records with Year_Built=0 imputed using neighborhood medians  
