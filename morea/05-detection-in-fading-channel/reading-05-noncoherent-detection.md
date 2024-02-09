---
title: "Noncoherent detection in Rayleigh fading channels"
published: true
morea_id: reading-05-noncoherent-detection
morea_summary: "Performance degrades in fading channels"
# morea_url: https://github.com/airbnb/javascript
morea_type: reading
morea_labels:
morea_sort_order: 53
---

# Noncoherent detection in Rayleigh fading channels

We have learned that [BPSK fails in the Rayleigh fading channel](reading-05-awgn-vs-fading.html). Can we design a signaling scheme that works in the fading channel?

The reason that BPSK fails is that BPSK encodes information in the phase of the transmit signal, and that the fading channel can change the phase of the signal uniformly randomly. So a natural idea is to encode the information in the magnitude of the transmit signal. One example is the orthogonal signaling, defined as

$$
\mathbf{x}_A = \left(
  \begin{aligned} 
    x[0] \\ x[1]
  \end{aligned} 
\right)
 = \left(
  \begin{aligned} 
    a \\ 0
  \end{aligned} 
\right)
~~\text{and}~~
\mathbf{x}_B = \left(
  \begin{aligned} 
    x[0] \\ x[1]
  \end{aligned} 
\right)
 = \left(
  \begin{aligned} 
    0 \\ a
  \end{aligned} 
\right).
$$

In this signal scheme, we use two symbols $x[0]$ and $x[1]$ to represent one bit. The tuples $\mathbf{x}_A$ and $\mathbf{x}_B$ have different magnitudes in different time slots. 

The received signal is a tuple of two symbols

$$
\mathbf{y} = \left(
  \begin{aligned} 
    y[0] \\ y[1]
  \end{aligned} 
\right)
 = \left(
  \begin{aligned} 
    h[0] x[0] + w[0] \\ h[1] x[1] + w[1]
  \end{aligned} 
\right).
$$

If $\mathbf{x}_A$ was sent, since $x[1]=0$, it is more likely that $y[1]$ is close to zero. Therefore, we should be able to distinguish the two transmit signals by comparing the magnitudes of $y[0]$ and $y[1]$.

## Maximum likelihood detector

We derive the maximum likelihood detector in this case:

$$
\hat{\mathbf{x}} = \left\{ 
  \begin{aligned} 
    &\mathbf{x}_A, && \text{if } \mathbf{P}(\mathbf{y} \vert \mathbf{x}_A) \ge \mathbf{P}(\mathbf{y} \vert \mathbf{x}_B), \\ 
    &\mathbf{x}_B, && \text{if } \mathbf{P}(\mathbf{y} \vert \mathbf{x}_A) < \mathbf{P}(\mathbf{y} \vert \mathbf{x}_B).
  \end{aligned} 
\right.
$$

When $\mathbf{x}_A$ was sent, we have $y[0] \sim \mathcal{CN}(0, a^2 + N_0)$ and $y[1] \sim \mathcal{CN}(0, N_0)$. When $\mathbf{x}_B$ was sent, we have $y[0] \sim \mathcal{CN}(0, N_0)$ and $y[1] \sim \mathcal{CN}(0, a^2 + N_0)$. In addition, given $\mathbf{x}_A$ or $\mathbf{x}_B$, $y[0]$ and $y[1]$ are conditionally independent because the chanenl gains $h[0]$ and $h[1]$ are independent and the noises $w[0]$ and $w[1]$ are independent. Hence, the conditional probability density function can be written explicitly as

\begin{aligned} 
  \mathbf{P}(\mathbf{y} \vert \mathbf{x}_A) = \mathbf{P}(y[0] \vert \mathbf{x}_A) \cdot \mathbf{P}(y[1] \vert \mathbf{x}_A) = \frac{1}{\pi (a^2+N_0)} e^{-\frac{\vert y[0] \vert^2}{a^2+N_0}} \cdot \frac{1}{\pi N_0} e^{-\frac{\vert y[1] \vert^2}{N_0}},
\end{aligned} 

and

\begin{aligned} 
  \mathbf{P}(\mathbf{y} \vert \mathbf{x}_B) = \mathbf{P}(y[0] \vert \mathbf{x}_B) \cdot \mathbf{P}(y[1] \vert \mathbf{x}_B) = \frac{1}{\pi N_0} e^{-\frac{\vert y[0] \vert^2}{N_0}} \cdot \frac{1}{\pi (a^2+N_0)} e^{-\frac{\vert y[1] \vert^2}{a^2+N_0}}.
\end{aligned} 

Therefore, we have

$$
\begin{aligned} 
                  & \quad \mathbf{P}(\mathbf{y} \vert \mathbf{x}_A) > \mathbf{P}(\mathbf{y} \vert \mathbf{x}_B) \\
  \Leftrightarrow & \quad - \frac{\vert y[0] \vert^2}{a^2+N_0} - \frac{\vert y[1] \vert^2}{N_0} > - \frac{\vert y[0] \vert^2}{N_0} - \frac{\vert y[1] \vert^2}{a^2+N_0} \\
  \Leftrightarrow & \quad \vert y[0] \vert^2 > \vert y[1] \vert^2.
\end{aligned} 
$$

So the maximum likelihood detector has a simple decision rule:

$$
\hat{\mathbf{x}} = \left\{ 
  \begin{aligned} 
    &\mathbf{x}_A, && \text{if } \vert y[0] \vert^2 \ge \vert y[1] \vert^2, \\ 
    &\mathbf{x}_B, && \text{if } \vert y[0] \vert^2 < \vert y[1] \vert^2.
  \end{aligned} 
\right.
$$

The maximum likelihood detector is again very intuitive: we compare the energy of the two symbols. It is also called the *noncoherent detector* or the *energy detector*.

## Performance analysis

Now we analyze the error probability of such a detector. Again, due to symmetry, we can focus on the case where $\mathbf{x}_A$ was sent but the detector output $\mathbf{\hat{x}} = \mathbf{x}_B$.

$$
  \begin{aligned} 
    p_e = \mathbf{P}(\vert y[0] \vert^2 < \vert y[1] \vert^2 \vert \mathbf{x}_A).
  \end{aligned}
$$

Given that $\mathbf{x}_A$ was sent, $y[0]$ and $y[1]$ are circularly symmetric Gaussian random variables. Therefore, their energy $z[0]=\vert y[0] \vert^2$ and $z[1]=\vert y[1] \vert^2$ are exponentially distributed with means $a^2 + N_0$ and $N_0$, respectively. Therefore, the error probability is

$$
  \begin{aligned} 
    p_e = \int_{-\infty}^\infty \int_{-\infty}^{z_1} \left( \frac{1}{a^2+N_0} e^{-\frac{z_0}{a^2+N_0}} \right) \left( \frac{1}{N_0} e^{-\frac{z_1}{N_0}} \right) d z_0 d z_1 = \frac{1}{2 + a^2/N_0}.
  \end{aligned}
$$

In this signal scheme, the energy per transmit symbol is $\frac{a^2}{2}$, and the noise energy per symbol is $N_0$. Hence, the SNR is $\frac{a^2}{2 N_0}$. Therefore, the error probability can be rewritten as

$$
  p_e = \frac{1}{2(1 + \textsf{SNR})}.
$$

In summary, in the fading channel, the orthogonal signal scheme works, but **the error rate decays only linearly with the SNR**. In contrast, the error rate decays exponentially with the SNR in the AWGN channel.
