---
title: "Input/output models"
published: true
morea_id: assessment-04-input-output-model
morea_summary: "Physical models of wireless channels"
# morea_outcomes_assessed:
 # - outcome-CHANGE-ME
morea_type: assessment
morea_start_date: "2024-02-06T00:00"
morea_end_date: "2024-02-12T23:55"
morea_labels: Google Colab
---

# Input/output models of wireless channels

*Please submit your solutions in Laulima.*

In this assessment, we look at a realistic channel model with its parameters determined by field measurements. Then we will implement a simplified version of this channel model in [this Google Colab notebook](https://colab.research.google.com/drive/1-Phfq-bfamIrVRMkTvJAtOFAIcUtPoEA?usp=sharing).

One feature of the 5th-generation (5G) wireless communication systems is the usage of the millimeter-wave (mmWave) band at 60 GHz. Therefore, it is crucial to understand the mmWave channels. The Millimetre-Wave Evolution for Backhaul and Access (MiWEBA) project is one of the efforts toward this goal. If you are interested, you might want to take a look at [the complete project report](https://citeseerx.ist.psu.edu/document?repid=rep1&type=pdf&doi=e41ca51b3a590d267f5d09661b790c9002d3abbc).

For this assessment, we will only need to refer to [this paper](https://jwcn-eurasipjournals.springeropen.com/articles/10.1186/s13638-016-0568-6), which summarizes the main findings in channel modeling. You can read through the first two sections to get the background of the study.

We will implement a quasi-deterministic (Q-D) channel model, as illustrated in Fig. 8 of [the paper](https://jwcn-eurasipjournals.springeropen.com/articles/10.1186/s13638-016-0568-6). The Q-D channel consists of a few strong deterministic rays (D-rays) and some random rays (R-rays). Each ray or multipath is a cluster of rays with similar delays. You can look at Fig. 9 of [the paper](https://jwcn-eurasipjournals.springeropen.com/articles/10.1186/s13638-016-0568-6) for an example with two D-rays (i.e., the line-of-sight (LoS) path and the ground reflection path) and two R-rays (i.e., one path due to reflection from a car and the other due to reflection from a building). 

Below are the list of tasks to do.
* (4 points) Please look at Fig. 3 and Fig. 4, and identify four major multipaths in terms of delay (in ns) and power (in dB).
  - Note that a major multipath should have a relatively high power (i.e., less attenuation).
* (2 points) How would you assign each one of the four major multipaths to the LoS D-ray, the ground reflection D-ray, and two R-rays?
* (2 points) Fill in the power delay profile above in [the Google Colab notebook](https://colab.research.google.com/drive/1-Phfq-bfamIrVRMkTvJAtOFAIcUtPoEA?usp=sharing). Then calculate the following quantities.
  - Calculate the excess delays of the multipaths relative to the LoS path. For example, if the delays are 100 ns, 150 ns, 250 ns, 300ns, the excess delays should be 0 ns, (150-100 = 50) ns, (250-100 = 150) ns, (300-100 = 200) ns. Then convert the excess delays in seconds to excess delays in time slots according to the sampling rate.
  - Convert the power in dB to the power in the linear scale.
* (1 point) Run the code to see the *power spectral density (PSD)* of the transmit signal and that of the received signal. Explain how the channel results in the difference between the two PSDs? *Hint: think about the delay spread of the channel.*
  - Note that the PSD illustrates the spectrum of a *random* signal. It is defined as the Fourier transform of the *autocorrelation function* of the random signal. Unlike a deterministic signal, for a random signal, we compute the Fourier transform of its autocorrelation function, instead of the signal itself, because the autocorrelation function is deterministic.

