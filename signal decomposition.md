# Frequency analysis

### Median Frequency

==步行速度的增加，脛前肌(TA)的肌電圖中值頻率會顯著下降==
ref. [[Effects of various walking intensities on leg muscle fatigue and plantar pressure distributions.pdf]]
$$Z_{xx}(f,t) = \mathcal{F} \left\{ x(t) w(t - \tau) \right\}$$
$$P(f,t) = |Z_{xx}(f,t)|^2
$$
$$\text{Median Frequency} = \text{median} \left( P(f,t) \right)
$$

### TKEO operator
$$\psi_d[x(n)] = x^2(n) - x(n+1) x(n-1)$$
把動態放大

---
# Recall system and signals
- $h(t)_{系統衝擊響應}$，為$\delta(x)_{Dirac\ delta單位脈衝函數}$輸入$LTI$系統所得到的響應
- LTI系統：線性響應, 時不變性（系統輸出與響應有相同位移）
- 系統響應：標準信號的輸出
- 系統輸出是信號與系統函數的卷積
$$y(t) = x(t) \ast h(t) = \int_{-\infty}^{\infty} x(\tau) h(t - \tau) \, d\tau.
$$
- [[Analytic signal and Hilbert Transform]]

ref. https://blog.csdn.net/ARM_qiao/article/details/108482457
瞬時頻率：透過analytic signal

---
# Signal Decomposition
### intrinsic mode function:
- 局部極值，與過零點數量相等
- 上下包絡線對於時間軸對稱（平均值為零）

### Empirical Mode Decomposition EMD
data-driven method，一個signal由多個IMF組成，IMF可以是線性或者非線性的
$$r(t) = x(t), \quad i = 0, \quad k = 1, \quad \text{SD} < \delta, \quad \delta \in [0.2, 0.3]
$$
用局部極值找到包絡線
$$e_{\text{max}}(t), \quad e_{\text{min}}(t)$$
$$m(t) = \frac{e_{\text{max}}(t) + e_{\text{min}}(t)}{2}$$
取得分量，減去均值包絡線
$$p(t) = r(t) - m(t)\quad \text{(2)}$$
$$\text{SD} = \frac{1}{N} \sum_{t=1}^{N} \left| p(t) - m(t) \right|$$
兩個條件
1. $$\text{If } \text{SD} < \delta, \text{ proceed to next step, otherwise return to step (2)}$$
2. r必須是單方向的$$\text{If } r(t) \text{ is not monotonic, then go back to step (2) and set } k = k + 1$$
$$x(t) = c_1(t) + c_2(t) + \cdots + c_n(t) + r_n(t)$$

頻譜： https://blog.maxkit.com.tw/2021/02/blog-post.html

---
### MEMD
ref. [nihms439498.pdf](https://pmc.ncbi.nlm.nih.gov/articles/PMC3831372/pdf/nihms439498.pdf)
multivariate data，用於local minimum不好找的情況。
projections along different directions in $(n−1)$dimensional spaces

$Hammersley$ 序列
$(n−1)$ 球面對應於 $n$ 維空間中的單位球面，$P_k (t)=v(t) \cdot x_{\theta_k}$
在特定投影上，主要特徵之極大值
$$m(t) = \frac{1}{K} \sum_{k=1}^K e_k(t)$$
$e_k(t)$為上邊界
$$d(t)=v(t)-m(t)$$

## CEEMDAN
ref. [[Denoising_electromyogram_and_electroencephalogram_.pdf]]