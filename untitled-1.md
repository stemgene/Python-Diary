# Pandas Profiling Report

## Pearson's r

The Pearson's correlation coefficient \(_r_\) is a measure of linear correlation between two variables. It's value lies between -1 and +1, -1 indicating total negative linear correlation, 0 indicating no linear correlation and 1 indicating total positive linear correlation. Furthermore, _r_ is invariant under separate changes in location and scale of the two variables, implying that for a linear function the angle to the x-axis does not affect _r_.

To calculate _r_ for two variables _X_ and _Y_, one divides the covariance of _X_ and _Y_ by the product of their standard deviations.

## Spearman's ρ

The Spearman's rank correlation coefficient \(_ρ_\) is a measure of monotonic correlation between two variables, and is therefore better in catching nonlinear monotonic correlations than Pearson's _r_. It's value lies between -1 and +1, -1 indicating total negative monotonic correlation, 0 indicating no monotonic correlation and 1 indicating total positive monotonic correlation.

To calculate _ρ_ for two variables _X_ and _Y_, one divides the covariance of the rank variables of _X_ and _Y_ by the product of their standard deviations.

## Kendall's τ

Similarly to Spearman's rank correlation coefficient, the Kendall rank correlation coefficient \(_τ_\) measures ordinal association between two variables. It's value lies between -1 and +1, -1 indicating total negative correlation, 0 indicating no correlation and 1 indicating total positive correlation.

To calculate _τ_ for two variables _X_ and _Y_, one determines the number of concordant and discordant pairs of observations. _τ_ is given by the number of concordant pairs minus the discordant pairs divided by the total number of pairs.

## Phik \(φk\)

Phik \(φk\) is a new and practical correlation coefficient that works consistently between categorical, ordinal and interval variables, captures non-linear dependency and reverts to the Pearson correlation coefficient in case of a bivariate normal input distribution. There is extensive documentation available [here](https://phik.readthedocs.io/en/latest/index.html).

## Cramér's V \(φc\)

Cramér's V is an association measure for nominal random variables. The coefficient ranges from 0 to 1, with 0 indicating independence and 1 indicating perfect association. The empirical estimators used for Cramér's V have been proved to be biased, even for large samples. We use a bias-corrected measure that has been proposed by Bergsma in 2013 that can be found [here](http://stats.lse.ac.uk/bergsma/pdf/cramerV3.pdf).

