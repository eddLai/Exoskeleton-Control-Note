## Fourier Series
$$f(x) =\sum_{n=-\infty}^\infty C_n \cdot e^{\frac{nx\pi}{p}j}$$
$$C_n=\frac{1}{2p}\int_{-p}^p f(x)e^{\frac{-nx\pi}{p}j}dx$$

---
# Fourier Transform
ref. [Chapter 1 Fourier Transforms | Calculus and Applications - Part II](https://bookdown.org/vshahrez/lecture-notes/fourier-transforms.html#fouriers-integral-formula)
$$f(x) = \frac{1}{2\pi} \int_{-\infty}^{\infty}  \hat{f}(\omega)  e^{i \omega x} \, d\omega,
$$
$$\hat{f}(\omega) = \int_{-\infty}^{\infty} f(x) e^{-i \omega x} \, dx.
$$

---
## Dirac delta function
ref. [set11.dvi](https://links.uwaterloo.ca/amath353docs/set11.pdf)其中的fourier transform似乎是錯的
"the function is an example of a distribution."
$$\delta(t-t_0)=\left\{ \begin{aligned} 
&0, &t \neq t_0
\\
&\infty, &t = t_0 
\end{aligned} \right.$$
$$\int_{-\infty}^\infty \delta(t)dt=1$$
that is
$$\int_{-\infty}^\infty f(t)\delta(t-t_0)dt=f(t_0)$$
$$ D(f) = \int_{-\infty}^{\infty}\delta(t-t_0)e^{-2\pi jkt}dt= e^{-2\pi jkt_0}$$

---
# Discretized system
## Sampling
$$\delta_T(t)=\sum_{k=-\infty}^\infty \delta(t-kT)$$
for a signal $x(t)$,
$$x_s(t)=x(t)\delta_T(t)$$
let
$$\omega_0 = 2\pi/T$$
$$fourier\ seriers\ form:\delta_T(t)\left\{ \begin{aligned} 
\delta_T(t)&=\sum_{n=-\infty}^\infty C_ne^{jk\omega_0t}
\\ 
C_n&=\frac{1}{T}\int_{T} \delta_T(t)e^{-jk\omega_0t}dt=\frac{1}{T}
\end{aligned} \right.$$
$$x_s(t) = \frac{1}{T}\sum_{n=-\infty}^\infty e^{jk\omega_0t}\cdot x(t)$$
![[Pasted image 20241212222724.png]]
## 
A continous time-invariant system
$$\left\{ \begin{aligned} 
\dot{x}(t) &= Ax(t)+bu(t)
\\ 
y(t) &= c\cdot x(t)
\end{aligned} \right.$$
