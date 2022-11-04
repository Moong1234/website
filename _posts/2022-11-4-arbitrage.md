---
title: Arbitrage
subtitle: Definition and theorem related to an arbitrage
layout: default
date: 2022-11-4
keywords: finance, mathematics
summary: Notes on arbitrage
published: true
---
#### tags: `finance`, `mathematics`

# What is arbitrage?
We say there's an arbitrage if we can take some positive return without taking any risk by exploiting some market condition. We can define this notion in mathematical expression as follows.  
  
### Definition (Arbitrage)
For a portfolio that has value of $X_t$ at time $t \geq 0$,
there's an arbitrage if $\exists T > 0$ such that the following three conditions hold,

{% katexmm %}
$$
\begin{aligned}
1.\quad &X_0 = 0\\
2.\quad &X_T \geq 0 \quad \text{a.s.} \\
3.\quad &P(X_T > 0) > 0\\
\end{aligned}
$$
{% endkatexmm %}

The first condition indicates the portfolio does not require any initial investment. The second condition states that an event of the terminal value is non-negative happens with probability 1, i.e., $P(X_T \geq 0) = 1$. The third condition implies that the probability of the terminal portfolio value being positive is greater than 0. 

Thus, if there is a portfolio that requires zero initial investment but the terminal value will never be less than 0 and there's a chance to have a positive return, then we say there's an arbitrage opportunity.

### Definition (Equivalence of probability measures)
A probability measure $\mathbb{\tilde{P}}$ is said to be equivalent to some other probability measure $\mathbb{P}$, and denoted $\mathbb{P} \sim \mathbb{\tilde{P}}$ if they agree with the events that occur with probability 1. i.e.,  

{% katexmm %}
$$
\mathbb{P}(E) = 1 \iff \Bbb{\tilde{P}}(E) = 1
$$
{% endkatexmm %}


With the above definition of arbitrage and the notion of equivalent probability measure, we can derive some useful theorem as follows. 

### Theorem
If $X$ is arbitrage under some probability measure $\mathbb{P}$, then it is also arbitrage for any equivalent measure $\mathbb{\tilde{P}}$.  

#### Proof
Assume that $\mathbb{P} \sim \mathbb{\tilde{P}}$ and $X$ is arbitrage under $\mathbb{P}$ but not arbitrage under $\mathbb{\tilde{P}}$.  

If X is an arbitrage under $\mathbb{P}$, by the second condition of arbitrage, 
{% katexmm %}
$$X_T \geq 0 \quad \text{a.s.} \iff \Bbb{P}(X_T \geq 0) = 1$$
{% endkatexmm %}

 Since equivalent probability measure $\tilde{\mathbb{P}}$ agrees with the event that occurs with probability 1, we have, 
{% katexmm %}
$$
\mathbb{P}(X_T \geq 0) = 1 \iff \tilde{\mathbb{P}}(X_T \geq 0) = 1
$$    
{% endkatexmm %}

Since we know $\mathbb{\tilde{P}}(X_T \geq 0) = 1$, X is not an arbitrage if and only if when X violates the third condition under $\mathbb{\tilde{P}}$. That is, $\mathbb{\tilde{P}}(X_T > 0) = 0 \iff \mathbb{\tilde{P}}(X_T = 0) = 1$.  

However, the equivalent probability measures should agree on all events that occur with probability 1.  

Since we have $\mathbb{P}(X_T > 0) > 0 \iff \mathbb{P}(X_T = 0) \neq 1$, there is a contradiction.

# References 
{% bibliography --file 2022-11-4-arbitrage %}
