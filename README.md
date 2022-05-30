# Retention Rate A/B Testing

This project aims to uncover if there are statistically significant differences in the player retention rates between setting the gate at level 30 versus 40. This project utilizes the Cookie Cat dataset, which contains the player's version, the total number of game rounds, and whether they're retained in the one or seven days metric. The retention rate will be calculated by the number of retained players divided by the total number of players in that version.

## Motivations

Organizations must determine if changes to their product have the intended effect on their clients. A/B testing would be a crucial component of understanding user behavior differences. This technique utilizes various statistical tests to determine if the changes are from random chance or a change. 

## Methods

This project is performed with Python and Jupyter Notebook. The data contained 90189 samples split between the gate 30 and gate 40 versions. 

#### ETL:
1. Read the data with Pandas Library.
2. Review the data to determine if the labels are in the correct datatype and find the number of null values.
3. Look for any illogical samples (i.e., retained for seven days, but not for one day).
4. Handle null values and discrepancies.

#### Exploratory Data Analysis:

In this step, I will go over each feature to address outliers, compare the game rounds of each version, and compare the retention rate of the different metrics. 

#### A/B Testing:

The metrics for the A/B test:
- Null Hypothesis: no significant difference in the retention rates between the versions.
- Alternate Hypothesis: statistically significant difference in the retention rates between the version.
- Alpha: 0.05

I did the A/B testing with a function that takes four inputs, the two different observations, the alpha level, and the direction of the test. This function first tests the normality of the two observations with the Shapiro test. This test operates with a null hypothesis that the data is normal; if the p-value is less than the alpha, the null hypothesis is rejected, and the data is not normal. This step is crucial because there are different statistical tests for normal and abnormal data. The normality assumption can also be satisfied if the sample size is large enough due to the central limit theorem. 

If the data is normal, the test is conducted with Student's T-Test; otherwise, it's conducted with the Mann-Whitney U Test. Then, to calculate the statistical power of the result, I calculated the effect size using Cohen's D. 

## Results:

Statistics for players with less than 100 rounds played

#### Overall retention rate 

one-day: 39%, seven-day: 7%.

#### One day Retention Rates

Gate30: 39%, Gate40: 38%.

Statiscally significant different with statistical power of 0.68.

#### Seven day Retention Rate

Gate30: 7%, Gate40: 6%.

Statiscally significant different with statistical power of 1.

#### Rounds Played

Percentage of players past round 30 - Gate30: 26.36%, Gate40: 25.46%.

Percentage of players past round 40 - Gate30: 18.56%, gate40: 18.5%.

## Recommendation

The gate 30 version showed higher retention rate in both one-day and seven-day metrics. The AB test also showed that this difference is statistically significant. Therefore, I recommend implementing the gate 30 version going forward.
