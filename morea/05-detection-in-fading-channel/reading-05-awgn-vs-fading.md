---
title: "AWGN vs fading channels"
published: true
morea_id: reading-05-awgn-vs-fading
morea_summary: "A failed attempt in the fading channel"
# morea_url: https://github.com/airbnb/javascript
morea_type: reading
morea_labels:
morea_sort_order: 52
---

# AWGN channel versus fading channel

The input/output model of a wired channel is usualy modeled as an additive white Gaussian noise (AWGN) channel, namely

\begin{align}
  y[m] = x[m] + w[m],
\end{align}
where $w[m] \sim \mathcal{CN}(0, N_0)$ is a circularly symmetric Gaussian random variable. It is reasonable to assume that the noises over different time slots are independent (i.e., "white").

In contrast, the input/output model of a wireless Rayleigh fading channel with only one path is

\begin{align}
  y[m] = h[m] x[m] + w[m],
\end{align}
where $h[m]$ is a circularly symmetric Gaussian random variable. Therefore, the channel has a magnitude following the Rayleigh distribution, and a phase following a uniform distribution in $[0, 2\pi]$.

Next, we use a simple signaling scheme, binary phase-shift keying (BPSK), to illustrate the key differences of the AWGN channel and the Rayleigh fading channel.


## Performance in the AWGN channel

In BPSK, we assign the binary bits of 0 and 1 to $x[m]=-a$ and $x[m]=+a$, respectively. Our goal is to determine which signal was sent base on the received signal $y[m] = x[m] + w[m]$. Therefore, we need to derive the optimal detection rule. 

### Maximum likelihood detector

A commonly-used principle of a detector is to maximize the likelihood, namely the conditional probability $\mathbf{P}(y[m] \vert x[m])$ of the received signal $y[m]$. Specifically, denoting the estimate of the transmit signal by $\hat{x}[m]$, the maximum likelihood detector is

$$
\hat{x}[m] = \left\{ 
  \begin{aligned} 
    &+a, && \text{if } \mathbf{P}(y[m] \vert x[m]=+a) \ge \mathbf{P}(y[m] \vert x[m]=-a), \\ 
    &-a, && \text{if } \mathbf{P}(y[m] \vert x[m]=+a) < \mathbf{P}(y[m] \vert x[m]=-a).
  \end{aligned} 
\right.
$$

When $x[m]=+a$, we have $y[m] - a \sim \mathcal{CN}(0, N_0)$, and when $x[m]=-a$, we have $y[m] + a \sim \mathcal{CN}(0, N_0)$. Hence, the conditional probability density function can be written explicitly as

\begin{aligned} 
  \mathbf{P}(y[m] \vert x[m]=+a) = \frac{1}{\pi N_0} e^{-\frac{\vert y[m] - a \vert^2}{N_0}} && \text{and} && \mathbf{P}(y[m] \vert x[m]=-a) = \frac{1}{\pi N_0} e^{-\frac{\vert y[m] + a \vert^2}{N_0}}.
\end{aligned} 

Therefore, we have

$$
\begin{aligned} 
                  & \quad \mathbf{P}(y[m] \vert x[m]=+a) > \mathbf{P}(y[m] \vert x[m]=-a) \\
  \Leftrightarrow & \quad \vert y[m] - a \vert^2 < \vert y[m] + a \vert^2 \\
  \Leftrightarrow & \quad \mathfrak{R}(y[m])^2 - 2 a \mathfrak{R}(y[m]) + a^2 + \mathfrak{I}(y[m])^2 < \mathfrak{R}(y[m])^2 + 2 a \mathfrak{R}(y[m]) + a^2 + \mathfrak{I}(y[m])^2 \\
  \Leftrightarrow & \quad \mathfrak{R}(y[m]) > 0
\end{aligned} 
$$

Then the detection rule can be simplified into

$$
\hat{x}[m] = \left\{ 
  \begin{aligned} 
    &+a, && \text{if } \mathfrak{R}(y[m]) \ge 0, \\ 
    &-a, && \text{if } \mathfrak{R}(y[m]) < 0.
  \end{aligned} 
\right.
$$

The optimal detection rule is also very intuitive. Since the signal $x[m] = \pm a$ is real-valued, we only need to check the real part of the received signal $\mathfrak{R}(y[m])$. If it is positive, it is more likely that $+a$ was sent.

### Performance analysis

Sometimes the noise is so large that even when $x[m]=-a$ was sent, the received signal $y[m]$ is positive. In this case, the detector would incorrectly conclude that $+a$ was sent. Now we analyze the chance of such an error happenning.

Since the signaling scheme of $x[m]=\pm a$ and the noise are both symmetric, the total probability of error is the same as the probability that the detector mistakens $-a$ for $+a$. So we can focus on this case. 

$$
  \begin{aligned} 
    p_e = \mathbf{P}(\mathfrak{R}(y[m]) > 0 \vert x[m]=-a) = \mathbf{P}\left( \frac{\mathfrak{R}(y[m])+a}{\sqrt{N_0/2}} > \frac{a}{\sqrt{N_0/2}} \right) = Q\left( \frac{a}{\sqrt{N_0/2}} \right),
  \end{aligned}
$$

where we use the fact that $\mathfrak{R}(y[m]) \sim \mathcal{N}(-a, N_0/2)$ when $-a$ was sent, and convert $\mathfrak{R}(y[m])$ to a standard Gaussian random variable $\frac{\mathfrak{R}(y[m])+a}{\sqrt{N_0/2}}$.

Now we introduce the important concept of **signal-to-noise ratio (SNR)**, defined as 

$$
\textsf{SNR} = \frac{\text{the average received signal energy per symbol}}{\text{noise energy per symbol}}.
$$

In BPSK, the SNR is $\frac{a^2}{N_0}$. Therefore, the error probability can be rewritten as

$$
  p_e = Q\left( \sqrt{2 \textsf{SNR}} \right).
$$

Since the Q function is upper bounded by $Q(x) < e^{-x^2/2}$, we have

$$
  p_e < e^{-\textsf{SNR}}.
$$

Therefore, **in the AWGN channel, the error rate decays exponentially with the SNR.**

## BPSK fails in the fading channel

How about the fading channel? In a Rayleigh fading channel, we have 

\begin{align}
  y[m] = h[m] x[m] + w[m],
\end{align}
where $h[m] \sim \mathcal{CN}(0,1)$.

When $x[m]=+a$ was sent, the receive signal $y[m] \sim \mathcal{CN}(0, a^2 + N_0)$, and when $x[m]=-a$ was sent, the receive signal $y[m] \sim \mathcal{CN}(0, a^2 + N_0)$. In other words, *the received signal follows the same distribution no matter which symbol was sent!* Therefore, we actually cannot tell which signal was sent from the receive signal. The root cause is that the channel can rotate the phase of the received signal uniformly randomly.

The failure of BPSK in the fading channel underscores the challenges when the channel is wireless.
