---
bg: "[[NTKLab_white bg.png]]"
---

<style>
    .reveal {
        font-family: 'Times New Roman', '標楷體';
        font-size: 30px;
        text-align: left;
        color: black;
        background-size: cover;
        background-position: center;
    }
	.reveal h1,
	.reveal h2,
	.reveal h3,
	.reveal h4,
	.reveal h5,
	.reveal h6 {
	  font-family: 'Times New Roman', '標楷體';
	  color: black;
	  %%text-transform: lowercase%%;
	  text-transform: capitalize;
	}
	.with-border{
		border: 1px solid red;
	}
</style>
<grid drag="70 10" drop="-3 40">
signal decomposition Note
<!-- element style="font-size: 40px;align: left; text-align: left;color: white"-->
</grid>

<grid drag="80 10" drop="-3 70">
賴宏達
</grid>

<!-- slide bg="../../NTKLab_white bg_cover_resize.png"-->

---
# Recall system and signals
- $h(t)_{系統衝擊響應}$，為$\delta(x)_{Dirac\ delta單位脈衝函數}$輸入$LTI$系統所得到的響應
- LTI系統：線性響應, 時不變性（系統輸出與響應有相同位移）
- 系統響應：標準信號的輸出
- 系統輸出是信號與系統函數的卷積
$$y(t) = x(t) \ast h(t) = \int_{-\infty}^{\infty} x(\tau) h(t - \tau) \, d\tau.
$$

[[instantaneous frequency-Analytic signal and Hilbert Transform]]，然而這個傳統的數學方法在複雜的波形會有巨大的飄移，他只能用在單純的波形上，透過使用在IMF使其有用武之地

---
科普文章連結 https://blog.csdn.net/ARM_qiao/article/details/108482457
>瞬時頻率：透過analytic signal，"本征模式函数(Intrinsic Mode Function，IMF)的新概念，基于这类函数的局部特性，使函数的任何一点瞬时频率都有意义。"

---
# Signal Decomposition
**目的**：用來改進如Fourier Transform需要的基底函數組成假設cos+sin的組合
也因此EMD並不直接產生頻譜圖
### intrinsic mode function:
定義：
- 局部極值，與過零點數量相等
- 上下包絡線對於時間軸對稱（平均值為零）

---
## Empirical Mode Decomposition, EMD
data-driven method，一個signal由多個IMF組成，IMF可以是線性或者非線性的
`emd.sift.get_padded_extrema()`，可以用這種方式修改設定
```python
ext_opts['pad_width'] = 5
max_locs, max_mag = emd.sift.get_padded_extrema(x, mode='peaks', **ext_opts)
```

$$r(t) = x(t), \quad i = 0, \quad k = 1, \quad \text{SD} < \delta, \quad \delta \in [0.2, 0.3]
$$
用局部極值找到包絡線
`emd.sift.interp_envelope()`
$$e_{\text{max}}(t), \quad e_{\text{min}}(t)$$
$$m(t) = \frac{e_{\text{max}}(t) + e_{\text{min}}(t)}{2}$$

![[EMD step1,2.png|500]]

---
取得分量，減去均值包絡線，==這樣就能得到最快的分量==
$$p(t) = r(t) - m(t)\quad \text{(2)}$$
$$\text{SD} = \frac{1}{N} \sum_{t=1}^{N} \left| p(t) - m(t) \right|$$
![[EMD step3,4.png|500]]

---
<split no-margin>
![[emd example 1.png|450]]
![[emd example 2.png|450]]
</split>

多次迭代
$$r_k(n) = r_{k-1}(n) - \sum_{k=1}^{K} IMF_k(n)$$

---
兩個條件跳出迭代
1. $$\text{If } \text{SD} < \delta, \text{ proceed to next step, otherwise return to step (2)}$$
2. r必須是單方向的$$\text{If } r(t) \text{ is not monotonic, then go back to step (2) and set } k = k + 1$$
$$x(t) = c_1(t) + c_2(t) + \cdots + c_n(t) + r_n(t)$$


---
# Example

