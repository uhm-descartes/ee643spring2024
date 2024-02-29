---
title: "Space-time codes"
published: true
morea_id: reading-07-space-time-codes
morea_summary: "Utilize spatial and temporal dimensions"
# morea_url: https://github.com/airbnb/javascript
morea_type: reading
morea_labels:
morea_sort_order: 73
---

# Space-time codes

In [the previous discussion](reading-07-transmit-diversity.html), we achieved the diversity gain with a data rate of one symbol per time slot by using rotation codes across multiple transmit antennas and multiple time slots. But with multiple antennas, our question is how can we further improve this scheme?

## Alamouti scheme

### Signaling scheme

To illustrate the Alamouti scheme, we consider the case of two transmit antennas and single receive antenna. In the Alamouti scheme, we transmit two independent *complex* symbols *simultaneously* from two antennas, denoted by $x_1[1] = u_1$ and $x_2[1] = u_2$. Then in the next time slot, we still transmit these two symbols but rearrange them so that $x_1[2] = -u_2^\ast$ and $x_2[2] = u_1^\ast$. Assuming that the channel remain constant over the two consecutive time slots, the overall signal model is

$$
    \left[ \begin{array}{cc} y[1] & y[2] \end{array} \right] = 
    \left[ \begin{array}{cc} h_1 & h_2 \end{array} \right] 
    \left[ \begin{array}{lr} u_1 & -u_2^\ast \\ u_2 & u_1^\ast \end{array} \right]  + 
    \left[ \begin{array}{cc} w[1] & w[2] \end{array} \right].
$$

Why we arrange the two symbols over the two time slots like this? This is because from the above signal model, we get two orthogonal vectors

$$
\left[ \begin{array}{c} u_1 \\ u_2 \end{array} \right] \quad \text{and} \quad \left[ \begin{array}{r} -u_2^\ast \\ u_1^\ast \end{array} \right].
$$

Each vector represents the symbols transmitted from the two transmit antennas. The two vectors over two time slots are orthogonal to each other. This orthogonality enables us to remove the interference between the two symbols at the receiver. 

### Detection in the Alamouti scheme
To see how to detect the symbols in the Alamouti scheme, we can rewrite the signal model as

$$
    \left[ \begin{array}{l} y[1] \\ y[2]^\ast \end{array} \right] = 
    \left[ \begin{array}{lr} h_1 & h_2 \\ h_2^\ast & -h_1^\ast \end{array} \right] 
    \left[ \begin{array}{c} u_1 \\ u_2 \end{array} \right]  + 
    \left[ \begin{array}{c} w[1] \\ w[2]^* \end{array} \right] = 
    \left[ \begin{array}{c} h_1 \\ h_2^\ast \end{array} \right] u_1 + 
    \left[ \begin{array}{r} h_2 \\ -h_1^\ast \end{array} \right] u_2  + 
    \left[ \begin{array}{c} w[1] \\ w[2]^* \end{array} \right].
$$

From the rewritten signal model above, it is clear that the two symbols $u_1$ and $u_2$ goes through two vector channels. More importantly, the two channels

$$
\left[ \begin{array}{c} h_1 \\ h_2^\ast \end{array} \right] \quad \text{and} \quad \left[ \begin{array}{r} h_2 \\ -h_1^\ast \end{array} \right]
$$

are also *orthogonal!*

Due to orthogonality, we can easily eliminate the interference between the two symbols. For example, we can eliminate the second symbol by

$$
r_1 = \left[ \begin{array}{cc} h_1^\ast & h_2 \end{array} \right] \left[ \begin{array}{l} y[1] \\ y[2]^\ast \end{array} \right] = \Vert \mathbf{h} \Vert^2 u_1 + w_1,
$$

where $\mathbf{h} = [h_1, h_2]^T$ and $w_1 \sim \mathcal{CN}\left(0, \Vert \mathbf{h} \Vert^2 N_0 \right)$.

Similarly, we can eliminate the first symbol by

$$
r_2 = \left[ \begin{array}{cc} h_2^\ast & -h_1 \end{array} \right] \left[ \begin{array}{l} y[1] \\ y[2]^\ast \end{array} \right] = \Vert \mathbf{h} \Vert^2 u_2 + w_2.
$$

