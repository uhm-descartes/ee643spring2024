---
title: "Complex Gaussian random variables"
published: true
morea_id: reading-05-complex-gaussian
morea_summary: "Everything you need to know about Gaussian"
# morea_url: https://github.com/airbnb/javascript
morea_type: reading
morea_labels:
morea_sort_order: 51
---

# Complex Gaussian random variables

<div class="alert alert-success" role="alert" markdown="1">
<i class="fa-solid fa-book fa-xl"></i> **Readings**
<hr/>

Most of the content in this page comes from [this excellent write-up by Robert G. Gallager](https://www.rle.mit.edu/rgallager/documents/CircSymGauss.pdf).
For a summary, please refer to Appendix A.1 of [the textbook](https://web.stanford.edu/~dntse/papers/book121004.pdf).
</div>

## Gaussian random variables

Gaussian random variables, or normal random variables, are one of the most important random variables.
We denote a real-valued Gaussian random variable $x$ by $\mathcal{N}(\mu, \sigma^2)$, where $\mathcal{N}$ means "normal", $\mu$ is the mean, and $\sigma^2$ is the variance. A Gaussian random variable is completely characterized by its mean and variance, as can be seen from its probability density function (PDF):
\begin{align}
  f(x) = \frac{1}{\sqrt{2 \pi \sigma^2}} e^{-\frac{(x-\mu)^2}{2 \sigma^2}}.
\end{align}

A *standard Gaussian* random variable is a Gaussian random variable with zero mean and unit variance, namely $w \sim \mathcal{N}(0,1)$. The *tail* of the standard Gaussian random variable $w$ is the *Q function*, defined as
\begin{align}
  Q(a) \triangleq \mathbf{P}(w > a) = \int_{a}^\infty \frac{1}{\sqrt{2 \pi}} e^{-\frac{w^2}{2}} dw.
\end{align}

We can convert any Gaussian random variable $x \sim \mathcal{N}(\mu, \sigma^2)$ to a standard Gaussian random variable by a linear transformation:
\begin{align}
  \frac{x - \mu}{\sigma} \sim \mathcal{N}(0,1).
\end{align}
Therefore, any probability involving linear inequalities of a Gaussian random variable can be expressed in terms of the Q function. For example, we have
\begin{align}
  \mathbf{P}(x > b) = \mathbf{P}\left( \frac{x - \mu}{\sigma} > \frac{b - \mu}{\sigma} \right) = Q\left( \frac{b - \mu}{\sigma} \right).
\end{align}

The Q function is so useful that most scientific computing packages implement it (e.g., [```scipy.stats.norm.sf```](https://docs.scipy.org/doc/scipy/reference/generated/scipy.stats.norm.html) in Python).

A useful upper bound of the Q function is 
\begin{align}
  Q(a) < e^{-\frac{a^2}{2}},~~\forall~a>0,
\end{align}
where means that $Q(a)$ decays very fast (faster than exponential decay).

## Complex Gaussian random variables
A general complex Gaussian random variable $x$ is a random variable whose real part $\mathfrak{R}(x)$ and imaginary part $\mathfrak{I}(x)$ are both Gaussian random variables. This is a very general definition, because the real part and the imaginary part can be correlated in any way. For example, they can be perfectly correlated, namely they always take the same random value. 

We focus on a special class of complex Gaussian random variable, called *circularly symmetric Gaussian* random variable $\mathcal{CN}(0,\sigma^2)$. A circularly symmetric Gaussian random variable $x$ has the following properties:
* Its real part and its imaginary part are independently identically distributed (i.i.d.) Gaussian random variables $\mathcal{N}\left(0, \frac{\sigma^2}{2}\right)$.
* Its phase is *uniform* in $[0, 2\pi]$ and is independent of its magnitude $r = \vert x \vert$, which follows the *Rayleigh* distribution.
* The square of its magnitude follows the exponential distribution with mean $\sigma^2$.
* It is invariant to rotation, namely $e^{j\theta} x$ has the same distribution of $x$ for any $\theta$. This property is where the name "circularly symmetric" comes from.

The PDF of a circularly symmetric Gaussian random variable $\mathcal{CN}(0,\sigma^2)$ is
\begin{align}
  f(x) = \frac{1}{\pi \sigma^2} e^{-\frac{\vert x \vert^2}{\sigma^2}}.
\end{align}
