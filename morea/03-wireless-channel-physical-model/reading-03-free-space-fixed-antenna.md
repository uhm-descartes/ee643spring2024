---
title: "Case 1: Fixed antennas in the free space"
published: true
morea_id: reading-03-free-space-fixed-antenna
morea_summary: "Two antennas in the space of nothingness"
# morea_url: https://github.com/airbnb/javascript
morea_type: reading
morea_labels:
morea_sort_order: 31
---

# Case 1: Fixed antennas in the free space

## The simplest environment
We start with the simpliest propagation model. Consider a transmitter anteanna, radiating into *free space*, and a receiver antenna in the *far field* (i.e., far away from the transmitter). There is nothing else in the space, so that the only propagation path for the signal is the line-of-sight (LOS) path from the transmitter to the receiver.

To make things even simpler, we let the transmitter send a sinusoid at frequency \\(f\\):
\\[ 
  \cos 2 \pi f t.
\\]

We can create an 3-dimensional (3D) coordination system with the transmitter antenna at the origin. Then the location of the receiver antenna can be described by a triple \\(\mathbf{u} = (r, \theta, \phi)\\), where \\(r\\) is the distance between the antennas, \\(\theta\\) is the vertical angle, and \\(\phi\\) is the horizontal angle.

In this simplest possible environment, we can analytically determine the received signal as
\\[
  E_r(f,t,\mathbf{u}) = \frac{\alpha(\theta,\phi,f) \cos 2 \pi f (t - r/c)}{r},
\\]
where \\(c = 3 \times 10^8\\)m/s is the speed of light.

## Breakdown
Now let us break down the above equation.
  * First, the received signal is still a sinusoid with the same frequency \\(f\\). But the phase is delayed by \\(2 \pi f r / c\\), which happened because the signal traveled across a distance of \\(r\\) at the speed \\(c\\).
  * Second, the magnitude of the received signal depends on the function \\(\alpha(\theta,\phi,f)\\), which represents the antenna gain. The technical term is *radiation pattern* of the antenna, which usually looks like this:

    <figure style="text-align: center;">
      <img src="03-radiation-pattern.svg" alt="A typical radiation pattern" width="500">
      <figcaption>By Timothy Truckle; Link: https://commons.wikimedia.org/w/index.php?curid=4245213</figcaption>
    </figure>

    + We can see that the antenna magnifies the signal at different levels depending on the angles. Since both the transmitter antenna and the receiver antenna have radiation patterns, the function \\(\alpha(\theta,\phi,f) = \alpha_s(\theta,\phi,f) \cdot \alpha_r(\theta,\phi,f)\\) is the product of the transmitter antenna radiation pattern \\(\alpha_s(\theta,\phi,f)\\) and the receiver antenna radiation pattern \\(\alpha_r(\theta,\phi,f)\\).
    + We will not talk much about the radiation pattern in this course, because they are fixed and known.
  
  * Third, the magnitude of the received signal is inverse propotional to the distance \\(r\\). This indicates that the power of the signal decreases as \\(r^{-2}\\). This is the *large-scale fading*. Note that the power law may change with the actual environment (i.e., raining or existence of other objects in the environment).

## Take-away
In summary, in a free space, the received signal attenuates by \\(r^{-2}\\). The frequency \\(f\\) does not change. The phase is delayed due to the distance. Nothing particularly interesting here.

We will see something more interesting in more complicated environments.