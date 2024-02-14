---
title: "Performance gain from time diversity"
published: true
morea_id: reading-06-performance-gain-time-diversity
morea_summary: "Diversity in time improves the performance"
# morea_url: https://github.com/airbnb/javascript
morea_type: reading
morea_labels:
morea_sort_order: 61
---

# Performance gain from time diversity

From [the previous module](../05-detection-in-fading-channel/reading-05-coherent-detection.html/), we realize the fundamental difference in the performance under the additive white Gaussian noise (AWGN) channels and the wireless fading channels. More specifically, the bit error rate (BER) decays exponentially with the signal-to-noise ratio (SNR), namely $p_e <  e^{-\textsf{SNR}}$, in the AWGN channel, while it decays only linearly, namely $p_e = \mathcal{O}\left(\frac{1}{\textsf{SNR}}\right)$ in the wireless fading channel. 

How can we improve the performance under wireless channels? We know that the reason for the performance degradation is deep fading, where the channel gain is so small that the received signal is at the same energy level of the noise. But the channel is changing over time, and deep fading happens with certain probability. If we send multiple copies of the transmit signal over time, it is more likely that some of the copies do not experience deep fading. This is the idea of **time diversity**.

## Performance of repetition coding

To get the insight of how time diversity works, we consider a simple case of *repetition code*. Specifically, we send $L$ copies of a transmit signal $x$, namely

$$
\mathbf{y}  = \left[ \begin{array}{c} y_1 \\ \vdots \\ y_L \end{array} \right] 
            = \left[ \begin{array}{c} h_1 x + w_1 \\ \vdots \\ h_L x + w_L \end{array} \right] 
            = \mathbf{h} \cdot x + \mathbf{w},
$$

where $x = \pm a$ is the symbol in binary phase shift keying (BPSK), $\mathbf{h} \in \mathbb{C}^L$ is the channel vector, and $\mathbf{w} \in \mathbb{C}^L$ is the noise vector. We assume that each channel gain $h_\ell$ are independent and follows the Rayleight distribution $h_\ell \sim \mathcal{CN}(0,1)$, and that each noise $w_\ell$ are independent and follows the Rayleight distribution $w_\ell \sim \mathcal{CN}(0,N_0)$.

We can assume that we know the channel gains $\mathbf{h}$ in these $L$ time slots perfectly. Then we can perform *coherent detection* of the transmit symbol $x$.

### Detection in a complex vector space

Before analyzing the repetition coding, we can quantify the performance of detection in a general complex vector space. The results can be applied to special cases later, including the case of BPSK under repetition coding.

Consider a signal scheme where the binary bits are mapped to two signals in a complex vector space, denoted by $\mathbf{u}_A \in \mathbb{C}^{L}$ and $\mathbf{u}_B \in \mathbb{C}^{L}$. The received signal is

$$
\mathbf{y} = \mathbf{u} + \mathbf{w},
$$

where $\mathbf{w} \sim \mathcal{CN}(\boldsymbol{0}, N_0 \mathbf{I}_L)$, and $\mathbf{I}_L$ is the $L \times L$ identify matrix.

The maximum likelihood detector compares the conditional probability density function (PDF) of the received signal given the transmit signal, namely 

