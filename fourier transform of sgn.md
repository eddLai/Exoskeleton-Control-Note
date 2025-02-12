$$\text{sgn}(t) = 
\begin{cases} 
1 & \text{for } t > 0 \\
0 & \text{for } t = 0 \\
-1 & \text{for } t < 0
\end{cases}$$
$$X(\omega) = \int_{-\infty}^{\infty} \text{sgn}(t) \cdot e^{-j\omega t} dt$$
$$= \int_{-\infty}^{\infty} \left( \lim_{a \to 0} [e^{-at} \cdot u(t) - e^{at} \cdot u(-t)] \cdot e^{-j\omega t} \right) dt$$
$$= \lim_{a \to 0} \int_{-\infty}^{\infty} \left( [e^{-at} \cdot u(t) - e^{at} \cdot u(-t)] \cdot e^{-j\omega t} \right) dt$$
$$= \lim_{a \to 0} \int_{-\infty}^{\infty} e^{-at} \cdot e^{-j\omega t} \cdot u(t) - \int_{-\infty}^{\infty} e^{at} \cdot e^{-j\omega t} \cdot u(-t) dt$$
$$= \lim_{a \to 0} \int_{0}^{\infty} e^{-(a+j\omega)t} dt - \lim_{a \to 0} \int_{-\infty}^{0} e^{(a-j\omega)t} dt$$
$$= \lim_{a \to 0} \int_{0}^{\infty} e^{-(a+j\omega)t} dt - \lim_{a \to 0} \int_{0}^{\infty} e^{-(a-j\omega)t} dt$$
$$= \lim_{a \to 0} \left( \frac{e^{-(a+j\omega)t}}{-(a+j\omega)} \right) \Bigg|_0^\infty - \left( \frac{e^{-(a-j\omega)t}}{-(a-j\omega)} \right) \Bigg|_0^\infty$$
$$= \lim_{a \to 0} \left( \frac{1}{a+j\omega} - \frac{1}{a-j\omega} \right)$$
$$= \frac{2}{j\omega}$$