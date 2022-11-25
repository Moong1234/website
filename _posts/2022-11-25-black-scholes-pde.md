---
title: Deriving Black-Scholes Partial Differential Equation
subtitle: Derive Black-Scholes PDE with pricing by replication
layout: default
date: 2022-11-25
keywords: finance, mathematics
summary: Derive Black-Scholes PDE with pricing by replication
published: true
---
#### tags: `finance`, `mathematics`

## Black-Scholes Partial Differential Equation

Black-Scholes PDE or Black-Scholes equation is an equation that governs the dynamics of European option value under the Black-Scholes model. The equation is given by,

{% katexmm %}
$$
\frac{\partial v}{\partial t} + \frac{1}{2}\sigma^2 s^2\frac{\partial^2 v}{\partial s^2} + r s \frac{\partial v}{\partial s} - rv = 0 
$$
{% endkatexmm %}  
  
## Black-Scholes Model

$dS_t = \mu S_t dt + \sigma S_t dW_t$

$dB_t = rB_tdt$

where $(W_t)_{0\leq t\leq T}$ is a Brownian motion. \
\
\
I will use the following known facts without proof.

For infinitesimally small $dt$,

 $dW_t \sim  O(\sqrt{dt}) = O(dt^{1/2})$

$(dW_t)^2 =dt$

## Pricing by replication
Consider a European option with payoff $\varphi(S_T)$ at maturity $T$ that has its value of $V_t$ at time $t$.

Construct a portfolio $X$ that replicates the payoff of this European option.
i.e., $X_t = V_t$  
<br />

Let $X_t = \Delta_t S_t + \frac{X_t - \Delta_t S_t}{B_t}B_t$.

where $\Delta_t$ indicates the number of shares of stocks in the portfolio.  
<br />

If the value of $X_t$ only depends on the value of $S$ and $B$ then \
<br />
{% katexmm %}
$$
\begin{aligned}
dX_t &= \Delta_t dS_t + \frac{X_t - \Delta_t S_t}{B_t}dB_t \\
&= \Delta_t (\mu S_tdt + \sigma S_t dW_t) + \frac{X_t - \Delta_t S_t}{B_t}rB_tdt \\
&= \Delta_t (\mu S_tdt + \sigma S_t dW_t) + (X_t - \Delta_t S_t)rdt \\
&= \Delta_tS_t (\mu -r)dt + \Delta_t S_t \sigma dW_t + rX_tdt \\
\end{aligned}
$$
{% endkatexmm %}  
<br />
  
{% katexmm %}
$$
d\left(\frac{X_t}{B_t}\right) = d\left(X_t\cdot \frac{1}{B_t}\right) = dX_t \cdot \frac{1}{B_t} + X_t \cdot d\left(\frac{1}{B_t}\right) + dX_t d\left(\frac{1}{B_t}\right)
$$
{% endkatexmm %}
<br />

Note that by letting $f(B_t) = \frac{1}{B_t}$ , for an infinitesimally small increment $dt$, we have 

{% katexmm %}
$$
\begin{aligned}
d\left( \frac{1}{B_t}\right) = df(B_t) &= f'(B_t)dB_t + \frac{1}{2}f''(B_t)(dB_t)^2 \\
&= -\frac{1}{B_t^2} \cdot dB_t + O(dt^2) \\
&= -\frac{rB_tdt}{B_t^2} \\
&= -\frac{r}{B_t}dt
\end{aligned}
\\
$$
{% endkatexmm %}
<br />

{% katexmm %}
$$
\\
\begin{aligned}
d\left(\frac{X_t}{B_t}\right) &= dX_t \cdot \frac{1}{B_t} + X_t \cdot d\left(\frac{1}{B_t}\right) + dX_t d\left(\frac{1}{B_t}\right) \\
&= \frac{dX_t}{B_t} + X_t\left(-\frac{r}{B_t}dt\right) + dX_t \left(-\frac{r}{B_t}dt\right) \\
&= \frac{\Delta_tS_t (\mu -r)dt + \Delta_t S_t \sigma dW_t + rX_tdt }{B_t} - \frac{rX_t}{B_t}dt + O(dt^2 + dt^{3/2}) \\
&= \frac{\Delta_tS_t (\mu -r)dt + \Delta_t S_t \sigma dW_t + rX_tdt }{B_t} - \frac{rX_t}{B_t}dt \\
&=\frac{\Delta_tS_t}{B_t}(\mu-r)dt + \frac{\Delta_tS_t}{B_t}\sigma dW_t
\end{aligned}
$$
{% endkatexmm %}

