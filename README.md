# Real Estate Market Analysis for Saudi Vision Holdings

# 📚 Table of Contents

1. [Project Name](#1-project-name)  
2. [Project Background](#2-project-background)  
3. [Project Goals](#3-project-goals)  
4. [Data Collection and Sources](#4-data-collection-and-sources)  
5. [Formal Data Governance](#5-formal-data-governance)  
6. [Regulatory Reporting](#6-regulatory-reporting)  
7. [Methodology](#7-methodology)  
8. [Data Structure & Initial Checks](#8-data-structure--initial-checks)  
9. [Documenting Issues](#9-documenting-issues)  
10. [Executive Summary](#10-executive-summary)  
11. [Insights Deep Dive](#11-insights-deep-dive)  
    - [Category 1: Geographic Investment Hotspots](#category-1-geographic-investment-hotspots)  
    - [Category 2: Property Type Economics](#category-2-property-type-economics)  
    - [Category 3: Market Dynamics](#category-3-market-dynamics)  
    - [Category 4: Financial Metrics](#category-4-financial-metrics)  
    - [Category 5: Property Size Distribution](#category-5-property-size-distribution)  
12. [Recommendations](#12-recommendations)  
13. [Future Work](#13-future-work)  
14. [Technical Details](#14-technical-details)  
15. [Assumptions and Caveats](#15-assumptions-and-caveats)

# Real Estate Market Analysis for Saudi Vision Holdings

## 1. Project Name  
**Saudi Vision Holdings: Property Investment Performance & Market Dynamics Analysis**  
Comprehensive evaluation of 50,000 property records across 5 Saudi cities to optimize investment strategies and portfolio management.

---

## 2. Project Background  
Saudi Vision Holdings (SVH) operates in Saudi Arabia's real estate sector since 2010, managing a portfolio of 12,000 properties valued at 36.4B SAR. Key operational details:
- **Business Model**: Hybrid (60% direct acquisitions, 25% rental management, 15% development partnerships)
- **Active Markets**: Riyadh, Jeddah, Dammam, Makkah, NEOM
- **Key Metrics Tracked**: 
  - Rental yield (current avg: 10.84% vs target 8%)
  - Occupancy rate (current avg: 74.56% vs target 80%)
  - Days on market (current avg: 187 days vs target <90)
- **Analysis Period**: Q1–Q4 2024 transaction data

---

## 3. Project Goals  
1. **Identify underperforming assets**:  
   - **18.16%** of properties stuck on market >300 days  
   - **46.47%** exceed 200 days on market (vs <90 target)  
2. Optimize acquisition strategy: Target cities/property types with >10% yield  
3. Mitigate vacancy risks: 25% portfolio has occupancy <50%  
4. Enhance pricing models: Resolve 38% variance in price/m² calculations  
5. Compliance alignment: Ensure 100% data adherence to GAZT standards  

---

## 4. Data Collection and Sources  
| Source | Records | Frequency | Key Attributes |  
|--------|---------|-----------|----------------|  
| Internal CRM | 42,000 | Daily | Property specs, ownership history |  
| Ministry of Housing API | 8,000 | Weekly | Regulatory status, zoning |  
| Market Listings Scraper | 12,000 | Real-time | Pricing comparables |  
| Payment Gateways | 50,000 | Monthly | Rental income verification |  
| OpenStreetMap API | N/A | On-demand | Distance to city center |  

---

## 5. Formal Data Governance  
**Implemented Frameworks**:  
- ISO 8000-110:2023 for real estate data quality  
- Saudi GAZT tax reporting schemas  
- DCAM maturity assessment (score: 3.2/5)  

**Improvement Initiatives**:  
1. Automated validation for Rental_Yield_Percent >100%  
2. Geocoding via Saudi Post's API  
3. Data lineage tracking for Price_per_m²  
4. Flagging Size_m² <10 or >10,000 anomalies  

---

## 6. Regulatory Reporting  
**Compliance Standards**:  
- SAMA real estate valuation (v2023.2)  
- AML transaction monitoring  
- GAZT rental taxation  

**Protocols**:  
1. Resolve 278 SAR/m² outliers  
2. 3-point check for >1,499m² properties  
3. Archive historical records (7 years)  
4. Biometric validation for ownership  

---

## 7. Methodology  
**Analytical Techniques**:  
- Correlation: Price_SAR ↔ Size_m² (r=0.82)  
- K-means clustering (5-city segmentation)  
- Time-series for absorption trend  
- Affordability Index = (Median_Income × 0.3) / (Rent + Mortgage)  

**Statistical Models**:  
- Regression (yield prediction, R²=0.78)  
- Survival analysis (DOM)  
- Monte Carlo simulations  

---

## 8. Data Structure & Initial Checks  

**Schema Summary**: 50,000 records – single table – Q4 2024 snapshot  

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


---

## 9. Documenting Issues  

| Table | Column | Issue | Magnitude | Solvable | Resolution |  
|-------|--------|-------|-----------|----------|------------|  
| Properties | Price_per_m² | 12 records >99k SAR/m² | High | Yes | Luxury tier cross-check |  
| Properties | Rental_Yield_Percent | 47 values >100% | Medium | Yes | Cap at 99th percentile (78%) |  
| Properties | Absorption_Rate | Negative values | High | Yes | Recalc: Leased_Units_30d / Available_Units |  
| Properties | Occupancy_Rate | 1,200 zeros | Medium | Partial | Separate flag for new builds |  
| Properties | Year_Built | 340 records = 0 | Low | Yes | Impute with neighborhood medians |  

---

## 10. Executive Summary  

**For Investment Directors**:  
- **Dammam** offers best ROI: 11.03% yield with redevelopment potential  
- **DOM Risk Alert**: 46.47% of listings exceed 200 days unsold  
- Absorption rate errors affect 22% of valuation logic  
- **Apartments**: +230bps over villas in yield, best affordability  

---

## 11. Insights Deep Dive  

### Category 1: Geographic Investment Hotspots  
- **Dammam**: 11.03% yield, aging stock = upside potential  
- **NEOM**: 8,950 SAR/m² price, but 0.206 affordability, 34.1% occupancy  
- **Riyadh**:  
  - Best DOM profile: Most properties in <150-day bins  
  - Outperforms other cities where 250–365 day bins dominate  

### Category 2: Property Type Economics  
- **Apartments**:  
  - 11.07% yield, 0.213 affordability index  
  - 13.89% sold in 50–100 DOM bin  
  - 74.1% occupancy  
- **Commercial**:  
  - 74.7% occupancy, 20.3 km to center  
  - 18% higher maintenance CAPEX  
- **Land**:  
  - 67% with negative absorption  
  - 89% overlap with dev zones  

### Category 3: Market Dynamics  
- **Price-size disconnect**: r = 0.22  
- **Occupancy Skew**:  
  - Median: 99%, Mean: 74.56%  
  - 25% of units at 0% occupancy  
- **Absorption Anomalies**:  
  - 8,200 entries negative  
  - Valid correlation with occupancy = 0.82  

### Category 4: Financial Metrics  
- **Yield compression**:  
  - >3M SAR = 7.2% yield  
  - <1M SAR = 12.4% yield  
- **Affordability**:  
  - Index <0.35 = unaffordable  
  - Makkah = 0.216 = best  
- **Maintenance**:  
  - Pre-2000 = +18.7% CAPEX  
  - Dammam = oldest stock  

### Category 5: Property Size Distribution  
| Size Bin (m²) | Properties | Percentage |
|---------------|------------|------------|
| 0 – 200       | 4,952      | 9.90%      |
| 200 – 400     | 6,976      | 13.95%     |
| 400 – 600     | 6,867      | 13.73%     |
| 600 – 800     | 6,870      | 13.74%     |
| 800 – 1000    | 6,898      | 13.80%     |
| 1000 – 1200   | 6,890      | 13.78%     |
| 1200 – 1500   | **10,547** | **21.09%** |

**Insights**:  
- Largest segment = 1200–1500m²  
- Balanced: 200–1200m² bins ~14% each  
- <200m² = only 9.9% of inventory  

---

## 12. Recommendations  
1. **Divest NEOM assets**: 4,200 units <35% occupancy → save 4.2M SAR/yr  
2. **Buy Dammam Apartments**: Focus on 400–1200m², 1990–2000 build  
3. **Accelerate Riyadh Sales**: Prioritize listings hitting 150-day mark  
4. **Add Compact Units**: Address <200m² shortage in dense cities  
5. **Fix Absorption Rate Calc**: Standardize to: `Leased_Units / Available_Units`  

---

## 13. Future Work  
- Forecast demand using GASTAT demographics  
- Simulate 5% RE transaction tax effect  
- Integrate Sentinel-2 for urban sprawl analysis  
- Benchmark vs. PIF-managed real estate funds  

---

## 14. Technical Details  
- **SQL Server**: Temporal joins (50M+ records)  
- **Python**: Pandas for ETL, Scikit-learn for prediction  
- **Tableau**: Dashboards for exec review  
- **Great Expectations**: Data checks on load  

**Links**:  
- [Data Cleaning Queries](https://github.com/svh-analytics/property_cleaning)  
- [BI Queries](https://github.com/svh-analytics/business_insights)  
- [Tableau Dashboard](https://tableau.svh.com/saudiproperty)  

---

## 15. Assumptions and Caveats  
- Absorption errors: 87% = data entry → excluded from models  
- Land yields = 0 → placeholder until future dev  
- NEOM: Limited comps (1,200 entries) → skew potential  
- Affordability Index uses 8,940 SAR/mo income (GASTAT)  
- Year_Built = 0 imputed from neighborhood  
- COVID period (2020–21) excluded from trend baselines  

## Data Structure & Initial Checks  
**Main Database**: 1 table with 50,000 records (2024 snapshot)  

