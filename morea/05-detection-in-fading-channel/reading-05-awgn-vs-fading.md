---
title: "AWGN vs fading channels"
published: true
morea_id: reading-05-awgn-vs-fading
morea_summary: "A failed attempt in the fading channel"
# morea_url: https://github.com/airbnb/javascript
morea_type: reading
morea_labels:
morea_sort_order: 51
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

Next, we use a simple signaling scheme, Binary Phase-shift keying (BPSK), to illustrate the key differences of the AWGN channel and the Rayleigh fading channel.


## Performance in the AWGN channel

In BPSK, we assign the binary bits of 0 and 1 to $x[m]=-a$ and $x[m]=+a$, respectively. Our goal is to determine which signal was sent base on the received signal $y[m]$. Therefore, we need to derive the optimal detection rule. 

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

Since

For any signal $s(t)$ with a bandwidth limited in $[-W/2, W/2]$, the sampling theorem asserts that we can sample it at a sampling frequency equal to its bandwidth $W$, namely at a sampling interval of $1/W$, and perfectly reconstruct it by

\begin{align}
  s(t) = \sum_{n} s[n] \text{sinc}(Wt-n),
\end{align}
where $s[n] = s(n/W)$ is the $n$-th sample, and $\text{sinc}(t)$ is defined as

\begin{align}
  \text{sinc}(t) \triangleq \frac{\sin(\pi t)}{\pi t}.
\end{align}

We can see that to perfectly reconstruct the continuous-time signal from its samples, we must sample it at a frequency at least as large as its bandwidth. This is intuitive. A signal with a larger bandwidth contains components at higher frequencies, which translate to faster variations in the time domain. Therefore, we need to sample it at smaller intervals to avoid missing any information.

This is also part of the reason why we want to do signal processing in the baseband. The passband signal has the highest frequency up to $f_c+W/2$, requiring us to sample it at a sampling frequency of $2 f_c + W$, which is much higher than the sampling frequency of $W$ required for a baseband signal.

### Modulation

The sampling theorem also suggests how we should convert the discrete-time data stream $x[n]$ to the continuous-time baseband signal $x_b(t)$:

\begin{align}
  x_b(t) = \sum_{n} x[n] \text{sinc}(Wt-n)
\end{align}

In other words, we pass the data stream $x[n]$ through a filter whose impulse response is the sinc function. We can also say that we "modulate" the data stream by the sinc function. 

In practice, we usually use other functions (e.g., raised cosine) to modulate the discrete-time signals.

## Discrete-time baseband channel model
Now that we know how to convert between the discrete-time signal and the continuous-time signal, we can derive an equivalent input/output model of the channel in the baseband and also in discrete time. As you may have guessed, the equivalent channel model is also a FIR filter, but in discrete time. 

Using the [equivalent channel model in the baseband](reading-04-baseband-equivalent-model.html), we can write the baseband receive signal as

$$
\begin{align}
  y_b(t)  & = \sum_i a_i^b(t) x_b(t - \tau_i(t)) \notag\\
          & = \sum_i a_i^b(t) \sum_{n} x[n] \text{sinc}\left[W(t-\tau_i(t))-n\right] \notag\\
          & = \sum_{n} x[n] \sum_i a_i^b(t) \text{sinc}\left(Wt-W\tau_i(t)-n\right). \notag
\end{align}
$$

The $m$-th sample of the baseband receive signal $y_b(t)$ is then

\begin{align}
  y[m] = y_b(m/W) = \sum_{n} x[n] \sum_i a_i^b(m/W) \text{sinc}\left[m-W\tau_i(m/W)-n\right] \notag
\end{align}

Defining the delay $\ell \triangleq m-n$, we have

\begin{align}
  y[m] = \sum_{\ell} x[m-\ell] \sum_i a_i^b(m/W) \text{sinc}\left[\ell-\tau_i(m/W) W\right] \notag
\end{align}

In conclusion, we can define the **discrete-time baseband equivalent channel model** as
\\[
  h_\ell[m] = \sum_i a_i^b(m/W) \text{sinc}\left[\ell-W\tau_i(m/W)\right],
\\]
so that the discrete-time baseband receive signal can be written as
$$
  y[m] = \sum_{\ell} h_\ell[m] x[m-\ell].
$$

Therefore, the discrete-time baseband equivalent chanenl model is *also a complex-valued FIR filter!*
