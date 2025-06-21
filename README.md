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
- K-means clustering (5 clusters) with PCA validation  
- Survival analysis (Kaplan-Meier) for Days on Market  
- Monte Carlo price simulations (1,000 iterations)  
- Absorption trend analysis by vintage  
- Rental yield regression (R²=0.69)  

**Statistical Models**:  
- Cluster quality metrics (Silhouette=0.182, Davies-Bouldin=1.393)  
- Price projection with 95% CI (SAR 3.181M - 3.187M)  
- DOM liquidity thresholds (50/100/200-day triggers)  
- Vintage absorption deterioration model (-36% since 1980s)  

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
| **Cluster** | K-means segment (0-4) | Portfolio strategy grouping |  

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
- **Cluster 0 (Affordable)** delivers exceptional 85.89% yield - prioritize expansion  
- **2020+ developments** show critical absorption risk (-1.9 vs -1.4 for 1980s)  
- **DOM crisis**: 46.47% listings >200 days, 20% >300 days illiquid  
- **Price projection**: Strong 5% growth (SAR 3.184M avg) led by luxury segments  
- **Cluster 4 (Struggling)**: 27.28% occupancy requires immediate divestment  

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
- **Absorption Crisis**:  
  - 2020s properties: -1.9 absorption (-36% vs 1980s)  
  - Pre-2000 vintage maintains healthier -1.4 to -1.5 range  
- **Liquidity Thresholds**:  
  ```markdown
  | DOM Milestone | % Liquidated | Action Trigger |
  |--------------|--------------|---------------|
  | ≤50 days    | 25%          | Premium pricing |
  | ≤100 days   | 40%          | Marketing boost |
  | ≤200 days   | 60%          | Price reduction |
  | >300 days   | 20% stagnant | Divestment review |

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
- **Absorption Crisis**:  
  - 2020s properties: -1.9 absorption (-36% vs 1980s)  
  - Pre-2000 vintage maintains healthier -1.4 to -1.5 range  
- **Liquidity Thresholds**:  

  | DOM Milestone | % Liquidated | Action Trigger      |
  |---------------|--------------|---------------------|
  | ≤50 days      | 25%          | Premium pricing     |
  | ≤100 days     | 40%          | Marketing boost     |
  | ≤200 days     | 60%          | Price reduction     |
  | >300 days     | 20% stagnant | Divestment review   |

- **Occupancy Skew**:  
  - Median: 99%, Mean: 74.56%  
  - 25% of units at 0% occupancy  

### Category 4: Financial Metrics  
- **Cluster Yield Stratification**:  

  | Cluster | Avg Yield | Price Segment             |
  |---------|-----------|---------------------------|
  | 0       | 85.89%    | Affordable (231K SAR)     |
  | 1       | 3.52%     | Luxury (4.57M SAR)        |
  | 2       | 12.34%    | Mid-tier (1.69M SAR)      |
  | 3       | 8.95%     | Niche premium (3.01M SAR) |
  | 4       | 6.72%     | Struggling (3.20M SAR)    |

- **Price Projection**:  
  - +5.0% overall growth (SAR 3.184M mean)  
  - Luxury clusters (1 & 3): +7–9% growth potential  

### Yield Calculation Formula
`Yield = 0.25 × Affordability - 0.18 × Price + 0.15 × Occupancy - 0.12 × Absorption`

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

### Category 6: Cluster Portfolio Segmentation  

| Cluster | Properties | Key Characteristics              | Strategic Position        |
|---------|------------|----------------------------------|---------------------------|
| **0**   | 2,060      | Affordable high-yield (85.89%)   | Yield arbitrage           |
| **1**   | 17,424     | Luxury low-yield (3.52%)         | Capital appreciation      |
| **2**   | 17,308     | Balanced mid-tier (12.34%)       | Core portfolio            |
| **3**   | 642        | Niche premium (99.33% occupancy) | Absorption risk           |
| **4**   | 12,566     | High vacancy (27.28% occupancy)  | Divestment target         |

**Quality Metrics**:  
- Silhouette Score: 0.182 (weak separation)  
- Davies-Bouldin: 1.393 (moderate compactness)  
- PCA shows overlap in mid/low-price segments  

---

## 12. Recommendations  

1. **Cluster-Driven Portfolio Strategy**:  
 - **Divest Cluster 4**: 5–7% discount for quick liquidation  
 - **Premium Pricing**: Cluster 0 (+3–5%) & Cluster 1 (+7–9%)  
 - **Boost Cluster 2**: Increase yield to 15% via occupancy optimization  

2. **Absorption Recovery**:  
 - Halt new construction where absorption < -1.7  
 - Discount 2020+ properties by 5–7%  
 - Acquire 1980–2000 vintage assets  


3. **Real Estate Portfolio Optimization Framework

### Portfolio Optimization Strategy
**Yield Optimization**  
- 🔴 **Divestment Criteria**: Assets with predicted yield < 6%  
- 🟢 **Acquisition Targets**:  
  `Affordability_Index > 0.3`  
  `Absorption_Rate > -1.5`  

**Vintage Repositioning**  
- ♻️ **Post-2020 Assets**: Convert underperformers to co-living spaces  
- 🧩 **Pre-2000 Assets**: Bundle with value-add services (e.g., smart home upgrades, concierge)  

---

### 13.Future Work Pipeline
| Module                      | Focus Area                          |
|-----------------------------|-------------------------------------|
| Cluster DOM Survival Curves | Tier-specific property lifecycle modeling |
| Absorption Forecasting      | City/cluster-level lease velocity predictions |
| Monte Carlo Simulations     | Risk analysis per cluster tier      |
| Satellite Data Integration  | Urban density validation            |
| Compliance Dashboards       | Cluster-based regulatory tracking   |

---

### 14.Technical Implementation
**Methodology**  
- **Clustering**: K-means (`k=5`) with PCA validation  
- **Survival Analysis**: Kaplan-Meier estimator (DOM modeling)  
- **Simulations**: Monte Carlo (1,000 iterations, normal dist. assumption)  
- **Yield Model**: Linear Regression (`R² = 0.69`)  