---
## recall FT
頻譜科普： https://blog.maxkit.com.tw/2021/02/blog-post.html
假設兩信號
```python
x = np.cos(2*np.pi*freq*time_vect)
y = np.cos(2*np.pi*freq*time_vect) + 0.25*np.cos(2*np.pi*freq*2*time_vect-np.pi)
```

![[a signal spectrum.png|400]]
$$ppy[k] = \sum_{n=0}^{N-1} y[n] e^{-j \frac{2\pi}{K} k n}, \quad k = 0, 1, 2, \dots, N-1$$
```python
pyy = np.fft.fft(y) / len(x)
```

---
## Reconstruct the signal from freq. domain
$$f(x) =\sum_{n=-\infty}^\infty C_n \cdot e^{\frac{nx\pi}{p}j}=C_0 + \sum_{n=1}^\infty 2 |C_n| \cos\left( \frac{n\pi}{p} x + \phi_n \right)$$
$$|C_n| = \sqrt{\text{Re}(C_n)^2 + \text{Im}(C_n)^2}, \quad \phi_n = \arctan\left( \frac{\text{Im}(C_n)}{\text{Re}(C_n)} \right)$$

---
$$ppy_k=ppy[k], k=specific\ frequency,e.g.\ 50, 100Hz$$

$$A=2\times |ppy|$$

$$\phi_{ppy_k}=tan^{-1}{\frac{Im(ppy_k)}{Rm(ppy_k)}}$$

$$comp(t)=Acos(2\pi k\cdot t+\phi)$$

```python
comp1 = comp1_amp * np.cos(2*np.pi*5*time_vect + comp1_phase)
```

---

FT decomposition

![[FT decomposition of a signal.png|400]]
EMD decomposition

![[EMD decomposition of a signal.png|400]]

---
但是FT會有低頻訊號被轉換為多個高頻**separate harmonics**的問題。
![[separate harmonics.png|600]]
影響到我們觀察高頻信號

---
### EMF hilbert
```python
IP, IF, IA = emd.spectra.frequency_transform(imf, sample_rate, 'hilbert')
plt.figure(figsize=(10, 6))
plt.subplots_adjust(hspace=0.4)
plt.subplot(211)
plt.plot(time_vect[:sample_rate], imf[:sample_rate, 0])
plt.title('IMF-1')
plt.subplot(212)
plt.plot(time_vect[:sample_rate], IF[:sample_rate, 0])
plt.title('IMF-1 Instantaneous Frequency')
plt.ylabel('Frequency (Hz)')
```
instantaneous frequency
![[instantaneous frequency.png|450]]

---
![[hilbert-huang transform.png|450]]
不同於FT，Hilbert-Huang用一個連續的波段就表示了這樣一個訊號。

---
### Application
對於一個週期性震盪的複雜訊號
我們需要不同的windows來比較出哪種resolution會比較好
![[STFT vs HHT 1.png|350]]![[STFT vs HHT 2.png|350]]

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

---
### CEEMDAN
透過加入噪聲，解決雜訊的問題。

原始論文：[[A_complete_ensemble_empirical_mode_decomposition_with_adaptive_noise.pdf]]
ref. 
- 科普：[CEEMDAN：一种优化的集合经验模态分解算法](https://cloud.baidu.com/article/3253447)
- 應用：
	- [[Denoising_electromyogram_and_electroencephalogram_.pdf]]
	- [[A Novel Noise Reduction Method of UAV Magnetic Survey Data Based on CEEMDAN, Permutation Entropy, Correlation Coefficient and Wavelet Threshold Denoising.pdf]]

---
<split even>
![[flowchart of EEMD.png|450]]
![[flowchart of CEEMDAN.png|500]]
</split>


---
工具庫
- python庫解決方案: [PyEMD包安装导入踩坑 - 哔哩哔哩](https://www.bilibili.com/opus/781745878429859881)
- [EMD Tutorials — emd 0.6.2 documentation](https://emd.readthedocs.io/en/stable/emd_tutorials/index.html)
- [3.7 HHT ( Hilbert-Huang Transform)](http://www.ancad.com.tw/VS_Online_Help/ch03s07.html)
