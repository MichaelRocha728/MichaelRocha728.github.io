---
layout: default
title: OM 620 Assignments
---

# OM 620: Tools and Technology for Analytics

[View the repository on GitHub](https://github.com/MichaelRocha728/om620-assignments)

This project is from my Tools and Technology for Analytics course at Cal State San Marcos. It combines my group's assignments 1 and 2 into a single notebook. 

## Repository Contents
The repository's data folder has the transaction dataset and the metadata. The notebooks folder has one notebook that combines Assignments 1 and 2.

## Assignment 1: Data Cleaning and Transformation

- The data contains 772,807 transactions, but it was not ready to use. Firstly, the column names did not match the convention from the metadata, so we renamed leadTime, Manufacturing Site, and division Code. From there, we used describe() and found negative values for both unit price and order quantity, which is not feasible.
- To correct these mistakes, we converted the negative values to positive values, as it is impossible to have a negative unit price or to order a negative amount of items.

- The next thing was the missing data. There were missing values in 5 columns, with manufacturing site missing the most at 149,524. With so many uncertainties, we decided the best course of action was to drop them.
- We also created a country column from the manufacturing site codes and a sales_value column by multiplying unit price by order quantity.

**Findings:**
- After dropping the missing values, 552,807 transactions were left, which means about 28% of the data was removed.
- The cleaned data has 619 unique SKUs, 18 manufacturing sites across 4 countries (United States, Japan, Canada, and Poland), and 54 divisions.
- We found the top and bottom 10 transactions by order quantity and by total sales value.

## Assignment 2: Safety Stock Calculation

- Assignment 2 continues from Assignment 1, with the goal of calculating safety stock for each SKU that is Made to Stock. Before we did anything, we cleaned the data again. This time we also found lead times with extra zeros added to the end (for example, 2800 instead of 28), so we fixed those. 
- Instead of dropping the missing values like in Assignment 1, we filled them with "Unknown", because removing them would have lost a lot of data.
- From there, we filtered for Made to Stock SKUs, which left 497,889 orders, and grouped them by SKU to find the min, max, median, variance, standard deviation, and average of order quantity, along with the average lead time. 
- We then used the formula `Safety Stock = z * standard deviation of demand * sqrt(lead time)` to calculate the safety stock at the 75%, 90%, and 95% service levels, where z is the z-score of the service level.

**Findings (95% service level):**
- SKU 7D640DC9 has the largest safety stock at 361 units.
- SKU 16A11D4A has the smallest safety stock at 31 units.
- The average safety stock across all SKUs is 118 units.


**Side Quest:** The formula assumes a normal distribution of demand, which isn't always the case. So we also calculated safety stock using empirical quantiles. This gave a lower average of about 112 units, which shows the normal distribution can overestimate the safety stock for some SKUs.

## References

Anthropic. (2026). *Claude* (Opus 5.5, Nov 26 version) [Large language model]. https://claude.ai

GitHub. (2026). *GitHub Copilot* [AI coding assistant in VS Code].

The SciPy Community. (2026). *scipy.stats.mstats.mquantiles*. SciPy v1.18.0 Manual. Retrieved November 18, 2026, from https://docs.scipy.org/doc/scipy/reference/generated/scipy.stats.mstats.mquantiles.html

The SciPy Community. (2026). *scipy.stats.rv_continuous.ppf*. SciPy v1.18.0 Manual. Retrieved November 16, 2026, from https://docs.scipy.org/doc/scipy/reference/generated/scipy.stats.rv_continuous.ppf.html

pandas development team. (n.d.). *pandas.DataFrame.rename*. Retrieved October 20, 2026, from https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.rename.html

pandas development team. (n.d.). *pandas.api.typing.SeriesGroupBy.std*. Retrieved November 16, 2026, from https://pandas.pydata.org/docs/reference/api/pandas.api.typing.SeriesGroupBy.std.html

pandas development team. (n.d.). *pandas.DataFrame.astype*. Retrieved November 17, 2026, from https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.astype.html

## Appendix: AI Assistance

I used Claude (Anthropic, 2026) as an editor while completing this milestone to help with presentation and grammar in the Assignment 1 and 2 notebooks. I also used GitHub Copilot in Assignment 2 to help write the quantile aggregation code. 