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

$$D(f) = \int_{-\infty}^{\infty}\delta(t-t_0)e^{-2\pi jkt}dt= e^{-2\pi jkt_0}$$

---
# Discretized system
## Sampling
$$\delta_T(t)=\sum_{k=-\infty}^\infty \delta(t-kT)$$
for a signal $x(t)$,
$$x_s(t)=x(t)\delta_T(t)$$
let
$$sampling\ rate:\omega_0 = 2\pi/T$$
$$fourier\ seriers\ form:\delta_T(t)\left\{ \begin{aligned} 
\delta_T(t)&=\sum_{n=-\infty}^\infty C_ne^{jk\omega_0t}
\\ 
C_n&=\frac{1}{T}\int_{T} \delta_T(t)e^{-jk\omega_0t}dt=\frac{1}{T}
\end{aligned} \right.$$
$$x_s(t) = \frac{1}{T}\sum_{k=-\infty}^\infty e^{jk\omega_0t}\cdot x(t)$$

---
![[delta sampling sine function T1.png]]
![[delta sampling sine function T0.3.png]]

---
## the nyquist rate
$$\mathscr{F}\{x_s(t)\} = \int_{-\infty}^{\infty} \frac{1}{T}\sum_{n=-\infty}^\infty e^{jk\omega_0t}\cdot x(t)\cdot e^{-j\omega t}dt=X_S(\omega)$$
$$X_S(\omega)= \frac{1}{T}\sum_{k=-\infty}^\infty X(\omega-k\omega_0)$$
間隔 $\omega_0$ 則重複一次$\frac{1}{T}$原始頻譜
需要 $\omega_0$ > $2\times \omega$，才不會aliasing

---
## Signal classification
Power Signal:
$$P = \lim_{T \to \infty} \frac{1}{2T} \int_{-T}^{T} |x(t)|^2 \, dt$$
Energy Signal: 有限能量，例如脈衝
$$E = \int_{-\infty}^{\infty} |x(t)|^2 \, dt$$

---
## I/O $\rightarrow$ state space description
A continous time-invariant system
I/O description
舉例，y是輸出，u是輸入。
$$\ddot{y}(t) + a_1 \dot{y}(t) + a_0 y(t) = b_1 \dot{u}(t) + b_0 u(t)$$

state space description
$$\left\{ \begin{aligned} 
\dot{x}(t) &= Ax(t)+bu(t)&\ system\ state\ equation
\\ 
y(t) &= c\cdot x(t)&\ system\ output\ function(time-domain)
\end{aligned} \right.$$

>- x, y通常是矩陣
>- 消去x即可回到I/O equation

[[derivation of the solution of a state space description system]]
$$x(t)=e^A(t−t0)x0+∫t0teA(t−τ)Bu(τ) dτ.x(t) = e^{A(t-t_0)}x_0 + \int_{t_0}^{t} e^{A(t-\tau)}B u(\tau) \, d\tau.$$