The two scalars $r_1$ and $r_2$ can be used to detect symbols $u_1$ and $u_2$, respectively. Since each symbol is multiplied by $\Vert \mathbf{h} \Vert^2$, the diversity gain is 2.

In conclusion, the Alamouti scheme achieves the diversity gain of 2 while transmitting one *complex* symbol per time slot, which amounts to two *real* symbols per time slot.

## General space-time codes

### Definition

Space-time codes modulate transmit signals across space (i.e., antennas) and time. Mathematically, we can represent a space-time code by a set of complex codewords $\\{\mathbf{X}_i\\}$, where each codeword $\{\mathbf{X}_i \in \mathbb{C}^{L \times N}\}$ is a complex-valued $L$ by $N$ matrix. Here, $L$ is the number of antennas, and $N$ is the *block length* of the code (i.e., the number of time slots).

For example, a repetition code over 2 time slots and 2 antennas and with binary phase shift keying (BPSK) modulation can be represented by the two codewords below

$$
\mathbf{X}_1 = \left[ \begin{array}{cc} +1 & 0 \\ 0 & +1 \end{array} \right], \quad \mathbf{X}_2 = \left[ \begin{array}{cc} -1 & 0 \\ 0 & -1 \end{array} \right].
$$

The Alamouti scheme over 2 time slots and 2 antennas and with binary phase shift keying (BPSK) modulation can be represented by 16 codewords of the form

$$
\left[ \begin{array}{lr} u_1 & -u_2^\ast \\ u_2 & u_1^\ast \end{array} \right], 
$$

where $u_1$ and $u_2$ can be $1+j$, $1-j$, $-1+j$, and $-1-j$.

For fair comparison, we normalize the codewords so that hte average energy per symbol is $1$. Therefore, the signal-to-noise ratio (SNR) is $\textsf{SNR} = 1/N_0$.

### Performance analysis

Assuming that the channel does not change during the block length (i.e., for $N$ time slots), the signal model can be written as

$$
\mathbf{y}^T = \mathbf{h}^T \cdot \mathbf{X} + \mathbf{w}^T,
$$

where

$$
\mathbf{y} = \left[ \begin{array}{c} y[1] \\ \vdots \\ y[N] \end{array} \right], \quad \mathbf{h} = \left[ \begin{array}{c} h_1 \\ \vdots \\ h_N \end{array} \right], \quad \mathbf{w} = \left[ \begin{array}{c} w[1] \\ \vdots \\ w[N] \end{array} \right].
$$

As in [performance analysis of the rotation code](../06-time-diversity/reading-06-beyond-repetition-coding.html), we focus on pariwise error probability, which is a good approximation of the exact error probability. Conditioned on the channel vector $\mathbf{h}$, the probability of confusing $\mathbf{X}_B$ with $\mathbf{X}_A$ is

$$
\mathbf{P}\left( \mathbf{X}_A \rightarrow \mathbf{X}_B | \mathbf{h} \right) = Q\left( \frac{\Vert \mathbf{h}^T (\mathbf{X}_A - \mathbf{X}_B) \Vert}{2 \sqrt{N_0/2}} \right),
$$

