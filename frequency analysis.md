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
WT(a, \tau) = \frac{1}{\sqrt{a}} \int_{-\infty}^\infty f(t) \psi^*\left(\frac{t - \tau}{a}\right) dt$$

尺度$a$, 平移量 $\tau$

---
解決：Fourier transform存在問題
- 不包含原始波的時序資訊
![[problem of fourier transform.png|500]]

大尺度因子，分辨率高，小頻率
![[Wavelet families.png|450]]

---
[Wavelets — PyWavelets Documentation](https://pywavelets.readthedocs.io/en/latest/ref/wavelets.html)
多種小波，有階數子集

數學證明:[小波变换——公式整理和简单介绍_离散小波变换公式-CSDN博客](https://blog.csdn.net/qq_32071849/article/details/103963394)

App. [[Feature Extraction and Reduction of Wavelet Transform Coefficients for EMG Pattern Classification.pdf]]

