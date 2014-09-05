Stats
=====


Counts
------

``totalFreq``: count of all records
``missingFreq``: count of missing records
``invalidFreq``: count of invalid records
``cardinality``: count of unique values

NumericInfo
-----------

### ``minimum`` / ``maximum``

### ``mean``

$$ mean={\Sigma_{i} x_i \over n}$$

trimmed mean: TODO

### ``standardDeviation``


### ``median``

50% quantile

### ``interQuartileRange``

75% quantile - 25% quantile

Discrete Statistics
-------------------

``modalValue``: most frequent discrete value

Continuous Statistics
---------------------

``totalValuesSum``

``totalSquaresSum``

``interval``


“ANOVA” stands for “Analysis of Variance” while “MANOVA” stands for “Multivariate Analysis of Variance.”
2.The ANOVA method includes only one dependent variable while the MANOVA method includes multiple, dependent variables.

Read more: Difference Between ANOVA and MANOVA | Difference Between | ANOVA vs MANOVA http://www.differencebetween.net/science/mathematics-statistics/difference-between-anova-and-manova/#ixzz3AmMaeJMj


T-test: 2 groups
ANOVA: more than 2 groups
Anova tests use variances to know whether the means are equal or not.

ANOVA and Regression: both continuous outcome variable

The regression model: based on one or more continuous predictor variables. 
ANOVA model: based on one or more categorical predictor variables.

In ANOVA there can be several error terms whereas there is only a single error term in regression.
ANOVA is mainly used to determine if data from various groups have a common means or not.

5.Regression is widely used for forecasting and predictions.


Type I Error: False Positive
Type II Error: False Negative


Moment

Central Moment

$$ {\bf Central \, Moment} = \mu_n = {\bf E} [(X - {\bf E}[X])^n] = \int_{-\infty}^{+\infty} (x-\mu)^n f(x) \, dx $$

where E is the expectation operator; f(x) is probability density function.

For random variables that have no mean, such as the Cauchy distribution, central moments are not defined.

* First moment is mean: $$\mu=mean$$;
* Zeroth central moment is 1: $$\mu_0 = 1$$
* Fisrt central moment is 0: $$\mu_1=0$$
* Second central moment is variance: $$\mu_2=\sigma^2$$, where $$\sigma$$ is standard deviation
* The 3rd and 4th central moments are used to define the standardized moments



Standardized Moment

$$ {\bf Standardized \, Moment} = {\mu_k \over \sigma^k} $$

The first standardized moment is zero, because the first moment about the mean is zero
The second standardized moment is one, because the second moment about the mean is equal to the variance (the square of the standard deviation)
The third standardized moment is the skewness
The fourth standardized moment is the kurtosis

$$ {\mu_1 \over \sigma} = {0 \over \sigma} = 0 $$


Laplace Distribution
--------------------
pdf

$$ {f(x \mid \mu, b)} = {1 \over 2b} {\exp - {\mid x - \mu \mid \over b}} $$

svm

http://svms.org/parameters/


Empirical Risk Minimization: NN; overfitting
Structural Risk Minimization: SVM

NN: local minima, SVM is global and unique

SVM have a simple geometric interpretation and give a sparse solution