which comes from the [vector Gaussian detection problem](../06-time-diversity/reading-06-performance-gain-time-diversity.html#detection-in-a-complex-vector-space) between $\mathbf{h}^T \mathbf{X}_A$ and $\mathbf{h}^T \mathbf{X}_B$.

Therefore, the pairwise error probability is

$$
\mathbf{P}\left( \mathbf{X}_A \rightarrow \mathbf{X}_B \right) = \mathbf{E}_{\mathbf{h}} \left[ Q\left( \sqrt{ \frac{ \textsf{SNR} \cdot \mathbf{h}^T (\mathbf{X}_A - \mathbf{X}_B) (\mathbf{X}_A - \mathbf{X}_B)^H \mathbf{h}^\ast }{2} } \right) \right]
$$

The $L \times L$ matrix $(\mathbf{X}_A - \mathbf{X}_B) (\mathbf{X}_A - \mathbf{X}_B)^H$ is Hermitian and positive semidefinite, and thus can diagonalized by

$$
(\mathbf{X}_A - \mathbf{X}_B) (\mathbf{X}_A - \mathbf{X}_B)^H = \mathbf{U} \mathbf{\Lambda} \mathbf{U}^H,
$$

where $\mathbf{U}$ is a unitary matrix, namely $\mathbf{U} \mathbf{U}^H = \mathbf{U}^H \mathbf{U} = \mathbf{I}$, and $\mathbf{\Lambda} = \text{diag} \left( \lambda_1^2, \ldots, \lambda_L^2 \right)$. Here, $\lambda_\ell$ is the $\ell$-th singular value of the codeword difference matrix $\mathbf{X}_A - \mathbf{X}_B$.

Then we can rewrite the pairwise error probability as

$$
\mathbf{P}\left( \mathbf{X}_A \rightarrow \mathbf{X}_B \right) = \mathbf{E}_{\mathbf{h}} \left[ Q\left( \sqrt{ \frac{ \textsf{SNR} \cdot \sum_{\ell=1}^L \vert \tilde{h}_\ell \vert^2 \lambda_\ell^2 }{2} } \right) \right],
$$

where $\mathbf{\tilde{h}} = \mathbf{U}^T \mathbf{h}$. Since $\mathbf{h}$ is a circularly symmetric complex Gaussian random vector, its linear transformation $$\mathbf{\tilde{h}}$ is also a circularly symmetric complex Gaussian random vector.

Using the property of the Q function $Q(x) \leq e^{-x^2/2}$ and the fact that $\vert \tilde{h}_\ell \vert^2$ are independent exponential random variables, we can bound the average pairwise error probability as

$$
\mathbf{P}\left( \mathbf{X}_A \rightarrow \mathbf{X}_B \right) \leq \mathbf{E}_{\mathbf{h}} \left[ e^{ -\frac{ \textsf{SNR} \cdot \sum_{\ell=1}^L \vert \tilde{h}_\ell \vert^2 \lambda_\ell^2 }{4} } \right] 
= \prod_{\ell=1}^L \mathbf{E}_{\tilde{h}_\ell} \left[ e^{ -\frac{ \textsf{SNR} \cdot \vert \tilde{h}_\ell \vert^2 \lambda_\ell^2 }{4} } \right] 
= \prod_{\ell=1}^L \frac{1}{ 1 + \textsf{SNR} \cdot \lambda_\ell^2 / 4 } .
$$

From here, we can see that it is important to have all the eeigenvalues $\lambda_\ell^2$ to be strictly positive. In this case, we can bound the error probability by

$$
\mathbf{P}\left( \mathbf{X}_A \rightarrow \mathbf{X}_B \right) \leq \frac{4^L}{\textsf{SNR}^L \prod_{\ell=1}^L \lambda_\ell^2} = \frac{4^L}{\text{det}\left[ (\mathbf{X}_A - \mathbf{X}_B) (\mathbf{X}_A - \mathbf{X}_B)^H \right]} \cdot \textsf{SNR}^{-L}.
$$

## Take-away

For a general space-time code, we need to design the codewords $\\{ \mathbf{X}_i \\}$ with the following rules.
 - The diversity gain is determined by the number of strictly positive eigenvalues $\lambda_\ell^2$, or equivalently the rank, of the matrix $(\mathbf{X}_A - \mathbf{X}_B) (\mathbf{X}_A - \mathbf{X}_B)^H$.
 - To achieve the maximum diversity gain of $L$, there should be $L$ strictly positive eigenvalues $\lambda_\ell^2$ of $(\mathbf{X}_A - \mathbf{X}_B) (\mathbf{X}_A - \mathbf{X}_B)^H$ over all pairs of codewords.
 - To minimize the multiplier before $\textsf{SNR}^{-L}$, we should maximize the minimum of the determinant $\text{det}\left[ (\mathbf{X}_A - \mathbf{X}_B) (\mathbf{X}_A - \mathbf{X}_B)^H \right]$ over all pairs of codewords.

Note that to achieve the maximum diversity gain of $L$, we need to have a block length $N$ greater than or equal to the number of transmit antennas $L$.
