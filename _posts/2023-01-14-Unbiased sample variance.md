---
title: Unbiased Sample Variance
subtitle: Bessel's correction for the sample variance
layout: default
date: 2023-01-14
keywords: statistics
summary: Bessel's correction for the sample variance
published: true
---
#### tags: `statistics`

## Why do we divide by $n-1$ instead of $n$ when we calculate the sample variance?

The definition of Variance of a random variable X is given by
{% katexmm %}
$$
Var[X] = E\left[(X_i - E[X])^2\right]
$$
{% endkatexmm %}

For the sample estimator of the variance, we often use the following sample
variance formula.

{% katexmm %}
$$
\hat{\sigma}^2 = \frac{1}{n-1}\left(\sum_{i=1}^n (X_i - \bar{X})^2\right) 
$$
{% endkatexmm %}

Why do we divide by $(n-1)$ instead of $n$? This might be confusing since we don't divide by $(n-1)$ for the sample mean $\bar{X} = \frac{\sum_{i=1}^n X_i}{n}$.

### Short answer 

It's because the sample variance $\hat{\sigma}^2$ with $(n-1)$ denominator is an unbiased estimator of the true variance $\sigma^2$ assuming that the samples are independent and identically distributed(iid).

>This behavior is called [Bessel's correction](https://en.wikipedia.org/wiki/Bessel%27s_correction). One thing you should keep in mind is that the Bessel's correction is only for the samples from iid distribuiton. If the samples are not iid, (e.g. Time-Series data) the Bessel's correction would not yield an unbiased estimator.

### Long answer

#### What is unbiased estimator?

When we estimate some unknown parameter $\theta$, we call an estimator $\hat{\theta}$ is unbiased when $E[\hat{\theta}] = \theta$. We may think of an estimator $\hat{\theta}$ as an educated guess for an unknown parameter $\theta$ under the available finite sample data $(X_1, X_2, \cdots, X_n)$. Unbiasedness is one of the desirable properties for an estimator.

#### Unbiasedness of sample variance

Let $X_i$'s $(i = 1, 2, \cdots, n)$ are iid random samples, from a distribution
with mean $\mu$ and variance $\sigma^2$ , and let $\bar{X} = \frac{\sum_{i=1}^n
X_i}{n}$.

{% katexmm %}
$$
\begin{aligned}
\hat{\sigma}^2 &= \frac{1}{n-1}\left(\sum_{i=1}^n (X_i - \bar{X})^2\right) \\
&= \frac{1}{n-1}\left(\sum_{i=1}^n (X_i^2 - 2X_i\bar{X} + \bar{X}^2)\right) \\
&= \frac{1}{n-1}\left(\sum_{i=1}^n X_i^2 - \sum_{i=1}^n 2X_i\bar{X} + \sum_{i=1}^n \bar{X}^2)\right) \\
&= \frac{1}{n-1}\left(\sum_{i=1}^n X_i^2 - 2\bar{X}\sum_{i=1}^n X_i + n \bar{X}^2)\right) \\
&= \frac{1}{n-1}\left(\sum_{i=1}^n X_i^2 - 2\bar{X}n\bar{X} + n \bar{X}^2)\right) \\
&= \frac{1}{n-1}\left(\sum_{i=1}^n X_i^2 - 2n\bar{X}^2 + n \bar{X}^2)\right) \\
&= \frac{1}{n-1}\left(\sum_{i=1}^n X_i^2 - n\bar{X}^2\right) \\
\end{aligned}
$$
{% endkatexmm %}

{% katexmm %}
$$
\begin{aligned}
E[\hat{\sigma}^2] &= E\left[\frac{1}{n-1}\left(\sum_{i=1}^n X_i^2 - n\bar{X}^2\right)\right] \\
&= \frac{1}{n-1}E\left[\left(\sum_{i=1}^n X_i^2 - n\bar{X}^2\right)\right] \\
&= \frac{1}{n-1}\left(E\left[\sum_{i=1}^n X_i^2 \right] - E\left[ n\bar{X}^2\right]\right) \\
&= \frac{1}{n-1}\left(\sum_{i=1}^n E\left[ X_i^2 \right] - nE\left[ \bar{X}^2\right]\right) \qquad (1)\\
\end{aligned}
$$
{% endkatexmm %}

Note that
{% katexmm %}
$$
\begin{aligned}
\sigma^2 &= E[X^2] - E[X]^2 \\
&= E[X^2] - \mu^2 \\
\\
\therefore \quad E[X^2] &= \sigma^2 + \mu^2 \qquad (2)
\end{aligned}
$$
{% endkatexmm %}

