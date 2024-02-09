---
title: "Coherent detection in Rayleigh fading channels"
published: true
morea_id: reading-05-coherent-detection
morea_summary: "Knowing the channel does not help much"
# morea_url: https://github.com/airbnb/javascript
morea_type: reading
morea_labels:
morea_sort_order: 54
---

# Coherent detection in Rayleigh fading channels

We are not very satisfied with [the linear decay of the error rate in SNR under noncoherent detection](reading-05-noncoherent-detection.html). But in noncoherent detection, we treat the channel as a random variable. What if we know the channel gains $h[m]$ perfectly?

If we know the channel gain $h[m]$ (through channel estimation), we can "undo" the channel by

$$
\hat{y}[m] = \frac{y[m]}{h[m]} = x[m] + \frac{w[m]}{h[m]}.
$$

Now we have something resembling the input/output model of the AWGN channel! Can we achieve the exponential decay in the error rate?

In this case, given the channel gain $h[m]$, we have an equivalent AWGN channel with noise $\frac{w[m]}{h[m]} \sim \mathcal{CN}\left(0, \frac{N_0}{\vert h[m] \vert^2}\right)$.

From [the previous analysis](reading-05-awgn-vs-fading.html), we know that BPSK has an error rate of

$$
Q\left( \frac{a}{\sqrt{(N_0 / \vert h[m] \vert^2) / 2}} \right) = Q\left( \sqrt{ 2 \vert h[m] \vert^2 \textsf{SNR} } \right).
$$

Since the channel gain $h[m]$ is random, we can take the expectation and get the average error rate 

$$
  p_e = \mathbb{E}\left[ Q\left( \sqrt{ 2 \vert h[m] \vert^2 \textsf{SNR} } \right) \right] = \frac{1}{2} \left( 1 - \sqrt{\frac{\textsf{SNR}}{1+\textsf{SNR}}} \right) \approx \frac{1}{4 \textsf{SNR}}.
$$

The result is kind of disappointing -- **we still get a linear decay**. Compared to the noncoherent detection, the error rate only reduces by a factor of 2, and is still much worse than the exponential decay in the AWGN channel.

The reason is that when we "undo" the channel by dividing the received signal by the channel gain, we may magnify the noise if the channel is in "deep fading" (i.e., $h[m]$ is very small). The error rate under deep fading is large, and the probability of deep fading is also considerable. This motivates us to explore more advanced techniques (e.g., diversity).