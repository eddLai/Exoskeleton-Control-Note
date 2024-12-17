# Frequency analysis
### STFT
ref. [深入理解短时傅里叶变换 STFT + Python 代码详解_stft python-CSDN博客](https://blog.csdn.net/weixin_44618906/article/details/116356081)

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
用來改進如Fourier Transform需要的基底函數組成假設cos+sin的組合
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
多次迭代
$$r_k(n) = r_{k-1}(n) - \sum_{k=1}^{K} IMF_k(n)$$

兩個條件跳出迭代
1. $$\text{If } \text{SD} < \delta, \text{ proceed to next step, otherwise return to step (2)}$$
2. r必須是單方向的$$\text{If } r(t) \text{ is not monotonic, then go back to step (2) and set } k = k + 1$$
$$x(t) = c_1(t) + c_2(t) + \cdots + c_n(t) + r_n(t)$$

![[EMD step1,2.png|500]]
![[EMD step3,4.png|500]]
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

### CEEMDAN
ref. 
- [[Denoising_electromyogram_and_electroencephalogram_.pdf]]
- [CEEMDAN：一种优化的集合经验模态分解算法](https://cloud.baidu.com/article/3253447)
- [IEEE Xplore Full-Text PDF:](https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=5947265)
- [[A Novel Noise Reduction Method of UAV Magnetic Survey Data Based on CEEMDAN, Permutation Entropy, Correlation Coefficient and Wavelet Threshold Denoising.pdf]]

![[flowchart of EEMD.png|400]]
![[flowchart of CEEMDAN.png|400]]
python庫解決方案: [PyEMD包安装导入踩坑 - 哔哩哔哩](https://www.bilibili.com/opus/781745878429859881)

---
### Wavelet transform
[小波变换（Wavelet Transform）-CSDN博客](https://blog.csdn.net/Forlogen/article/details/88535027)
波的basis由多個有限長會衰減的小波組成；相比傅立葉由無限長的三角函數
![[wavelet.png]]
Fourier transform存在問題
![[problem of fourier transform.png|400]]
不包含時序資訊
大尺度因子，分辨率高，小頻率
![[Wavelet families.png|400]]
[Wavelets — PyWavelets Documentation](https://pywavelets.readthedocs.io/en/latest/ref/wavelets.html)
多種小波，有階數子集

數學證明:[小波变换——公式整理和简单介绍_离散小波变换公式-CSDN博客](https://blog.csdn.net/qq_32071849/article/details/103963394)

App. [[Feature Extraction and Reduction of Wavelet Transform Coefficients for EMG Pattern Classification.pdf]]
