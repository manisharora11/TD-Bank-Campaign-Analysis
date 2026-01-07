# TD-Bank-Campaign-Analysis

This Power BI dashboard analyzes marketing campaign data to identify high-potential customer segments and optimize operational efficiency. The goal was to increase Term Deposit subscriptions while reducing telemarketing costs.

<img width="812" height="529" alt="image" src="https://github.com/user-attachments/assets/ea768e49-19dc-49b3-a4c4-782e68a32ed8" />

<img width="810" height="531" alt="image" src="https://github.com/user-attachments/assets/f89778d2-dcdd-4c2a-a55e-12b43b0a0f54" />


## 1. Executive Summary

### Goal
The objective of this analysis was to optimize the effectiveness of Term Deposit marketing campaigns by identifying high-conversion customer segments and eliminating operational inefficiencies. The resulting dashboard provides a strategic view for executives to reallocate budget toward high-probability targets.

### Key Findings
* **Targeting Strategy:** The analysis identified two hyper-performing segments: **Students (29% conversion)** and **Retirees (23% conversion)**. These groups convert at 2x-3x the rate of the general population (11.7%), suggesting that future campaigns should prioritize age-based and occupation-based targeting.
* **Seasonal Timing:** Campaign performance is highly seasonal, with significant peaks in **March and September**. Conversely, high-volume outreach during the summer months (May and July) yielded the lowest returns, indicating a need to reduce summer spend.
* **Operational Efficiency:** A "Diminishing Returns" analysis revealed that conversion probability drops below 10% after the **4th call attempt**. Continuing outreach beyond this point yields negative ROI.

### Strategic Recommendations
1.  **Implement a "4-Call Cap":** Cease outreach after four unsuccessful attempts to reduce operational costs by approximately 30% without significantly impacting total sales.
2.  **Shift Budget:** Reallocate resources from low-performing summer months to aggressive targeted campaigns in March and September.
3.  **Cross-Sell Focus:** Prioritize "Debt-Free" customers, as data shows that existing loan holders have a significantly lower propensity to save.

---

## 2. Data Logic & Assumptions

To ensure data integrity and user clarity, the following transformation steps were applied to the raw dataset:

* **Data Cleaning & Terminology:** The raw field `y` (target variable) was renamed to **"Outcome"**, and values were mapped from "yes/no" to **"Subscribed / Not Subscribed"**. This aligns the dashboard with standard banking terminology.
* **Handling Ambiguity:** Records with "Unknown" values in key demographic fields (Job, Education) were filtered out of top-level visuals to prevent skewed insights, while ensuring the overall success rate calculation remained accurate across the total population.
* **Metric Definition:** **Conversion Rate** was calculated as the simple average of successful outcomes (`Count of 'Subscribed' / Total Rows`). Given the granular nature of the dataset (1 row = 1 contact), a weighted average was not required.

---

## 3. Strategic Modeling (The "Why")

Beyond standard descriptive analytics, two strategic models were developed to answer the "So What?" for the business:

### A. Call Frequency & Efficiency Modeling
* **Problem:** Call centers often waste resources on "stubborn" leads.
* **Analysis:** I plotted conversion rates against the `campaign` (contact frequency) variable. The data revealed a sharp efficiency curve where success rates stabilize and then decline after the 4th contact.
* **Solution:** I implemented a visual "Stop Point" on the dashboard to guide operational managers on exactly when to stop spending money on a lead.

### B. Financial Profile Segmentation
* **Problem:** Evaluating customers based on single product holdings (e.g., just "Housing Loan") failed to capture their total liquidity.
* **Analysis:** I created a composite "Financial Profile" variable that categorizes customers based on their full debt portfolio (Housing + Personal Loans).
* **Insight:** The model proved that "Debt-Free" customers are the primary drivers of Term Deposit sales, while "Dual Loan Holders" are high-risk targets for savings products.

---

## 4. Technical Appendix

This dashboard leverages advanced Power BI features to enhance storytelling and user experience:

### Power Query (M Code)
Custom logic was used to derive the `Financial Profile` column, simplifying complex cross-product logic into a single readable attribute:

```powerquery
// Logic to determine debt profile
if [housing] = "no" and [loan] = "no" then "Debt Free" else ...

