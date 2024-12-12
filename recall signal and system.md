# Discretized system
## Dirac delta function
ref. [set11.dvi](https://links.uwaterloo.ca/amath353docs/set11.pdf)
"the function is an example of a distribution."
$$\delta(t-t_0)=\left\{ \begin{aligned} 
&0, &t \neq t_0
\\
&\infty, &t = t_0 
\end{aligned} \right.$$
$$\int_{-\infty}^\infty \delta(t)dt=1$$
that is
$$\int_{-\infty}^\infty f(t)\delta(t-t_0)dt=f(t_0)$$
$$ \delta(t-t_0) = \int_{-\infty}^{\infty}\delta(t-t_0)e^{-2\pi jkt}dt= e^{-2\pi jkt_0}$$

---
## Sampling
$$\delta_T(t)=\sum_{k=-\infty}^\infty \delta(t-kT)$$
$$x_s(t)=x(t)\delta_T(t)$$
$$\omega_0 = 2\pi/T$$
很直觀的數學意義
$$\left\{ \begin{aligned} 
\mathscr{F}\{\delta_T(t)\}=\sum_{k=-\infty}^\infty c_ke^{-jk\omega_0t}
\\ 
c_k=\frac{1}{T}\int_{T} \delta_T(t)e^{jk\omega_0t}dt==1/T
\end{aligned} \right.$$

## 
A continous time-invariant system
$$\left\{ \begin{aligned} 
\dot{x}(t) &= Ax(t)+bu(t)
\\ 
y(t) &= c\cdot x(t)
\end{aligned} \right.$$
