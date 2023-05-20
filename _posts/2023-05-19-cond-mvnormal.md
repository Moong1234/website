---
title: Deriving conditional multivariate normal distribution
subtitle: Conditional distribution when multivariate normal random vector is conditioned on its partition.
layout: default
date: 2023-05-19
keywords: statistics, mathematics
summary: Conditional distribution when multivariate normal random vector is conditioned on its partition.
published: true
---

#### tags: `statistics`, `mathematics`

Let random vector $\mathbf{x}$ follows a multivariate normal distribution $\mathbf{x} \sim N(\boldsymbol{\mu}, \boldsymbol{\Sigma})$. Consider the conditional distribution of $\mathbf{x_1}\vert\mathbf{x_2}$ where $\mathbf{x_1}$ and $\mathbf{x_2}$ are partitions of the random vector $\mathbf{x}$. We first create partitions as follows.

{% katexmm %}
$$
\mathbf{x} = \begin{bmatrix}
\mathbf{x_1}\\
\mathbf{x_2}
\end{bmatrix}
\qquad
\boldsymbol{\mu} = \begin{bmatrix}
\mathbf{\mu_1}\\
\mathbf{\mu_2}
\end{bmatrix}
\qquad
\boldsymbol{\Sigma}=
\begin{bmatrix}
\Sigma_{11} &\Sigma_{12} \\
\Sigma_{21} &\Sigma_{22}
\end{bmatrix}
$$
{% endkatexmm %}

Then, $\mathbf{x_1} \vert \mathbf{x_2} \sim N(\tilde{\boldsymbol{\mu}}, \tilde{\boldsymbol{\Sigma}})$ where $\tilde{\boldsymbol{\mu}}$ and $\tilde{\boldsymbol{\Sigma}}$ is given by,

{% katexmm %}
$$
\tilde{\boldsymbol{\mu}} = \mu_1 + \Sigma_{12}\Sigma_{22}^{-1}(\mathbf{x_2} -
\boldsymbol{\mu}_2) \\
$$
{% endkatexmm %}
{% katexmm %}
$$
\tilde{\boldsymbol{\boldsymbol{\Sigma}}} = \Sigma_{11} - \Sigma_{12}\Sigma_{22}^{-1}\Sigma_{21}
$$
{% endkatexmm %}

# Proof
It is known that conditional distribution of multivaritate normal, conditioned on
a subset of variables are again multivariate normal. Thus, we can verify the
above theorem by deriving the conditional mean and covariace.
Assuming $\Sigma_{22}$ is invertible, define a new variable $\mathbf{z} = \mathbf{x_1} + A\mathbf{x_2}$, where $A = -\Sigma_{12}\Sigma_{22}^{-1}$.

