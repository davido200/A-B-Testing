This is an 'Suggested Solution' analysis of the [Fast Food Marketing Campaign A/B Test](https://www.kaggle.com/datasets/chebotinaa/fast-food-marketing-campaign-ab-test). The dataset concerns a fast food chain that wanted to introduce a new item to its menus. To decide on which promotional campaign to run, the chain ran an experiment.

<br>

# Goal of the Test

By running the test the company was aiming to increase sales. The goal of the test is to choose the best marketing campaign in terms of sales revenue.

<br>

# Target Metric

The dataset provides only one metric - SalesInThousands, measuring revenue per location and week in thousands. Therefore, sales will be our target metric (summed by location).

The best property of this metric is that it measures the business objective directly–revenue maximization is indeed the goal of many businesses. However, currency-denominated metrics tend to be insensitive because of high variance (here’s a [good reference](https://www.microsoft.com/en-us/research/group/experimentation-platform-exp/articles/beyond-power-analysis-metric-sensitivity-in-a-b-tests/) on metric sensitivity).

<br>

# Calculations

I will apply the t-test to see if the differences in average sales between campaigns is statistically significant. This means we will have to test three hypotheses instead of one, which will increase the false positive rate. To adjust for that, I will use a confidence level of 99% (or alpha of 0.01). Note that we could do a single hypothesis test by using [ANOVA](https://www.scribbr.com/statistics/one-way-anova/). However, ANOVA only tells us that there is a difference between groups. We also care about the direction of the difference, in addition to significance, and that requires another test.

For the calculations we will use the [Two-Sample T-Test](https://www.evanmiller.org/ab-testing/t-test.html) calculator.

<br>

| promotion  | count | avg_sales | stddev_sales |
| ----------- | ----------- | ----------- | ----------- |
| 1 | 43 | 232.4 | 64.11 |
| 2 | 47 | 189.32 | 57.99 |
| 3| 47 | 221.46 | 65.54 |

**Table 1**. Summary of the results of the Cookie Cat A/B test.

<br>

## Campaigns 1 vs 2

The difference between campaigns 1 and 2 is statistically significant. Campaign 1 performs better than campaign 2 with a difference of means of 43 thousand dollars. In other words, over the period of the test, campaign 1 generated an estimated 43 thousand dollars more than campaign 2.

<br>

<div><img src="https://i.imgur.com/7mp02ca.png" title="source: imgur.com"/></div>

<br>

## Campaigns 2 vs 3

The difference between campaigns 2 and 3 is not statistically significant. Given the alpha level I set before this analysis, the p-value of 0.0136 is too high. To establish statistical significance, the test should be run for longer or in more locations.

<br>

<div><img src="https://i.imgur.com/mS0Qi4L.png" title="source: imgur.com"/></div>

<br>

## Campaigns 1 vs 3

Likewise, the difference between campaigns 1 and 3 is not statistically significant.

<br>

<div><img src="https://i.imgur.com/tuVyzTk.png" title="source: imgur.com"/></div>

<br>

# Decision

Just looking at raw numbers, campaign 1 seems to be performing the best. However, we were only able to establish statistical significance when comparing it to campaign 2. For other comparisons, the p-values were too high to rule out the possibility that the differences occurred by chance, given the confidence level.

The recommendation would be to discontinue campaign 2 due in favor of either campaign 1 or 3. However, the choice between the two campaigns should be made by running another experiment, in which these promotion campaigns would be compared against one another.

<br>

# Appendix

### Query for table 1

```sql
WITH
 sales AS (
 SELECT
   location_id,
   promotion,
   SUM(sales_in_thousands) AS sales_thousands
 FROM
   `tc-da-1.turing_data_analytics.wa_marketing_campaign`
 GROUP BY
   ALL )
SELECT
 promotion,
 COUNT(location_id) AS `count`,
 AVG(sales.sales_thousands) AS avg_sales,
 STDDEV(sales.sales_thousands) AS stddev_sales
FROM
 sales
GROUP BY
 ALL
```
