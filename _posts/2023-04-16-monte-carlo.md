---
title: Importance Sampling and Black Magic of Monte Carlo
subtitle: notes on Importance Sampling and Exponential Smoothing
layout: default
date: 2023-04-16
keywords: mathematics
summary: Introduce a motivating examples of Importance Sampling in the univariate case and stochastic process.
published: true
---

#### tags: `mathematics`


# Monte Carlo method
The Monte Carlo method is a computational method that approximates the target value by repetitive random sampling. The goal of the method is to evaluate a function $g(X)$ where $X$ is some random quantity. One naive approach is generating random samples, $X_1, X_2, ... X_n$, from computer simulation using pseudo-random number generation, and taking the average of evaluated $g(X_i)$. That is,
{% katexmm %}
$$
E[g(X)] \approx \frac{1}{n} \sum_{i=1}^{n} X_i
$$
{% endkatexmm %}
This is called the direct sampling method and is indeed powerful in many
settings. However, it has a severe shortcoming when the function is related to the
occurrence of rare events. Let's assume we have a standard normal random
variable $X\sim N(0, 1)$ and want to evaluate a function $g(X) = \mathbb{1}(X >
30)$. Note that $E[\mathbb{1}(X > 30)] = P(X > 30)$ so we know that the
analytical solution of this problem is not zero. And also, notice that the
direct estimation is essentially just counting the number of samples greater
than 30 and calculating the frequency of that event. 

Fortunately, we can easily generate standard normal samples using the Box-Muller algorithm, but it is almost impossible to get a sample greater than 30. Our direct MC estimate will indicate 0 until we get a single observation greater than 30, which will require a tremendous amount of samples unless we are very lucky. Even though we observe a desired sample with a meager chance, the variance of the estimation, hence the efficiency of the method, would still be poor.

# Importance Sampling
## Univariate case
One way to address this issue is using the Importance Sampling method. With the following simple algebra, we can convert the estimation to one that is amazingly more efficient than the direct method. 
{% katexmm %}
$$
\begin{aligned}
E[g(X)] &= \int_{-\infty}^{\infty} g(x)f_X(x)dx \\
&= \int_{-\infty}^{\infty} g(x) \frac{1}{\sqrt{2\pi}}\exp\left(-\frac{x^2}{2}\right)dx \\
&= \int_{-\infty}^{\infty} g(x) \frac{1}{\sqrt{2\pi}}\exp\left(-\frac{x^2}{2}+\mu x -\frac{\mu^2}{2} -\mu x + \frac{\mu^2}{2}\right)dx \\
&= \int_{-\infty}^{\infty} g(x) \frac{1}{\sqrt{2\pi}}\exp\left(-\frac{(x - \mu)^2}{2} -\mu x + \frac{\mu^2}{2}\right)dx \\
&= \int_{-\infty}^{\infty} g(x) \frac{1}{\sqrt{2\pi}}\exp\left(-\frac{(x - \mu)^2}{2}\right) \exp\left( -\mu x + \frac{\mu^2}{2}\right)dx \\
&= \int_{-\infty}^{\infty} g(x) \exp\left( -\mu x + \frac{\mu^2}{2}\right) f_{X'}(x) dx \quad \text{where } X' \sim N(\mu, 1)\\
&= E\left[g(X') \exp\left( -\mu X' + \frac{\mu^2}{2}\right)\right]\\
&\approx \frac{1}{n}\sum_{i=1}^n\left\{g(x'_i)\exp\left(-\mu x'_i + \frac{\mu^2}{2}\right)\right\}
\end{aligned}
$$
{% endkatexmm %}
Here, we're sampling from a shifted normal variable $X'$, evaluate $g$ with samples $x_i'$ and do a correction by multiplying $\exp\left(-\mu x'_i + \frac{\mu^2}{2}\right)$ to retrieve the original target value. If we choose a $\mu = 30$, we can easily sample $x'>30$ and this significantly improves the quality of the Monte Carlo estimate.

