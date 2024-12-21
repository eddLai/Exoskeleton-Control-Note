FT可以[[recall signal and system]]
# STFT
ref. [深入理解短时傅里叶变换 STFT + Python 代码详解_stft python-CSDN博客](https://blog.csdn.net/weixin_44618906/article/details/116356081)

$$Z_{xx}(f,t) = \mathcal{F} \left\{ x(t) w(t - \tau) \right\}$$
$$P(f,t) = |Z_{xx}(f,t)|^2
$$
$$\text{Median Frequency} = \text{median} \left( P(f,t) \right)
$$


---
# TKEO operator
$$\psi_d[x(n)] = x^2(n) - x(n+1) x(n-1)$$
把動態放大

---
# Wavelet transform
- [小波变换（Wavelet Transform）-CSDN博客](https://blog.csdn.net/Forlogen/article/details/88535027)
- [数学基础-小波变换的原理及其应用_小波变换原理-CSDN博客](https://blog.csdn.net/weixin_37801695/article/details/80652113)
波的basis由多個有限長會衰減的小波組成；相比傅立葉由無限長的三角函數
![[wavelet.png]]
$$F(w) = \int_{-\infty}^\infty f(t) e^{-iwt} dt \quad \Rightarrow \quad 
WT(a, \tau) = \frac{1}{\sqrt{a}} \int_{-\infty}^\infty f(t) \psi^*\left(\frac{t - \tau}{a}\right) dt$$
尺度a和平移量 τ

---
解決：Fourier transform存在問題
![[problem of fourier transform.png|400]]
不包含時序資訊
大尺度因子，分辨率高，小頻率
![[Wavelet families.png|400]]
[Wavelets — PyWavelets Documentation](https://pywavelets.readthedocs.io/en/latest/ref/wavelets.html)
多種小波，有階數子集

數學證明:[小波变换——公式整理和简单介绍_离散小波变换公式-CSDN博客](https://blog.csdn.net/qq_32071849/article/details/103963394)

App. [[Feature Extraction and Reduction of Wavelet Transform Coefficients for EMG Pattern Classification.pdf]]