$$
\hat{\mathbf{u}} = \left\{ 
  \begin{aligned} 
    &\mathbf{u}_A, && \text{if } f(\mathbf{y} \vert \mathbf{u}_A) \ge f(\mathbf{y} \vert \mathbf{u}_B), \\ 
    &\mathbf{u}_B, && \text{if } f(\mathbf{y} \vert \mathbf{u}_A) < f(\mathbf{y} \vert \mathbf{u}_B).
  \end{aligned} 
\right.
$$

When $\mathbf{x}_A$ was sent, we have $\mathbf{y} - \mathbf{u}_A \sim \mathcal{CN}(\boldsymbol{0}, N_0 \mathbf{I}_L)$. When $\mathbf{u}_B$ was sent, we have $\mathbf{y} - \mathbf{u}_B \sim \mathcal{CN}(\boldsymbol{0}, N_0 \mathbf{I}_L)$. Hence, the conditional PDF can be written explicitly as ([see results on complex Gaussian random vectors here](../05-detection-in-fading-channel/reading-05-complex-gaussian.html/))

\begin{aligned} 
  f(\mathbf{y} \vert \mathbf{u}_A) = \frac{1}{\pi^L N_0^L} e^{-\frac{\Vert \mathbf{y} - \mathbf{u}_A \Vert^2}{N_0}} \quad \text{and} \quad f(\mathbf{y} \vert \mathbf{u}_B) = \frac{1}{\pi^L N_0^L} e^{-\frac{\Vert \mathbf{y} - \mathbf{u}_B \Vert^2}{N_0}}.
\end{aligned} 

Therefore, the maximum likelihood detector has a simple decision rule:

$$
\hat{\mathbf{u}} = \left\{ 
  \begin{aligned} 
    &\mathbf{u}_A, && \text{if } \Vert \mathbf{y} - \mathbf{u}_A \Vert^2 \le \Vert \mathbf{y} - \mathbf{u}_B \Vert^2, \\ 
    &\mathbf{u}_B, && \text{if } \Vert \mathbf{y} - \mathbf{u}_A \Vert^2 > \Vert \mathbf{y} - \mathbf{u}_B \Vert^2.
  \end{aligned} 
\right.
$$

The physical meaning is also very clear: the transmit signal is more likely to be the one that is closer to the received signal.

Now we can derive the error probability of the maximum likelihood detection. Due to symmetry of the noise, we can focus on the case where $\mathbf{u}_A$ was sent and the detector output $\hat{\mathbf{u}} = \mathbf{u}_B$. In this case, the errors happens when $\Vert \mathbf{y} - \mathbf{u}_A \Vert^2 > \Vert \mathbf{y} - \mathbf{u}_B \Vert^2$. Using the fact that $\mathbf{y} = \mathbf{u}_A + \mathbf{w}$, we have

$$
\begin{aligned} 
                  & \quad \Vert \mathbf{y} - \mathbf{u}_A \Vert^2 > \Vert \mathbf{y} - \mathbf{u}_B \Vert^2 \\
  \Leftrightarrow & \quad \Vert (\mathbf{u}_A + \mathbf{w}) - \mathbf{u}_A \Vert^2 > \Vert (\mathbf{u}_A + \mathbf{w}) - \mathbf{u}_B \Vert^2 \\
  \Leftrightarrow & \quad \Vert \mathbf{w} \Vert^2 > \Vert \mathbf{w} + \mathbf{u}_A - \mathbf{u}_B \Vert^2 \\
  \Leftrightarrow & \quad \mathfrak{R}\left[ \left( \mathbf{u}_A - \mathbf{u}_B \right)^H \mathbf{w} \right] < - \frac{\Vert \mathbf{u}_A - \mathbf{u}_B \Vert^2}{2} \\
\end{aligned} 
$$

Since the noise vector $\mathbf{w} \sim \mathcal{CN}(\boldsymbol{0}, N_0 \mathbf{I}_L)$, we have $\left( \mathbf{u}_A - \mathbf{u}_B \right)^H \mathbf{w} \sim \mathcal{CN}(0, \Vert \mathbf{u}_A - \mathbf{u}_B \Vert^2 N_0)$. Hence, we have

$$
\mathfrak{R}\left[ \left( \mathbf{u}_A - \mathbf{u}_B \right)^H \mathbf{w} \right] \sim \mathcal{N}\left(0, \Vert \mathbf{u}_A - \mathbf{u}_B \Vert^2 \frac{N_0}{2}\right).
$$

Now we can write the error probability in terms of the Q function

$$
\mathbf{P}\left( \mathfrak{R}\left[ \left( \mathbf{u}_A - \mathbf{u}_B \right)^H \mathbf{w} \right] < - \frac{\Vert \mathbf{u}_A - \mathbf{u}_B \Vert^2}{2} \right) = Q\left( \frac{\Vert \mathbf{u}_A - \mathbf{u}_B \Vert^2 / 2}{\sqrt{\Vert \mathbf{u}_A - \mathbf{u}_B \Vert^2 N_0 / 2}} \right) = Q\left( \frac{\Vert \mathbf{u}_A - \mathbf{u}_B \Vert}{2 \sqrt{N_0 / 2}} \right).
$$

We can see that the error rate decreases with the distance $\Vert \mathbf{u}_A - \mathbf{u}_B \Vert$ between the two symbols and increases with the noise power $N_0$.

### Detection for BPSK under repetition coding

Now we consider the special case of BPSK, where $x = \pm a$. Under repetition coding, we have $\mathbf{u}_A = a \cdot \mathbf{h}$ and $\mathbf{u}_B = -a \cdot \mathbf{h}$. Then given a realization of the channel gain $\mathbf{h}$, the error probability is

$$
\mathbf{P}(\text{error}|\mathbf{h}) = Q\left( \frac{\Vert a \mathbf{h} - (-a \cdot \mathbf{h}) \Vert}{2 \sqrt{N_0 / 2}} \right) = Q\left( \frac{a \Vert \mathbf{h} \Vert}{\sqrt{N_0 / 2}} \right) = Q\left( \sqrt{2 \Vert \mathbf{h} \Vert^2 \textsf{SNR}} \right).
$$

Since the channel follows Rayleigh fading, the square of the norm $\Vert \mathbf{h} \Vert^2 = \sum_{\ell=1}^L \vert h_\ell \vert^2$ follows the [Chi-square distribution with $2L$ degrees of freedom](https://en.wikipedia.org/wiki/Chi-squared_distribution).

Therefore, the average error probability is

$$
p_e = \int_{0}^{\infty} Q\left( \sqrt{2 \Vert \mathbf{h} \Vert^2 \textsf{SNR}} \right) f(\Vert \mathbf{h} \Vert^2) d \Vert \mathbf{h} \Vert^2 \approx \mathcal{O}\left( \frac{1}{\textsf{SNR}^L} \right).
$$

Compared to BPSK without repetition coding, we get a better scaling law of $\textsf{SNR}^{-L}$. We call $L$ the **diversity gain**. 

However, the diversity gain comes at the expense of the reduced data rate under repetition coding, because we transmit the same symbol over $L$ time slots. Can we get the diversity gain without sacrificing the data rate?