## Exponential Smoothing
It turns out that there is a direct analog of this approach for the Multivariate case and even for the stochastic process, called Exponential Smoothing. For example, let's consider the following Brownian Motion(BM) with drift. 
{% katexmm %}
$$
X_t = B_t + \mu t \quad t \geq 0
$$
{% endkatexmm %}
and we have discrete time points s.t. $0=t_0 < t_1< \cdots < t_n = T$.

Similar to the Univariate case, our objective is to evaluate the expectation, $E[f(X_{t_1}, X_{t_2}, \dots, X_{t_n})]$, where $f: \mathbb{R}^n \rightarrow \mathbb{R}$ is a bounded Borel function. Notice that since $B_t$ is BM, $X_t$ has independent increments. Let $x_0 = 0$, and $g: \mathbb{R}^n \rightarrow \mathbb{R}$ s.t. $f(x_1, x_2, \dots, x_n) = g(x_1 - x_0, x_2-x_1, \cdots, x_n - x_{n-1})$
Because of the independent increments, the joint density is a product of the marginal probability of the increments $X_i - X_{i-1}$, which is given by. 
{% katexmm %}
$$
\begin{aligned}
X_i - X_{i-1} &= B_{t_i} + \mu t_i - B_{t_{i-1}} - \mu t_{i-1} \\
&= B_{t_i} - B_{t_{i-1}} + \mu (t_i - t_{i-1}) \\
\end{aligned}
$$
{% endkatexmm %}
Since $B_{t_i} - B_{t_{i-1}} \sim N(0,\ t_i - t_{i-1})$, $X_i - X_{i-1} \sim N(\mu(t_i - t_{i-1}),\ t_i - t_{i-1})$. Then the joint pdf is given by, 
{% katexmm %}
$$
\prod_{i=1}^n \frac{1}{\sqrt{2\pi}\sqrt{t_i - t_{i-1}}} \exp\left(- \frac{((x_i - x_{i-1}) - \mu(t_i - t_{i-1}))^2}{2(t_i - t_{i-1})}\right)
$$
{% endkatexmm %}
We can separate the constant term of
{% katexmm %}
$$
C = (2\pi) ^{-n/2}\cdot \left( t_1-t_{0}\right) ^{-1/2}\cdot \left( t_{2}-t_{1}\right) ^{-1/2} \ldots \left( t_{n}-t_{n-1}\right) ^{-1/2}
$$
{% endkatexmm %}
and the remaining exponent part,
{% katexmm %}
$$
\begin{aligned}
& \prod_{i=1}^n \exp\left(- \frac{((x_i - x_{i-1}) - \mu(t_i - t_{i-1}))^2}{2(t_i - t_{i-1})}\right)\\ 
=& \prod_{i=1}^n \exp\left(- \frac{(x_i - x_{i-1})^2 -2(x_i - x_{i-1})\mu(t_i - t_{i-1}) + \mu^2(t_i - t_{i-1})^2}{2(t_i - t_{i-1})}\right) \\
=& \prod_{i=1}^n \exp\left(- \frac{(x_i - x_{i-1})^2}{2(t_i - t_{i-1})}  +(x_i - x_{i-1})\mu - \frac{\mu^2}{2}(t_i - t_{i-1})\right) \\
=& \prod_{i=1}^n \exp\left(- \frac{(x_i - x_{i-1})^2}{2(t_i - t_{i-1})}\right) \exp\left((x_i - x_{i-1})\mu - \frac{\mu^2}{2}(t_i - t_{i-1})\right) \\
=& \prod_{i=1}^n \exp\left(- \frac{(x_i - x_{i-1})^2}{2(t_i - t_{i-1})}\right) \prod_{i=1}^n \exp\left((x_i - x_{i-1})\mu - \frac{\mu^2}{2}(t_i - t_{i-1})\right) \\
=& \left\{\prod_{i=1}^n \exp\left(- \frac{(x_i - x_{i-1})^2}{2(t_i - t_{i-1})}\right)\right\} \exp\left(\sum_{i=1}^n(x_i - x_{i-1})\mu - \frac{\mu^2}{2}(t_i - t_{i-1})\right) \\
=& \left\{\prod_{i=1}^n \exp\left(- \frac{(x_i - x_{i-1})^2}{2(t_i - t_{i-1})}\right)\right\} \exp\left(\mu\sum_{i=1}^n (x_i - x_{i-1}) - \frac{\mu^2}{2} \sum_{i=1}^n (t_i-t_{i-1})\right) \\
=& \left\{\prod_{i=1}^n \exp\left(- \frac{(x_i - x_{i-1})^2}{2(t_i - t_{i-1})}\right)\right\} \exp\left(\mu x_n - \frac{1}{2}\mu^2 t_n\right) 
\end{aligned}
$$
{% endkatexmm %}