---

Now consider the value of the European option at time $t$, $V_t.$

It is reasonable to assume that the value of a European option will only depend on time $t$ and the stock price $S_t$.

That is, assume  $V_t$$=v(t, S_t)$.

<br />
By using the multi-dimensional Ito’s lemma,

{% katexmm %}
$$
\begin{aligned}
dV_t &= dv(t, S_t) \\
&= \frac{\partial v}{\partial t}dt + \frac{\partial v}{\partial s} dS_t + \frac{1}{2}\frac{\partial^2 v}{\partial s^2}(dS_t)^2 \\
&= \frac{\partial v}{\partial t}dt + \frac{\partial v}{\partial s} (\mu S_t dt + \sigma S_t dW_t) + \frac{1}{2}\frac{\partial^2 v}{\partial s^2}(\mu S_t dt + \sigma S_t dW_t)^2 \\
&= \frac{\partial v}{\partial t}dt + \frac{\partial v}{\partial s} (\mu S_t dt + \sigma S_t dW_t) + \frac{1}{2}\frac{\partial^2 v}{\partial s^2}(\mu^2 S_t^2 (dt)^2 + \sigma^2 S_t^2 (dW_t)^2 + 2\mu\sigma S_t^2dtdW_t) \\ 
&= \frac{\partial v}{\partial t}dt + \frac{\partial v}{\partial s} (\mu S_t dt + \sigma S_t dW_t) + \frac{1}{2}\frac{\partial^2 v}{\partial s^2}(O(dt^2) + \sigma^2 S_t^2 dt + O(dt^{3/2})) \\ 
&= \frac{\partial v}{\partial t}dt + \frac{\partial v}{\partial s} \mu S_t dt + \frac{\partial v}{\partial s}\sigma S_t dW_t + \frac{1}{2}\frac{\partial^2 v}{\partial s^2}\sigma^2 S_t^2 dt \\ 
&= \left[\frac{\partial v}{\partial t} + \frac{\partial v}{\partial s} \mu S_t + \frac{1}{2}\frac{\partial^2 v}{\partial s^2}\sigma^2 S_t^2 \right] dt + \frac{\partial v}{\partial s} \sigma S_t dW_t \\
\end{aligned}
$$
{% endkatexmm %}
<br />

{% katexmm %}
$$
\begin{aligned}
d\left(\frac{V_t}{B_t}\right) &= d\left(V_t\cdot \frac{1}{B_t}\right) = dV_t \cdot \frac{1}{B_t} + V_t \cdot d\left(\frac{1}{B_t}\right) + dV_t d\left(\frac{1}{B_t}\right) \\
&= \frac{dV_t}{B_t} + V_t \left(-\frac{r}{B_t}dt\right) + dV_t d\left(\frac{1}{B_t}\right) \\
&= \frac{dV_t}{B_t} - \frac{rV_t}{B_t}dt + O(dt^2 +dt^{3/2}) \\
&= \frac{dV_t}{B_t} - \frac{rV_t}{B_t}dt + O(dt^2 +dt^{3/2}) \\
&= \frac{1}{B_t}(dV_t - rV_tdt) \\
&= \frac{1}{B_t}\left (\left[\frac{\partial v}{\partial t} + \frac{\partial v}{\partial s} \mu S_t + \frac{1}{2}\frac{\partial^2 v}{\partial s^2}\sigma^2 S_t^2 \right] dt + \frac{\partial v}{\partial s} \sigma S_t dW_t - rV_tdt \right) \\
&= \frac{1}{B_t}\left (\left[\frac{\partial v}{\partial t} + \frac{\partial v}{\partial s} \mu S_t + \frac{1}{2}\frac{\partial^2 v}{\partial s^2}\sigma^2 S_t^2 - rV_t \right] dt + \frac{\partial v}{\partial s} \sigma S_t dW_t \right)
\end{aligned}
$$
{% endkatexmm %}
<br />