First notice that $\mathbf{z}$ and $\mathbf{x_2}$ has zero covariance,
{% katexmm %}
$$
\newcommand{\cov}{\text{Cov}}
\newcommand{\var}{\text{Var}}
\newcommand{\A}{-\Sigma_{12}\Sigma_{22}^{-1}}
\newcommand{\bv}[1]{\mathbf{#1}}
\begin{aligned}
\cov(\bv{z},\ \bv{x}_2) &= \cov(\bv{x}_1 + A\bv{x}_2,\ \bv{x}_2) \\
&= \cov(\bv{x}_1,\ \bv{x}_2) + \cov(A\bv{x}_2, \bv{x}_2) \\
&= \cov(\bv{x}_1,\ \bv{x}_2) + A\cov(\bv{x}_2, \bv{x}_2) \\
&= \Sigma_{12} + A\Sigma_{22} \\
&= \Sigma_{12} + \A\Sigma_{22} \\
&= \Sigma_{12} - \Sigma_{12} \\
&= 0 \\
\end{aligned}
$$
{% endkatexmm %}

Since $\mathbf{z}$ and $\mathbf{x}$ are jointly normal and uncorrelated, they
are independent by the property of mulitvariate normal. Now we can easily find
the conditional mean as follows.

{% katexmm %}
$$
\newcommand{\cov}{\text{Cov}}
\newcommand{\var}{\text{Var}}
\newcommand{\A}{-\Sigma_{12}\Sigma_{22}^{-1}}
\newcommand{\bv}[1]{\mathbf{#1}}
\newcommand{\ind}{\perp \!\!\! \perp}
\begin{aligned}
E(\bv{x}_1 \vert \bv{x}_2) &= E(\bv{z} - A\bv{x}_2 \vert \bv{x}_2) \\
&= E(\bv{z}\vert \bv{x}_2) - AE(\bv{x}_2 \vert \bv{x}_2) \\
&= E(\bv{z}) - A\bv{x}_2 \qquad (\because \bv{x}_2 \ind \bv{z}) \\
&= E(\bv{x}_1 + A\bv{x}_2) - A\bv{x}_2 \\
&= E(\bv{x}_1) + AE(\bv{x}_2) - A\bv{x}_2 \\
&= \bv{\mu}_1 + A\bv{\mu}_2 - A\bv{x}_2 \\
&= \bv{\mu}_1 - A(\bv{x}_2 - \bv{\mu}_2)\\
&= \bv{\mu}_1 + \Sigma_{12}\Sigma_{22}^{-1}(\bv{x}_2 - \bv{\mu}_2)\\
&= \tilde{\boldsymbol{\mu}}\\
\end{aligned}
$$
{% endkatexmm %}

Before jumping into conditional variance. Recall the following facts for random
vectors $\mathbf{x},\ \mathbf{y}$ and non-random matrix $A, B$, 

{% katexmm %}
$$
\newcommand{\cov}{\text{Cov}}
\newcommand{\var}{\text{Var}}
\newcommand{\bv}[1]{\mathbf{#1}}
\begin{aligned}
\var(\bv{x} + \bv{y}) &= \var(\bv{x}) + \var(\bv{y}) + \cov(\bv{x},\ \bv{y}) +
\cov(\bv{y},\ \bv{x}) \\
\cov(A\bv{x}, B\bv{y}) &= A\cov(\bv{x}, \bv{y})B^T
\end{aligned}
$$
{% endkatexmm %}

Using the above fact, we can expand the conditional variance as follows.

{% katexmm %}
$$
\newcommand{\cov}{\text{Cov}}
\newcommand{\var}{\text{Var}}
\newcommand{\A}{-\Sigma_{12}\Sigma_{22}^{-1}}
\newcommand{\bv}[1]{\mathbf{#1}}
\newcommand{\ind}{\perp \!\!\! \perp}
\begin{aligned}
\var(\bv{x}_1 \vert \bv{x}_2) &= \var(\bv{z} - A\bv{x}_2 \vert \bv{x}_2) \\
&= \var(\bv{z} \vert \bv{x}_2) + \var(- A\bv{x}_2 \vert \bv{x}_2) + \cov(\bv{z}
,\ - A\bv{x}_2 \vert \bv{x}_2) + \cov(- A\bv{x}_2,\ \bv{z} \vert \bv{x}_2) \\
\end{aligned}
$$
{% endkatexmm %}

Since $-A\mathbf{x}_2 \vert \mathbf{x}_2$ is not random anymore given
$\mathbf{x}_2$, we are only left with the first term.
  
{% katexmm %}
$$
\newcommand{\cov}{\text{Cov}}
\newcommand{\var}{\text{Var}}
\newcommand{\A}{\Sigma_{12}\Sigma_{22}^{-1}}
\newcommand{\bv}[1]{\mathbf{#1}}
\newcommand{\ind}{\perp \!\!\! \perp}
\begin{aligned}
&= \var(\bv{z} \vert \bv{x}_2) \\
&= \var(\bv{z})  \qquad (\because \bv{x}_2 \ind \bv{z}) \\
&= \var(\bv{x}_1 + A \bv{x}_2)\\
&= \var(\bv{x}_1) + \var(A \bv{x}_2) + \cov(\bv{x}_1,\ A \bv{x}_2) + \cov(A \bv{x}_2,\ \bv{x}_1)\\
&= \var(\bv{x}_1) + A\var(\bv{x}_2)A^T + \cov(\bv{x}_1,\ \bv{x}_2)A^T + A\cov(\bv{x}_2,\ \bv{x}_1)\\
&= \Sigma_{11} + A\Sigma_{22}A^T + \Sigma_{12}A^T + A\Sigma_{21}\\
&= \Sigma_{11} - A\Sigma_{22} (\A)^T + A\Sigma_{21} + A\Sigma_{21} \\
&= \Sigma_{11} - A\Sigma_{22} \Sigma_{22}^{-1}\Sigma_{21} + 2A\Sigma_{21} \\
&= \Sigma_{11} - A\Sigma_{21} + 2A\Sigma_{21} \\
&= \Sigma_{11} + A\Sigma_{21} \\
&= \Sigma_{11} - \A \Sigma_{21} \\
&= \tilde{\boldsymbol{\Sigma}} \\
\end{aligned}
$$
{% endkatexmm %}

Therefore, the proof is done. 

# References
{% bibliography --file 2023-05-19-cond-mvnormal %}