Note that $C \left\lbrace \prod_{i=1}^n \exp\left(- \frac{(x_i - x_{i-1})^2}{2(t_i - t_{i-1})}\right)\right\rbrace $ is the joint density of $(B_{t_1}- B_{t_0}, \ B_{t_2}- B_{t_1}, \cdots,\ B_{t_n}-B_{t_{n-1}})$.
Then we can convert the original expectation as follows. 

{% katexmm %}
$$
E[f(X_{t_1}, X_{t_2}, \dots, X_{t_n})] = E\left[f(B_{t_1}, B_{t_2}, \dots, B_{t_n}) \exp\left(\mu B_T - \frac{1}{2}\mu^2 T\right)\right]
$$
{% endkatexmm %}


As in the Univariate case, we have converted the expection with respect to $B_t$ instead of $X_t$, evaluate $f(\cdot)$, then do a correction by multiplying $\exp\left(\mu B_T - \frac{1}{2}\mu^2 T\right)$. One interesting fact is that the correction term $M_t = \exp\left(\mu B_t - \frac{1}{2}\mu^2 t\right)$ is a martingale.
{% katexmm %}
$$
\newcommand{\indep}{\perp \!\!\! \perp}
\begin{aligned}
E[M_t|\mathcal{F_s}] &= E\left[\exp\left(\left.\mu B_t - \frac{1}{2}\mu^2 t\right)\right|\mathcal{F_s}\right] \\
&= E\left[\exp\left(\left.\mu B_t - \mu B_s + \mu B_s - \frac{1}{2}\mu^2 (t-s) - \frac{1}{2}\mu^2 s \right)\right|\mathcal{F_s}\right] \\
&= E\left[\exp\left(\mu B_s - \frac{1}{2}\mu^2 s\right) \exp\left(\left.\mu (B_t - B_s) - \frac{1}{2}\mu^2 (t-s)  \right)\right|\mathcal{F_s}\right] \\
&= M_s E\left[\exp\left(\mu (B_t - B_s) - \frac{1}{2}\mu^2 (t-s)  \right)\right] \quad \because\ B_t - B_s \indep \mathcal{F_s} \\
&= M_s E\left[\exp\left(\mu (B_t - B_s)\right) \exp\left(- \frac{1}{2}\mu^2 (t-s)  \right)\right] \\
&= M_s \exp\left(- \frac{1}{2}\mu^2 (t-s)  \right) E\left[\exp\left(\mu Y\right) \right] \quad \text{where } Y\sim N(0,\ t-s) \\
\\
\text{Notice }&E\left[\exp\left(\mu Y\right) \right] \text{ is the MGF of }Y \\
\\
&= M_s \exp\left(- \frac{1}{2}\mu^2 (t-s) \right) \exp\left(\frac{1}{2}\mu^2 (t-s) \right)  \\
&= M_s
\end{aligned}
$$
{% endkatexmm %}

# Change of measure
In the previous example, while we were deriving the joint pdf of the process, we only did algebra and used some trivial properties of BM. Surprisingly, however, we ended up having the martingale correction term $M_t$. It further turns out that $M_t$ coincides with the Radon-Nikodym derivative we get if we apply Girsanov's theorem to the same problem.
