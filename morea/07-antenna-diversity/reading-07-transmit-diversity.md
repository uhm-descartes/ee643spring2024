---
title: "Transmit Diversity"
published: true
morea_id: reading-07-transmit-diversity
morea_summary: "Need to be clever to achieve transmit diversity"
# morea_url: https://github.com/airbnb/javascript
morea_type: reading
morea_labels:
morea_sort_order: 72
---

# Transmit Diversity

We have learned that [receive diversity is essentially time diversity](reading-07-receive-diversity.html). Specifically, by sending multiple copies of the transmit signal to $L$ receive antennas, we can achieve a diversity gain of $L$ when the channels to different receive antennas are independent. 

Now consider the case of multiple transmit antennas and single receive antenna, namely multiple-input-single-output (MISO). Can we achieve the same diversity gain by copying the transmit signal to different transmit antennas?

## Copy and paste does not work

Suppose that in time slot $m$, we send $L$ copies of the transmit signal $x[m]$ to the $L$ transmit antennas. Then the receive signal $y[m]$ will be

$$
y[m] = h_1[m] x[m] + \cdots + h_{L}[m] x[m] + w[m] = \left( \sum_{\ell=1}^L h_\ell[m] \right) x[m] + w[m].
$$

Essentially, the transmit signal goes through a channel with channel gain $\sum_{\ell=1}^L h_\ell[m] \sim \mathcal{CN}(0, LN_0)$. It is still a Rayleigh fading channel, but with $L$ times the gain.

Therefore, we do not get any diversity gain. The bit error rate (BER) will improve by the increased signal-to-noise ratio (SNR). But the BER versus SNR curve is simply shifted to the left, but has the same slope.

This example shows that we need to carefully design the transmission scheme to obtain the transmit diversity.

## Repetition code and rotation code

The simple "copy and paste" scheme does not work, because the copies of the transmit signals are combined at the single receiver. This is different from the case of multiple receive antennas, where we get independent copies at the receiver. So the natural idea is to create indepedent copies at the receiver in the MISO case.

Since there is only one receive antenna, we have to utilize the temporal dimension again. For example, we can transmit the signal $x$ at one transmit antenna in each time slot while keeping all the other transmit antennas idle. More specifically, we have

$$
y[m] = h_m[m] x + w[m] \qquad m=1,\ldots,L.
$$

It is clear that this scheme is equivalent to time diversity and will result in a diversity gain of $L$. However, since we are repeating the same signal $x$ in $L$ time slots, the data rate is reduced $L$ times.

To achieve the same diversity gain without sacrificing the data rate, we can use the [rotation code](../06-time-diversity/reading-06-beyond-repetition-coding.html).

However, we could have achieved the diversity gain of $L$ with one symbol per time slot using time diversity only. With multiple transmit antennas, we would like to achieve more.
