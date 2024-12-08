# 現在方案
1. Cygnus, protocol:BT 
>Cygnus version: 0.28.0.7
>Operative system: Windows
>Device ID: STEEG_DG819202
>Device bandwidth: DC to 131 Hz
>Device sampling rate: 1000 samples/second
>Data type / unit: non-EEG / micro-volt (uV)
>Bandpass filter: None
>Notch filter: None

1. high-pass filter: `filted_emg = self.h_filter.filtfilt(signal)`
2. notch filter:`filted_emg = self.n_filter.filtfilt(filted_emg)`
3. Rectification: `rect_emg = np.abs(filted_emg)`
4. Get the envelope using low-pass filter: `envelope = self.l_filter.filtfilt(rect_emg)`
5. normalize_data to `[0,1]`==標準差不會是1==
6. 
# Data collection
硬體突破：
- [無線EMG貼片](https://www.bio-translational-exoskeleton.com/)

可能要用來配合建立DQN的模型

---
# Models
MUAPs:肌肉基本運動單元，包含肌肉纖維及神經元
### Denoise方法
- muscle artifact (MA)
- ocular artifacts
- Baseline wander
- CEEMDAN

---
# Analysis methods
https://web.ntnu.edu.tw/~algo/Signal.html
# Recall system and signals
系統函數，為Dirac delta單位脈衝函數$\delta(x)$輸入LTI系統所得到的響應
LTI系統：

### Hilbert tansform
$$\hat{x}(t) = \frac{1}{\pi} \int_{-\infty}^{\infty} \frac{x(\tau)}{t - \tau} d\tau$$
$$\hat{X}(f) = -j \, \text{sgn}(f) X(f)$$
$$\text{sgn}(f) =
\begin{cases}
j, & f > 0 \\
0, & f = 0 \\
-j, & f < 0
\end{cases}$$

### Analytic signal
使得$x(t)$之原始信號，沒有負頻率（傅立葉轉換僅僅為了維持
$$z(t) = x(t) + j \hat{x}(t)$$
$$\hat{f} (\xi)=\int_{-\infty}^{\infty}f(x)e^{-2\pi ix\xi}dx$$
$$X(f) = \mathscr{F}\{x(t)\}$$
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
$$x_a(t) \overset{\text{def}}{=} \mathcal{F}^{-1} \left[ X_a(f) \right]$$
$$x_a(t) = \mathcal{F}^{-1} \left[ X(f) \right] + \mathcal{F}^{-1} \left[ \text{sgn}(f) \right] \ast \mathcal{F}^{-1} \left[ X(f) \right]$$
$$x_a(t) = x(t) + j \left[ \frac{1}{\pi t} \ast x(t) \right]=x(t)+s_a(t) = s(t) + j \hat{x}(t).
$$
$$u(f) = \frac{1 + \text{sgn}(f)}{2}.$$

MSE
經驗模態分解法：
瞬時頻率, intrinsic mode function
intrinsic mode entropy (IMEn):based on the recently developed multivariate empirical mode decomposition (MEMD) method
IMF: 波動是0，上下差小於1

- [[neurologic disorders and sEMG]]
- [[level of fatigue from EMG]]