# 📊 Statistics Research Projects

Two research projects from my Bachelor of Statistics at **Universitas Diponegoro**, each written up as a manuscript for *Jurnal Gaussian*. Both use **clustering** as the first step and then answer a real decision question: *where should poverty programs focus?* and *how should an investor split money across sustainable stocks?*

| # | Project | Question | Methods | Tools |
|---|---|---|---|---|
| 1 | [Poverty Clustering with DENCLUE](#1-poverty-clustering-of-514-indonesian-regenciescities-with-denclue) | Which regions share similar poverty profiles? | Density-based clustering (DENCLUE), DBCV validation, spatial mapping | R, RStudio, Excel |
| 2 | [Stock Portfolio Optimization](#2-sri-kehati-stock-portfolio-optimization-with-ward-clustering--mean-semivariance) | How do you build a downside-risk-aware portfolio? | Ward clustering, Silhouette, Mean-Semivariance, Value at Risk | R, RStudio, Excel |

---

## 1. Poverty Clustering of 514 Indonesian Regencies/Cities with DENCLUE

*Undergraduate thesis · with Moch. Abdul Mukid & Diah Safitri (supervisors)* · 📄 [Read the manuscript](Jurnal%20Gaussian%201.pdf)

![Cluster map of Indonesia](assets/denclue-map-indonesia.png)

### ❓ Question
Indonesia's poverty rate was 8.47% in March 2025, but conditions differ widely between regions, so a one-size-fits-all national policy works poorly. **Which regencies and cities share similar poverty characteristics, so programs can be targeted?**

### 🗂️ Data
- **514 regencies/cities**, from BPS's *Data dan Informasi Kemiskinan Kabupaten/Kota 2025*
- **8 indicators:** poverty rate, poverty severity index (P2), share of residents who finished primary/junior high school, share not working, share in informal work, share of spending on food, access to safe water, and access to proper sanitation

### ⚙️ Method
```
Z-score standardization → Euclidean distance → Gaussian kernel density
→ Hill climbing to density attractors → Merge attractors within radius → Density threshold
→ Validate with DBCV → Profile clusters → Map
```
I chose DENCLUE because it finds clusters of **irregular shape** and handles **outliers** better than distance-only methods. I evaluated it with **DBCV**, a validation index designed for density-based clustering.

### 📈 Results
- Best parameters: σ = 1.3, merge radius = 0.07, density threshold = 1, giving a **DBCV score of 0.8152** (a high-quality cluster structure)
- **6 clusters**, with 223, 285, 1, 3, 1 and 1 members

| Cluster | Members | Profile |
|---|---|---|
| 1 & 2 | 508 regions | Relatively prosperous: poverty around 10%, water and sanitation access above 84% |
| 3 | Supiori | Highest poverty (42.6%) and severity (P2 = 4.96), and very high non-employment |
| 4 | Puncak, Yahukimo, Pegunungan Bintang | Mostly informal work (87%), very low water (43%) and sanitation (14%) access |
| 5 | Puncak Jaya | High poverty (35.5%) despite the best water access (93%) |
| 6 | Tolikara | Multidimensional vulnerability: lowest education (13%), highest food-spending share (78%), lowest water and sanitation access |

![Cluster characteristics](assets/denclue-cluster-profile.png)

### 💡 Insight
Almost every region outside Papua falls into Clusters 1–2. The vulnerable clusters sit in **inland and highland Papua**, while coastal areas such as Sorong, Merauke and Jayapura join the national pattern. Poverty is therefore **geographically concentrated, not random**, which supports policies designed around local characteristics rather than uniform national programs.

![Cluster map of Papua](assets/denclue-map-papua.png)

---

## 2. SRI-KEHATI Stock Portfolio Optimization with Ward Clustering & Mean-Semivariance

*with Abdul Hoyyi & Sugito* · 📄 [Read the manuscript](Jurnal%20Gaussian%202.pdf)

### ❓ Question
Indonesia had 5.9 million stock investors in 2024. For investors who care about sustainability, the **SRI-KEHATI index** (25 stocks screened for environmental, social and governance criteria) is an option. **How can you pick stocks from it and weight them so the portfolio limits downside risk?**

### 🗂️ Data
- **ROA, ROE and NPM** from the 2024 financial statements of the **25 SRI-KEHATI constituents**, used for clustering
- **Daily closing prices**, 3 Jun 2024 – 24 Jan 2025, with the **IHSG** (Jakarta Composite Index) as benchmark, used for portfolio building

### ⚙️ Method
```
Standardize ROA/ROE/NPM → Check KMO & VIF → Ward clustering (3, 4, 5 clusters)
→ Pick k by Silhouette → From each cluster, take the stock with the highest positive expected return
→ Semivariance–semicovariance matrix → Mean-Semivariance weights → Historical-Simulation VaR
```
I used **Mean-Semivariance** instead of classic Mean-Variance because it measures only **downside** deviations and does not assume normally distributed returns.

### 📈 Results
- **4 clusters** gave the best Silhouette score (0.517, compared with 0.433 for 3 clusters and 0.483 for 5)
- Selected **DSNG, UNTR and BBCA**. UNVR was dropped because its expected return was negative.

| Stock | Weight |
|---|---|
| BBCA | 69.96% |
| UNTR | 28.50% |
| DSNG | 1.54% |

- Expected daily portfolio return of **0.0441%**, with semivariance of **0.0000738**
- **Value at Risk (95%, Historical Simulation):**

| Holding period | 1 day | 5 days | 10 days | 20 days |
|---|---|---|---|---|
| VaR | 1.52% | 3.40% | 4.81% | 6.81% |

### 💡 Insight
Clustering on profitability gives a structured way to **shortlist stocks**, and Mean-Semivariance turns that shortlist into weights that focus on **losses rather than total volatility**. VaR then puts a number on the worst expected loss at each holding period.

> *Academic research only, not investment advice.*

---

## 🧰 Skills Demonstrated

`Cluster analysis (density-based & hierarchical)` · `Cluster validation (DBCV, Silhouette)` · `Kernel density estimation` · `Portfolio optimization` · `Risk measurement (semivariance, VaR)` · `Assumption checks (KMO, VIF)` · `Spatial visualization` · `R / RStudio` · `Excel` · `Scientific writing`

---

↩️ Back to [my profile](https://github.com/gencWeze)
