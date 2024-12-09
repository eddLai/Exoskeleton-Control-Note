[[fourier transform of sgn]]
$$H(f)=\text{sgn}(w) = 
\begin{cases} 
1 & \text{for } t > 0 \\
0 & \text{for } t = 0 \\
-1 & \text{for } t < 0
\end{cases}$$

### Analytic signal
使得$x(t)$之原始信號，沒有負頻率（傅立葉轉換僅僅為了維持)
$$Hermitian\_sysmetry:X(-f) = X^*(f)$$
$$X_a(f) \overset{\text{def}}{=} 
\begin{cases} 
2X(f), & \text{for } f > 0, \\
X(f), & \text{for } f = 0, \\
0, & \text{for } f < 0,
\end{cases}=X(f)+\text{sgn}(f) X(f)
$$
$$X(f) = 
\begin{cases}
\frac{1}{2} X_a(f), & \text{for } f > 0, \\
X_a(f), & \text{for } f = 0, \\
\frac{1}{2} X_a(-f)^*, & \text{for } f < 0 \, \text{(Hermitian symmetry)},
\end{cases}=\frac{1}{2} \left[ X_a(f) + X_a(-f)^* \right]$$

$$X_a(F) = X(f) + \text{sgn}(f) \cdot X(f)$$

---
$$x_a(t) \overset{\text{def}}{=} \mathcal{F}^{-1} \left[ X_a(f) \right]$$
$$x_a(t) = \mathcal{F}^{-1} \left[ X(f) \right] + \mathcal{F}^{-1} \left[ \text{sgn}(f) \right] \ast \mathcal{F}^{-1} \left[ X(f) \right]$$
$$x_a(t) = x(t) + j \left[ \frac{1}{\pi t} \cdot x(t) \right]=x(t) + j \hat{x}(t)= x(t) + j \cdot H(x(t))$$

---
### Define Hilbert transform
$$H(x(t)) = \mathcal{F}^{-1}\left[ -i \cdot \text{sgn}(\omega) \cdot X(\omega) \right]$$
$$H(x(t)) = \frac{1}{\pi} \, \text{p.v.} \int_{-\infty}^{\infty} \frac{x(\tau)}{t - \tau} d\tau$$
$$BTW. u(f) = \frac{1 + \text{sgn}(f)}{2}.$$

---
### Meaning of Hilbert tansform in freq domain
https://tzupingkao.coderbridge.io/2022/09/24/9-HilbertTransform/
對頻譜做$90^o$相位偏移
$$z=re^{j\theta}$$
$$e^{j\theta}=cos(\theta)+jsin(\theta)$$
$$\theta=arg(z)=arctan(\frac{Im(z)}{Re(z)})$$
$$a+bj=\frac{1}{jw}=-j\frac{1}{w}$$
$$arctan(-\infty)=-\pi/2, for\ \omega>0$$
$$arctan(\infty)=\pi/2, for\ \omega<0$$
