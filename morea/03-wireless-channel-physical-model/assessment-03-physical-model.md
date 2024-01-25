---
title: "Physical models"
published: true
morea_id: assessment-03-physical-model
morea_summary: "Physical models of wireless channels"
# morea_outcomes_assessed:
 # - outcome-CHANGE-ME
morea_type: assessment
morea_start_date: "2024-01-24T00:00"
morea_end_date: "2024-01-31T23:55"
morea_labels:
---
# Physical models of wireless channels

*Please submit your solutions in Laulima.*

## A reflecting wall at the transmitter

We have worked on examples where there is a perfectly reflective wall at the receiver. Now let us assume that the wall is at the transmitter.

<figure style="text-align: center;">
  <img src="03-moving-antenna-reflecting-wall-tx.png" alt="Moving antennas with a reflecting wall at the transmitter" width="600">
</figure>

* (1 point) Derive the analytical expression of the received signal using the ray tracing method.
* (2 points) Following [the procedure here](reading-03-reflecting-wall-fixed-antenna.html), derive the coherence distance, the delay spread, and the coherence bandwidth. Compare them with the example when the wall is at the receiver.
* (2 points) Following [the procedure here](reading-03-reflecting-wall-moving-antenna.html), derive the Doppler spread and the coherence time. Compare them with the example when the wall is at the receiver.

## Reflecting on the ground plane

Consider the scenario where the transmit and receive antennas are at different heights. There is a line-of-sight path and a path where the signal is reflected on the ground.

<figure style="text-align: center;">
  <img src="03-reflection-from-ground-plane.png" alt="Two antennas at different heights" width="500">
</figure>

* (1 point) Derive the analytical expression of the received signal using the ray tracing method.
  * We can assume that the ground is a perfect reflector: it does not absorb energy and shifts the phase by \\(180^\circ\\).
  * Please use the heights \\(h_s, h_r\\) and the *horizontal distance* \\(r\\) as the parameters in the expression.
  * You would need to use some geometry to write \\(r_1\\) and \\(r_2\\) as a function of \\(h_s, h_r, r\\).
* (2 points) Write a Python script to draw the energy of the received signal as a function of the horizontal distance \\(r\\) between the transmitter and the receiver. Verify that the power scaling law is roughly \\(r^{-4}\\).
  * You can reuse our code in [the experiential learning](experience-03-fixed-antenna-reflecting-wall.html).
  * You can set the heights of the transmitter and the receiver as \\(h_s=30\\)m and \\(h_r=1\\)m, respectively.
  * Note that we derived the signal. For its power, we need to square it.
  * To verify the scaling law, it may be easier to plot in the log scale.