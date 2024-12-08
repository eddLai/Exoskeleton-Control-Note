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
# Analysis
https://web.ntnu.edu.tw/~algo/Signal.html
### Analytic signal
對於$x(t)$之原始信號，存在沒有負頻率的複值形式
$$z(t) = x(t) + j \hat{x}(t)$$
$$\hat{f} (\xi)=\int_{-\infty}^{\infty}f(x)e^{-2\pi ix\xi}dx$$
$$X(f) = \mathscr{F}\{x(t)\}$$
$$X(-f) = X^*(f)$$
### Hilbert tansform
$$\hat{x}(t) = \frac{1}{\pi} \int_{-\infty}^{\infty} \frac{x(\tau)}{t - \tau} d\tau$$
$$\hat{X}(f) = -j \, \text{sgn}(f) X(f)$$
$$\text{sgn}(f) =
\begin{cases}
j, & f > 0 \\
0, & f = 0 \\
-j, & f < 0
\end{cases}$$


MSE
經驗模態分解法：
瞬時頻率, intrinsic mode function
intrinsic mode entropy (IMEn):based on the recently developed multivariate empirical mode decomposition (MEMD) method
IMF: 波動是0，上下差小於1

- [[level of fatigue from EMG]]