---
title: "Receive diversity"
published: true
morea_id: reading-07-receive-diversity
morea_summary: "Receive diversity is similar to time diversity"
# morea_url: https://github.com/airbnb/javascript
morea_type: reading
morea_labels:
morea_sort_order: 71
---

# Receive diversity

We start from the simplest case with one transmit antenna and multiple receive antenna. This is also called single-input-multiple-output (SIMO).

The signal model can be written as

$$
y_\ell[m] = h_\ell[m] x[m] + w_\ell[m] \qquad \ell=1,\ldots,L,
$$

where $L$ is the number of receive antennas, $m$ is the index of the time slot, $h_\ell[m]$ is the channel gain from the transmit antenna to the $\ell$-th receive antenna, $x[m]$ is the transmit signal, $w_\ell[m] \sim \mathcal{CN}(0,N_0)$ is the additive Gaussian noise, and $y_\ell[m]$ is the receive signal at the $\ell$-th receive antenna.

In this case, we essentially send multiple copies of the transmit signal to the receive antennas. The signal model is fundamentally the same as that in [repetition coding](../06-time-diversity/reading-06-performance-gain-time-diversity.html). 

Therefore, assuming that the channel gains to different receive antennas are independent, we can achieve the same diversity gain of $L$ as in time diversity. Such a diversity gain can be realized by either coherent or noncoherent detection.