{% katexmm %}
$$
\begin{aligned}
Var[\bar{X}] &= E[\bar{X}^2] - E[\bar{X}]^2 \\ 
E[\bar{X}^2] &= Var[\bar{X}] + E[\bar{X}]^2 \\ 
\end{aligned}
$$
{% endkatexmm %}
i)
{% katexmm %}
$$
\begin{aligned}
Var[\bar{X}] &= Var\left[ \frac{\sum X_i}{n} \right] \\
&= \frac{1}{n^2} Var\left[ \sum X_i \right] \\
&= \frac{1}{n^2} \sum Var\left[X_i \right] \quad \because X_i\text{'s are mutually ind.}\\
&= \frac{1}{n^2} n\sigma^2 \quad \because X_i\text{'s are identically distributed}\\
&=\frac{\sigma^2}{n}
\end{aligned}
$$
{% endkatexmm %}
ii)

{% katexmm %}
$$
\begin{aligned}
E[\bar{X}] &= E\left[{\frac{\sum X_i}{n}}\right] \\
&= \frac{1}{n}{\sum E[X_i]} \\
&= \frac{1}{n}n\mu \\
&= \mu \\
\end{aligned}
$$
{% endkatexmm %}

{% katexmm %}
$$\therefore \quad E[\bar{X}^2] = Var[\bar{X}] + E[\bar{X}]^2 =
\frac{\sigma^2}{n} - \mu^2 \qquad (3)
$$
{% endkatexmm %}
Thus, from (1), (2), (3),

{% katexmm %}
$$
\begin{aligned}
E[\hat{\sigma}^2] &= \frac{1}{n-1}\left(\sum_{i=1}^n E\left[ X_i^2 \right] - nE\left[ \bar{X}^2\right]\right) \\
&= \frac{1}{n-1}\left(\sum_{i=1}^n (\sigma^2 + \mu^2) - n\left(\frac{\sigma^2}{n} - \mu^2\right)\right) \\
&= \frac{1}{n-1}\left(n (\sigma^2 + \mu^2) - n\left(\frac{\sigma^2}{n} - \mu^2\right)\right) \\
&= \frac{1}{n-1}\left(n\sigma^2 + n\mu^2 - \sigma^2 - n\mu^2\right) \\
&= \frac{1}{n-1}(n - 1) \sigma^2 \\
&= \sigma^2 \\
\end{aligned}
$$
{% endkatexmm %}

{% katexmm %}
$$
\therefore \quad E[\hat{\sigma}^2] = \sigma^2
$$
{% endkatexmm %}

Since the sample variance with the denominator of $(n-1)$ is an unbiased estimator for the true variance $\sigma^2$, any other estimator with different denominator would be biased.

#### What about the sample mean?

Along the way to show the $\hat{\sigma}^2$ is unbiased, we've already shown why we don't apply the same logic for the sample mean $\bar{X}$. In ii), we derived that $\bar{X}$ is unbiased $E[\bar{X}] = \mu$ without any correction, unlike the sample variance.

## Implementations

In most cases, we don't explicitly calculate the sample variance. Instead, we call the implemented function from the numerical library we use. Thus, it is useful to know whether the function uses Bessel's correction or not, since it varies by the implementation details.

### Numpy
Numpy has the [`np.var`](https://numpy.org/doc/stable/reference/generated/numpy.var.html) method to calculate the variance of a given input. `np.var` returns the uncorrected variance, which is divided by $n$ unless you specify `ddof` argument. To get an unbiased sample variance, you have to add `ddof=1`. The `np.var` will return the result divided by `n-ddof`.
```python
import numpy as np
x = np.array([1,2,3])
np.var(x) # Divide by n where n = len(x)
np.var(x, ddof=1) # Divide by (n-1)
```

### Pandas
Pandas has a method in its DataFrame class, [`pd.DataFrame.var`](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.var.html). Unlike the `np.var`, `pd.DataFrame.var` returns the corrected sample variance with the denominator of $(n-1)$. This can also be changed by specifying the `ddof` argument as in `np.var`.
```python
import pandas as pd
x = pd.DataFrame([1,2,3])
x.var() # Divide by (n-1)
x.var(ddof=0) # Divide by n = (n-ddof)
```

### R
Standard function [`var`](https://www.rdocumentation.org/packages/cmvnorm/versions/1.0-7/topics/var) in R returns the unbiased sample variance with $(n-1)$ denominator. Unlike numpy and pandas, this behavior cannot be changed. Thus you should correct externally if you need to.

>These functions use $n−1$ on the denominator purely for consistency with `stats::var()` (for the record, I disagree with the rationale for $n−1$).
>-R Documentation-

```R
x <- rnorm(10)
n <- len(x)
var(x) # Divide by (n-1)
var(x) * (n-1) / n # Divide by n
```

## Conclusion

Now we know why we divide by $n-1$ instead of $n$ for the sample variance. However, this doesn't mean that you should always use Bessel's correction. As I mentioned in the beginning, Bessel's correction only works with the iid samples. And even for the iid samples, one might want to use a different estimator depending on the problem. Again, unbiasedness is just another good property to have. In fact, the uncorrected sample variance gives the Maximum Likelihood Estimator(MLE) when the samples are from iid normal. If one prefers the maximum likelihood over the unbiasedness, the uncorrected sample variance still gives a good estimation.
