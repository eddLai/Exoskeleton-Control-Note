這是為什麼要做FT的原因，對於「一個信號進入一個系統」，的這個系統，可以轉成以頻域表達的系統函式，並用相乘來代表「一個信號進入一個系統」這件事情
$$y(t) = \int_{-\infty}^\infty x(\tau) h(t - \tau) \, d\tau
$$
$$Y(f)=X(f)\cdot H(f)$$
所以我們有需要把時域轉換成頻域

---
## Fourier Series
[[derivation of Fourier Transform]]
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
$$\delta_T(t)=\frac{1}{T}\sum_{n=-\infty}^\infty e^{jk\omega_0t}$$
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

## Z-transform
$$x_s(t)=x(t)\sum_{k=-\infty}^\infty \delta(t-kT)=\sum_{k=-\infty}^\infty x(kT)\delta(t-kT)$$
$$X_S(\omega) = \int_{-\infty}^{\infty} \sum_{k=-\infty}^\infty x(kT)\delta(t-kT)\cdot e^{-j\omega t}dt$$
$$=\sum_{k=-\infty}^\infty x(kT)\int_{-\infty}^{\infty} \delta(t-kT)\cdot e^{-j\omega t}dt=\sum_{k=-\infty}^\infty x(kT)e^{-j\omega kT}$$
配合離散形式系統
$$z=e^{jwk}, X(z)=\sum_{k=0}^\infty x[k]z^{-k}$$
把信號離散之後再進行傅立葉轉換

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
$$x(t) = e^{A(t-t_0)}x_0 + \int_{t_0}^{t} e^{A(t-\tau)}B u(\tau) \, d\tau$$

