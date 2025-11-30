# REPORTS — Oil Sales Analysis

## 1) Approach & assumptions

Approach
- Conducted exploratory data analysis (EDA) to summarize the dataset and spot distributions, seasonality, and anomalies.
- Performed data quality checks (missing values, duplicates, negative numbers, internal price consistency checks) to validate the dataset.
- Detected outliers with the Interquartile Range (IQR) method and visualized them for interpretation (no automatic removal was performed).
- Encoded categorical variables (label encoding) and created modeling features that include product attributes, location, time, and price information.
- Built baseline predictive models using Random Forest (regression to predict sale value and classification to label high/low sales based on the median).

Assumptions
- Each row in the dataset represents a valid, individual sales transaction.
- `volume_sales`, `value_sales`, and `average_price` are numerical; any non-numeric rows were converted/validated before modeling.
- Large transactions flagged as outliers may be legitimate (e.g., wholesale/bulk orders), so the notebook does not remove them automatically.
- Label encoding is appropriate for tree-based models; if different models are used later (e.g., linear models), encoding strategy should be revisited.

---

## 2) Key findings from the analysis

1. Revenue concentration in a small set of SKUs
   - Top-performing SKUs account for a large share of revenue (top 10 SKUs contribute a meaningful percentage). This shows portfolio concentration and dependence on a few products.

2. Clear seasonality across months
   - Monthly revenue analysis shows peaks and troughs indicating predictable seasonality. These trends can be used to optimize inventory and promotion timing.

3. Distinct pricing clusters and pricing anomalies
   - The dataset contains both high-priced and low-priced SKUs and small price inconsistencies were found between computed price and recorded `average_price`. These are candidates for targeted pricing experiments and corrective validation.

4. City/region-level differences
   - Revenue distribution across cities is uneven. A small number of cities generate the majority of revenue — opportunities for localized decisions and investment.

5. High-value transactions (outliers) exist and may be business relevant
   - Large value transactions are present which might be bulk orders or B2B transactions. They should be treated separately when required for pricing / forecasting decisions.

6. Model-level insights
   - Random Forest models provided strong baseline performance and feature importances that highlight which attributes (price, brand, size, location) drive revenue and sales category predictions.

---

## 3) Possible next steps (short- and medium-term)

Short-term (analysis & modeling)
- Cross-validate and tune models using GridSearchCV or RandomizedSearchCV; try gradient boosting (LightGBM/XGBoost) to improve predictions.
- Run per-SKU and regional models where data is concentrated to achieve higher precision for top products and top cities.
- Separate high-value/bulk transactions from regular retail sales to build specialized models and prevent skew in forecasting.
- Carry out price elasticity testing (A/B experiments) on groups of SKUs to inform pricing strategy.

Medium-term (data & operations)
- Enrich the dataset with customer-level and channel-level information (customer type, online vs in-store, promotional flags) to enable segmentation and better personalization.
- Build an automated pipeline for feature extraction, model training, and evaluation (CI/CD for data science) to keep models updated with new data.
- Create dashboards that track sales performance, stockouts, price changes, and model monitoring metrics so teams can make faster commercial decisions.

Long-term / productized
- Package the model as a small API for real-time scoring or batch inference to integrate with merchandising and pricing tools.
- Implement controlled experiments and monitor ROI on pricing changes, merchandising, and marketing investments.

---

If you want, I can convert this summary into a short presentation (PDF or slides), generate reproducible environment files (`environment.yml` or `requirements.lock`), or help prepare the models for production (API + retraining pipeline).