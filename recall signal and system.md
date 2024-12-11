# Discretized system
## Sampling
$$x_s(t)=x(t)\delta_T(t)$$
$$\mathscr{F}\{\delta_T(t)\}=\sum_{k=-\infty}^\infty c_ke^{jk\omega_0t}$$
$$c_k=\frac{1}{T}\int_{T} \delta_T(t)$$
## 
A continous time-invariant system
$$\left\{ \begin{aligned} 
\dot{x}(t) &= Ax(t)+bu(t)
\\ 
y(t) &= c\cdot x(t)
\end{aligned} \right.$$