## Discretization
$$x((k+1)T) = e^{A((k+1)T - kT)} x[k] + \int_{kT}^{(k+1)T} e^{A((k+1)T-\tau)} b u(\tau) \, d\tau.$$
$$= e^{A T} x[k] + u[k] \int_{kT}^{(k+1)T} e^{A((k+1)T-\tau)} b \, d\tau\quad (1)$$
解決上面 $x(t)$ 之算式 $u(\tau)$ 仍為連續之問題。
$$k=kT$$
$$u[t]=u(kT)$$
$$x[k]=x(kT)$$
$$when\ kT\leq t \leq (k+1)T$$
$$初始條件\ x_0=x[k]$$
$$let\ (1), \alpha=\tau-kT, d\alpha=d\tau$$
$$x[k+1]=e^{AT}x[k] + u[k]\int_{0}^{T} e^{A(T-\alpha)}b d\alpha$$
$$\left\{ \begin{aligned} 
&A_T=e^{AT}
\\ 
&B_T=\int_{0}^{T} e^{A(T-\alpha)}b d\alpha
\end{aligned} \right.$$
$$\left\{ \begin{aligned} 
\dot{x}(t) &= Ax(t)+bu(t)
\\ 
y(t) &= c\cdot x(t)
\end{aligned} \right.= \left\{ \begin{aligned} 
&{x}[k+1] = A_Tx[k]+B_Tu[t]
\\ 
&y[k] = c\cdot x[k]
\end{aligned} \right.$$
can be proof by 
$$\dot{x}(t)=\frac{x[k+1]-x[k]}{T}$$
or Taylor Series of $e^{AT}$

---
## Stability of the system
$$e^x=1+x+\frac{1}{2!}x^2+\frac{1}{3!}x^3+...$$
$$limit_{T \rightarrow 0}\ e^{AT}\approx I+AT$$
eigenvalues are in the left half complex plane.

---
## DTFT
discrete time fourier transform, 
known
$$X_S(\omega)=\sum_{k=-\infty}^\infty x[k]e^{-j\omega kT}$$
如果對freqency domain也進行抽象
$$\Omega=\omega T$$
$$DTFT:X_S(\Omega)=\sum_{k=-\infty}^\infty x[k]e^{-j\Omega k}$$
$$InverseDTFT:\int_{\Omega_1}^{\Omega_1+2\pi}X(\Omega)e^{j\Omega n}d\Omega=\sum_{k=-\infty}^\infty x[k]\int_{\Omega_1}^{\Omega_1+2\pi}e^{-j\Omega k}\cdot e^{j\Omega n} d\Omega$$
only when $k=n$,
$$2\pi \cdot x[n] $$
$$InverseDTFT: x[n]=\frac{1}{2\pi}\int_{\Omega_1}^{\Omega_1+2\pi}X(\Omega)e^{j\Omega n}d\Omega$$
>notice the cycling convolution

---
## DFT
ref. [离散信号（七）| 离散傅里叶变换（DFT）推导_dft的推导-CSDN博客](https://blog.csdn.net/SanyHo/article/details/107102250)
對頻譜再做一次sampling, 
對於一個有限(finite time duration)的信號
$$x_0[k]=\left\{ \begin{aligned} 
&x_N[k],\ 0 \leq k\leq N-1
\\ 
&0,\ otherwise
\end{aligned} \right.$$
$$x[k]=x_0[k] \ast \delta_N(k)=\sum_{m=-\infty}^\infty x_0[m]\delta(k-m)$$

known: 
$$\delta_T(t)=\sum_{k=-\infty}^\infty \delta(t-kT)=\frac{1}{T}\sum_{k=-\infty}^\infty e^{jk\omega_0t}$$
discrete:
$$\delta_N(t)=\sum_{n=-\infty}^\infty \delta(k-nN)=\frac{1}{N}\sum_{n=-\infty}^\infty e^{jk\omega_0k}$$
$$\sum_{n=-\infty}^\infty x_0[m]\delta(k-m)=\sum_{m=-\infty}^\infty x_0[m]\delta(k-m-nN)$$
$$=\sum_{m=0}^{N-1} x_0[m]\sum_{m=-\infty}^\infty\delta(k-
m-nN)=x[k]$$

$$D_N(\Omega)=\sum_{n=-\infty}^\infty e^-j\Omega (nN)$$

$$X_S(\Omega)=\mathrm{F}_{DT}\{x[k]\}=X_0(\Omega)D_N(\Omega)=X_0(\Omega)\sum_{n=-\infty}^\infty e^-j\Omega (nN)$$
==從缺==
$$X[k] = \sum_{n=0}^{N-1} x[n] e^{-j \frac{2\pi}{K} k n}, \quad k = 0, 1, 2, \dots, N-1$$

---
## FFT
[FFT原理——详细推导理解FFT变换-CSDN博客](https://blog.csdn.net/weixin_40106401/article/details/106128194)
[離散餘弦變換、傅立葉變換、快速傅立葉變換 - iT 邦幫忙::一起幫忙解決難題，拯救 IT 人的一天](https://ithelp.ithome.com.tw/articles/10231357)
將DFT中的
$$W_N^{kn}=e^{-j \frac{2\pi}{K} k n},W=e^{-j \frac{2\pi}{N}}$$
利用其週期性及對稱性，進行縮放
$$W_N^{kn}=W_{N/k}^{n}$$

---
## STFT
[短时傅里叶变换STFT原理-CSDN博客](https://blog.csdn.net/m0_71709005/article/details/132247518)
[Lecture-3-STFT.dvi](https://ocw.nthu.edu.tw/ocw/upload/130/1603/10410%E5%8A%89%E5%A5%95%E6%96%87%E6%95%99%E6%8E%88%E6%95%B8%E4%BD%8D%E6%95%B8%E4%BD%8D%E8%81%B2%E8%A8%8A%E5%88%86%E6%9E%90%E8%88%87%E5%90%88%E6%88%90L3_Lecture-3-STFT.pdf)

$$X(\omega,n_0) = \sum_{n=-N}^{N-1} \omega[n] x[n+n_0]e^{-j \omega n}$$
$$overlap=N-(n_{0b}-{n_{0a}})*2+n_{0b}-{n_{0a}}=N-n_{0b}-{n_{0a}}$$
$$num\_windows=\frac{N_x-length(window)}{length(window)-noverlap(窗口重疊之樣本數)
}$$
window可以做選擇
![[window and resolution.png]]
提高頻率分辨率的方法:
- threshold
- 頻率譜集中

對於截取片段之訊號
- 除了起點不同，window所截取
- 因為overlap問題，所以跟整個總共的資料輸入也有關係。

![[STFT flowchart.png]]
不同的窗函數，[深入理解短时傅里叶变换 STFT + Python 代码详解_stft python-CSDN博客](https://blog.csdn.net/weixin_44618906/article/details/116356081)

- 主瓣（main lobe）：分辨率
- 旁瓣（Side Lobe）：一系列小波峰
