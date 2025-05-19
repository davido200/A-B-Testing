# A/B Testing for Fast-Food Marketing Campaigns

## Project Objective

A fast-food chain introduced a new item and tested three different marketing campaigns to promote it. This project analyzes the sales data collected over the first four weeks from various locations to determine which marketing campaign had the greatest positive effect on sales revenue for the new item.

## Dataset

The dataset used for this analysis is `WA_Marketing-Campaign.csv`. It contains the following columns:

* `MarketID`: Unique identifier for the market.
* `MarketSize`: Size of the market (e.g., Small, Medium, Large).
* `LocationID`: Unique identifier for the store location.
* `AgeOfStore`: Age of the store in years.
* `Promotion`: The type of marketing campaign used (1, 2, or 3).
* `week`: The week number of the promotion (1 to 4).
* `SalesInThousands`: Sales of the new item in thousands of dollars for that week at that location.

## Analysis Overview

The analysis was conducted using Python in a Jupyter Notebook (`Fast_food_Markerting_test.ipynb`). The key steps involved were:

1.  **Data Loading and Cleaning:** The dataset was loaded using pandas, checked for missing values, and its basic structure was examined.
2.  **Exploratory Data Analysis (EDA):**
    * Calculated total and average sales for each promotion type.
    * Visualized sales distributions using boxplots and violin plots to compare the performance of the three promotions.
    * Examined sales performance across different market sizes.
3.  **Statistical Testing (A/B Testing):**
    * An **ANOVA (Analysis of Variance)** test was performed to determine if there were any statistically significant differences in mean sales among the three promotion groups.
    * **Tukey's HSD (Honestly Significant Difference) post-hoc test** was used to identify which specific pairs of promotions had significantly different sales means.
4.  **Further Analysis:** Investigated if the best-performing promotion varied by `MarketSize`.

## Libraries Used

* `pandas` for data manipulation and analysis.
* `matplotlib.pyplot` and `seaborn` for data visualization.
* `scipy.stats` for statistical functions.
* `statsmodels.api`, `statsmodels.formula.api`, and `statsmodels.stats.multicomp` for conducting ANOVA and Tukey's HSD tests.

## Key Findings

### Overall Promotion Performance:

* **ANOVA Test:** The results showed a statistically significant difference in mean sales among the three promotions (F-statistic: 21.95, p-value < 0.001).
* **Tukey's HSD Test:**
    * **Promotion 1 vs. Promotion 2:** Promotion 1 resulted in significantly higher sales than Promotion 2. (Mean difference: approx. 10.77k, p < 0.001)
    * **Promotion 1 vs. Promotion 3:** There was **no statistically significant difference** in sales between Promotion 1 and Promotion 3. (Mean difference: approx. 2.73k, p = 0.2444)
    * **Promotion 2 vs. Promotion 3:** Promotion 3 resulted in significantly higher sales than Promotion 2. (Mean difference: approx. 8.04k, p < 0.001)

### Average Sales (in Thousands):

* Promotion 1: ~58.10k
* Promotion 3: ~55.36k
* Promotion 2: ~47.33k

### Promotion Performance by Market Size:

The analysis also identified the promotion with the highest average sales within each market size:

* **Large Market:** Promotion 3
* **Medium Market:** Promotion 1
* **Small Market:** Promotion 1

## Conclusion & Recommendations

1.  **Promotion 2 is the least effective** and should be avoided as it consistently resulted in significantly lower sales compared to both Promotion 1 and Promotion 3.
2.  **Both Promotion 1 and Promotion 3 significantly outperformed Promotion 2.**
3.  While Promotion 1 had the highest overall average sales, there was **no statistically significant difference in performance between Promotion 1 and Promotion 3.**

**Recommendations for the Fast-Food Chain:**

* Given that Promotion 1 and Promotion 3 perform similarly well (statistically), the choice between them can be based on other factors:
    * **Cost of Implementation:** If one promotion is significantly cheaper or easier to implement, it might be preferred.
    * **Market-Specific Strategy:** The chain could consider tailoring promotions by market size:
        * Use **Promotion 3** in **Large Markets**.
        * Use **Promotion 1** in **Medium and Small Markets**.
    * If a single, uniform campaign is desired, **Promotion 1** could be chosen due to its slightly higher overall average sales, keeping in mind its statistical similarity to Promotion 3.

## How to Use

To replicate this analysis or explore the data further:

1.  Ensure you have Python and the listed libraries installed.
2.  Download the dataset `WA_Marketing-Campaign.csv` and the Jupyter Notebook `Fast_food_Markerting_test.ipynb`.
3.  Place both files in the same directory.
4.  Open and run the cells in the Jupyter Notebook.
