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
frequency analysis
<!-- element style="font-size: 40px;align: left; text-align: left;color: white"-->
</grid>

<grid drag="50 10" drop="40 70">
賴宏達
<!-- element style="font-size: 40px;align: right; text-align: right"-->
</grid>

<!-- slide bg="../../NTKLab_white bg_cover_resize.png"-->

---

background knowledge: [[recall signal and system]]
## STFT
ref. [深入理解短时傅里叶变换 STFT + Python 代码详解_stft python-CSDN博客](https://blog.csdn.net/weixin_44618906/article/details/116356081)

$$Z_{xx}(f,t) = \mathcal{F} \left\{ x(t) w(t - \tau) \right\}$$
$$P(f,t) = |Z_{xx}(f,t)|^2
$$
$$\text{Median Frequency} = \text{median} \left( P(f,t) \right)
$$


---
## TKEO operator
$$\psi_d[x(n)] = x^2(n) - x(n+1) x(n-1)$$
把動態放大

---
## Wavelet transform
- [小波变换（Wavelet Transform）-CSDN博客](https://blog.csdn.net/Forlogen/article/details/88535027)
- [数学基础-小波变换的原理及其应用_小波变换原理-CSDN博客](https://blog.csdn.net/weixin_37801695/article/details/80652113)

波的basis由多個有限長會衰減的小波組成；相比傅立葉由無限長的三角函數，更符合複雜系統。
![[wavelet.png]]
$$F(w) = \int_{-\infty}^\infty f(t) e^{-iwt} dt \quad \Rightarrow \quad 
WT(b, a) = \frac{1}{\sqrt{a}} \int_{-\infty}^\infty f(t) \psi^*\left(\frac{t - a}{b}\right) dt$$

尺度$b$, 平移量 $a$

---
解決：Fourier transform不包含原始波的時序資訊的問題
![[problem of fourier transform.png|600]]
大$b$，分辨率高，小頻率

---
ref. [Wavelets — PyWavelets Documentation](https://pywavelets.readthedocs.io/en/latest/ref/wavelets.html)
多種小波，有階數子集
![[Wavelet families.png|600]]

---
resolution of continuous WT

ref.[連續小波轉換 - Wikiwand](https://www.wikiwand.com/zh-hk/articles/%E8%BF%9E%E7%BB%AD%E5%B0%8F%E6%B3%A2%E5%8F%98%E6%8D%A2)
![[resolution of WT.png]]
母波能量$\rightarrow$子波能量不變
$$\int_{-\infty}^\infty \left| \psi\left(\frac{t - a}{b}\right) \right|^2 dt = 1$$，低頻信號則b(時間尺度)較大


---
對於DiscreteWT存在
![[DWT tree.png]]
- 數學證明:[小波变换——公式整理和简单介绍_离散小波变换公式-CSDN博客](https://blog.csdn.net/qq_32071849/article/details/103963394)
- App. [[Feature Extraction and Reduction of Wavelet Transform Coefficients for EMG Pattern Classification.pdf]]

