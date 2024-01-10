---
title: "Building Blocks of Communication Systems"
published: true
morea_id: reading-building-blocks
morea_summary: "Building blocks of a typical communication system"
# morea_url: https://github.com/airbnb/javascript
morea_type: reading
morea_labels:
---

## Basic building blocks

Here is the block diagram of a typical <span style="color: red;">point-to-point</span> communication system.

<figure>
  <img src="02-building-blocks.png" alt="Building blocks of a typical communication system" width="500">
  <figcaption>Building blocks of a typical communication system. The top row are blocks in the transmitter, and the bottom row are in the receiver.</figcaption>
</figure>

Note that for each block in the transmitter, there is a counterpart in the receiver. Let us divide into each block and discuss their roles.

## Source Encoder and Source Decoder

<figure>
  <img src="02-building-blocks-source-coding.png" alt="Source coding in a typical communication system" width="500">
  <figcaption>The source encoder converts the source signal into a binary sequence, and the source decoder reconstructs the source signal.</figcaption>
</figure>

The source encoder "encodes" the message that the transmitter wishes to send. Here, "encodes" includes, but is not limited to, sampling the continuous-time signal to get a discrete-time signal, quantization, and compression.

For example, if we make a phone call, the source is an analog audio signal. Then the source encoder at the transmitter will sample, quantize, and compress the source and output a binary sequence. The source decoder at the receiver will reconstruct the analog audio signal.

Even if the source is already a binary sequence (e.g., a text message that is natively represented by a sequence of bits in our phone), the source encoder is still useful in compressing the original binary sequence into a shorter binary sequence.

Source coding is an important topic in information theory. But we will not dive deep into this topic in this course.

## Channel Encoder and Channel Decoder

<figure>
  <img src="02-building-blocks-channel-coding.png" alt="Channel coding in a typical communication system" width="500">
  <figcaption>The channel encoder adds redundancy to combat the channel errors, and the channel decoder "decodes" the message.</figcaption>
</figure>

The channel encoder *adds redundancy* to the binary sequence produced by the source encoding. This might seem counterintuitive -- didn't the source encoder just compress the source signal to *reduce* redundancy?

Well, the source encoder removes the inherent redundancy in the source signal, while the channel encoder adds *a different type of redundancy* to combat the imperfections of the channel. 

We will discuss some simple channel coding and decoding schemes in this course.

## Modulator and Demodulator

<figure>
  <img src="02-building-blocks-modulation.png" alt="Modulation in a typical communication system" width="500">
  <figcaption>The modulator "places" the signal in the correct space, time, and frequency, and the demodulator retrieves the signal.</figcaption>
</figure>

The radio spectrum is a very scarce resource. [Mobile operators spend tens of billions of dollars to buy a few hundred MHz of spectrum](https://www.spglobal.com/marketintelligence/en/news-insights/latest-news-headlines/big-4-wireless-carriers-spent-100b-on-5g-spectrum-was-it-worth-it-68488095).
> Verizon, meanwhile, spent $45.45 billion in the C-band spectrum auction in 2021 when the Federal Communications Commission auctioned 280 MHz of spectrum in the 3.7 GHz-3.98 GHz band. AT&T dished out $23.41 billion in the C-band auction and then followed that up by shelling out an additional $9.08 billion in the subsequent 3.45 GHz auction, which ended earlier this month. All told, the carrier spent $32.49 billion on mid-band spectrum across the two auctions. 
>
> _- S&P Global_

Therefore, the transmitter needs to carefully "modulate" the signal into the correct frequency band, and the receiver needs to "demodulate" (i.e., retrieve) the signal from the correct band.

Modulation is also important in avoiding *multi-user interference*. For example, in LTE, if two AT&T cell phones are making phone calls in the same room, their signals will be modulated into different frequency bins withint the AT&T spectrum.

Of course, the frequency is not the only degree of freedom. Modulation can place signals in different space and time. We will elaborate on this important topic later.