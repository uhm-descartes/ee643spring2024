---
title: "Case 4: Reflecting wall and moving antennas"
published: true
morea_id: reading-03-reflecting-wall-moving-antenna
morea_summary: "Reflection creates delay spread"
# morea_url: https://github.com/airbnb/javascript
morea_type: reading
morea_labels:
morea_sort_order: 34
---

# Case 4: Reflecting wall and moving antennas

## Ray tracing

Continuing from the [previous example](reading-03-reflecting-wall-fixed-antenna.html), now we let the receive antenna move towards the wall at the speed \\(v\\).

<figure style="text-align: center;">
  <img src="03-reflecting-wall-moving-antenna.png" alt="Moving antennas with a reflecting wall" width="500">
</figure>

We need to update the time-varying distance between the two antennas as \\(r(t) = r_0 + vt\\). Using the same ray tracing method, we can calculate the received signal as
\\[
  E_r(f,t) = \frac{\alpha \cos 2 \pi f \left[(1-v/c) t - r_0 / c\right]}{r_0+vt} - \frac{\alpha \cos 2 \pi f \left[(1+v/c)t + (r_0-2d)/c\right]}{2d-r_0-vt}.
\\]

## Coherence distance, delay spread and coherence bandwidth
From the expression, we know that the received signal is a superposition of two sinusoids. 
* If the two sinusoids have a phase difference that is an even integer multiple of \\(\pi\\), they add up *constructively*. 
* If they have a phase difference that is an odd integer multiple of \\(\pi\\), they add *destructively* or *canel each other*.

Let us formulate this idea mathematically. The phase difference between the two sinusoids is
\\[
  \Delta \theta = \left( \frac{2 \pi f (2d-r)}{c} + \pi \right) - \left( \frac{2 \pi f r}{c} + \pi \right) = \frac{4 \pi f}{c} (d-r) + \pi.
\\]

The two sinusoids go from adding up constructively to canceling each other when the phase difference changes by \\(\pi\\), namely when
\\[
  \frac{4 \pi f}{c} (d-r) = \pi \Rightarrow \frac{4 f}{c} (d-r) = 1.
\\]

This means when the distance \\(r\\) or the frequency \\(f\\) changes a little, the strength of the received signal may change a lot, because the two sinusoids go from being constructive to destructive to each other.

In terms of the distance, the distance from a peak to a valley is defined as **coherence distance**, namely
\\[
  \Delta x_c \triangleq \frac{\lambda}{4},
\\]
where \\(\lambda = c/f\\) is the wavelength. 

In terms of the frequency, the signal strength changes from a peak to a valley when the frequency changes by
\\[
  \frac{1}{2} \left( \frac{2d-r}{c} - \frac{r}{c} \right)^{-1}.
\\]
Notice that the reciprocal of the above quantity, namely
\\[
  T_d = \frac{2d-r}{c} - \frac{r}{c},
\\]
is actually the propagation delay of the two paths. This is called **delay spread**.

We define \\(1/T_d\\) as the **coherence bandwidth**.

## Take-away
In wireless communication channels, multipath is common. Multipath creates **delay spread**, resulting in phase differences between signals arriving from different paths. The signals can either add up or canel each other. 

When the distance between the transmitter and the receiver changes by the **coherence distance**, the received signal goes from a peak to a valley.

When the frequency of the signal changes by the **coherence bandwidth**, the received signal goes from a peak to a valley.

Therefore, it is importance to know the coherence distance and the coherence bandwidth of a wireless channel. They tell us how fast the channel changes in the time domain and the frequency domain.