Suppose $X_0 = V_0$ and $d\left(\frac{V_t}{B_t}\right) = d\left(\frac{X_t}{B_t}\right)$, then we have

$\frac{X_t}{B_t} = \frac{X_0}{B_0} + \int_0^td\left(\frac{X_t}{B_t}\right) = \frac{V_0}{B_0} + \int_0^td\left(\frac{V_t}{B_t}\right) = \frac{V_t}{B_t}$.

<br />

From $d\left(\frac{V_t}{B_t}\right) = d\left(\frac{X_t}{B_t}\right)$, 

{% katexmm %}
$$
d\left(\frac{V_t}{B_t}\right) - d\left(\frac{X_t}{B_t}\right) = 0\\
\frac{1}{B_t}\left (\left[\frac{\partial v}{\partial t} + \frac{\partial v}{\partial s} \mu S_t + \frac{1}{2}\frac{\partial^2 v}{\partial s^2}\sigma^2 S_t^2 - rV_t \right] dt + \frac{\partial v}{\partial s} \sigma S_t dW_t \right) - \left( \frac{\Delta_tS_t}{B_t}(\mu-r)dt + \frac{\Delta_tS_t}{B_t}\sigma dW_t \right)= 0 \\
\frac{1}{B_t}\left (\left[\frac{\partial v}{\partial t} + \frac{\partial v}{\partial s} \mu S_t + \frac{1}{2}\frac{\partial^2 v}{\partial s^2}\sigma^2 S_t^2 - rV_t - \Delta_tS_t(\mu-r)\right] dt + \left[\frac{\partial v}{\partial s} \sigma S_t - \Delta_tS_t\sigma  \right] dW_t \right) = 0 \\
\left[\frac{\partial v}{\partial t} + \frac{\partial v}{\partial s} \mu S_t + \frac{1}{2}\frac{\partial^2 v}{\partial s^2}\sigma^2 S_t^2 - rV_t - \Delta_tS_t(\mu-r)\right] dt + \left[\frac{\partial v}{\partial s} - \Delta_t \right] \sigma S_t dW_t = 0 \\
$$
{% endkatexmm %}
<br />

Choose $\Delta_t$ s.t. $\left[\frac{\partial v}{\partial s} - \Delta_t \right] \sigma S_t dW_t = 0$, i.e., $\Delta_t = \frac{\partial v}{\partial s}$.

{% katexmm %}
$$
\left[\frac{\partial v}{\partial t} + \frac{\partial v}{\partial s} \mu S_t + \frac{1}{2}\frac{\partial^2 v}{\partial s^2}\sigma^2 S_t^2 - rV_t -\frac{\partial v}{\partial s} S_t(\mu-r)\right] dt = 0 \\
\left[\frac{\partial v}{\partial t} + \frac{\partial v}{\partial s} \mu S_t + \frac{1}{2}\frac{\partial^2 v}{\partial s^2}\sigma^2 S_t^2 - rV_t -\frac{\partial v}{\partial s} S_t\mu + \frac{\partial v}{\partial s} S_t r \right] dt = 0 \\
\left[\frac{\partial v}{\partial t} + \frac{1}{2}\frac{\partial^2 v}{\partial s^2}\sigma^2 S_t^2 - rV_t + \frac{\partial v}{\partial s} S_t r \right] dt = 0 \\
\frac{\partial v}{\partial t} + \frac{1}{2}\frac{\partial^2 v}{\partial s^2}\sigma^2 s^2 - rv + \frac{\partial v}{\partial s} r s= 0
$$
{% endkatexmm %}
<br />

By rearranging the expression, we have the Black-Scholes Partial Differential Equation.

{% katexmm %}
$$
\frac{\partial v}{\partial t} + \frac{1}{2}\sigma^2 s^2\frac{\partial^2 v}{\partial s^2} + r s \frac{\partial v}{\partial s} - rv = 0 
$$
{% endkatexmm %}
