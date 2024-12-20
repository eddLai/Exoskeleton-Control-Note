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
Comparison of Empirical Mode Decomposition (EMD) and Wavelet Transform Methods for EMG Gait Pattern and Fatigue Analysis
<!-- element style="font-size: 40px;align: left; text-align: left;color: white"-->
</grid>

<grid drag="50 10" drop="40 70">
賴宏達
<!-- element style="font-size: 40px;align: right; text-align: right"-->
</grid>

<!-- slide bg="../../NTKLab_white bg_cover_resize.png"-->

---
## 測試是否可以用EMD方案取代以下幾點：
- Fatigue分析中的
	- 取代STFT: 
		- \[1\] [Mean frequency derived via Hilbert-Huang transform with application to fatigue EMG signal analysis - ScienceDirect](https://www.sciencedirect.com/science/article/pii/S0169260706000472?ref=pdf_download&fr=RR-2&rr=8f3e26022ac98454)
		- \[2\] [EMG Mean Power Frequency Determination Using Wavelet Analysis](https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=757017) 
	- Wavelet:
		- \[3\] [Frontiers | Comparison of Empirical Mode Decomposition, Wavelets, and Different Machine Learning Approaches for Patient-Specific Seizure Detection Using Signal-Derived Empirical Dictionary Approach](https://www.frontiersin.org/journals/digital-health/articles/10.3389/fdgth.2021.738996/full)
		- \[4\] [[Analysis of EMG Signals Based on Wavelet.pdf]]
- Filter: \[5\] [EMG signal filtering based on Empirical Mode Decomposition - ScienceDirect](https://www.sciencedirect.com/science/article/pii/S1746809406000085)


---
## Review of Wavelet transform on EMG
[4] 頻譜分析：
- 短時傅立葉轉換 (STFT)
- Wigner-Ville 分佈 (WVD)
- Choi-Williams 分佈 (CWD) 
- 小波轉換 (WT)

WT: 選用與 MUAP 相似的波形
- "**the typical MUAP shape can be approximated as the second-order derivative of a Gaussian distribution**"
- "**Mexican hat wavelet, which is indeed the second-order derivative of a Gaussian distribution**"

去噪：Daubechies 小波（db2、db8 和 db6）和正交 Meyer 小波

---
"***the EMG is a non-stationary signal, especially for contraction levels higher than 50% of maximum voluntary contraction(MVC)***"[1]
- more info. [Enhancement of spectral analysis of myoelectric signals during static contractions using wavelet methods | IEEE Journals & Magazine | IEEE Xplore](https://ieeexplore.ieee.org/document/764944)

"***It does not require any quasi-stationarity and linear assumptions***"[1]
- more info. [Fatigue analysis of the surface EMG signal in isometric constant force contractions using the averaged instantaneous frequency - PubMed](https://pubmed.ncbi.nlm.nih.gov/12665043/)

一些自回歸方法[1] :autoregressive(AR), movingaverage (MA), autoregressive moving average (ARMA)

---
mean instantaneous frequency of isometric contraction[1]

IF=$\omega$, IA=$a$, IPower=$a^2$

$$MIF(j)=\frac{\sum_{i=1}^m\omega_j(i)a_j^2(i)}{\sum_{i=1}^ma_j^2(i)}$$

$$||a_j||=\sqrt{\sum_{i=1}^ma_j^2(i)}$$

$$MIF=\frac{\sum_{j=1}^m||a_j||MIF(j)}{\sum_{j=1}^m||a_j||}$$

whereas
$$W(s, t) = \int_{-\infty}^{\infty} x(\tau) \psi^*\left(\frac{\tau - t}{s}\right) d\tau
$$

$$P(s,t)=|W(s, t)|^2$$
兩者其實概念接近

---
## Comparison
穩定性量化between HHT, AR, Wavelet transform[1]
- $\sigma$標準差代表離散程度
- $\mu$提供中心值

相除以剔除量級因素
$$CoV=\frac{\sigma}{\mu}$$

分散$\rightarrow$不穩定
![[CoV result of different spectrum analysis.png|350]]

---
## Is Possible to combine DWT and EMD?

---
## Noise problem of EMG