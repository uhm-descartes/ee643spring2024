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


