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

<grid drag="80 10" drop="40 70">
賴宏達
<!-- element style="font-size: 40px;align: right; text-align: right"-->
</grid>

<!-- slide bg="../../NTKLab_white bg_cover_resize.png"-->

---
測試是否可以用EMD方案取代以下幾點：
- Fatigue分析中的
	- 取代STFT: [Mean frequency derived via Hilbert-Huang transform with application to fatigue EMG signal analysis - ScienceDirect](https://www.sciencedirect.com/science/article/pii/S0169260706000472?ref=pdf_download&fr=RR-2&rr=8f3e26022ac98454), [EMG Mean Power Frequency Determination Using Wavelet Analysis](https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=757017)
	- Wavelet: [Frontiers | Comparison of Empirical Mode Decomposition, Wavelets, and Different Machine Learning Approaches for Patient-Specific Seizure Detection Using Signal-Derived Empirical Dictionary Approach](https://www.frontiersin.org/journals/digital-health/articles/10.3389/fdgth.2021.738996/full)
- Filter: [EMG signal filtering based on Empirical Mode Decomposition - ScienceDirect](https://www.sciencedirect.com/science/article/pii/S1746809406000085)

---
用`emd.sift.get_padded_extrema()`來抓peak??一樣是用`from scipy.signal import argrelextrema`的實現
[[Speed_analysis]]中的做法接近
![[peak from emd tool.png]]

---
```python
import emd
import matplotlib.pyplot as plt  # 修正 matplotlib 的正確導入
import numpy as np

# 確保 x 是 Numpy 陣列
x = Neck["Y"].to_numpy()  # 如果 Neck["X"] 是 pandas.Series，轉換為 Numpy 陣列

# 獲取極值點
peak_locs, peak_mags = emd.sift.get_padded_extrema(x, pad_width=0, mode='peaks')
trough_locs, trough_mags = emd.sift.get_padded_extrema(x, pad_width=0, mode='troughs')

# 繪圖
plt.figure()  # 呼叫 pyplot 的 figure() 函數來創建圖形
plt.plot(x, 'k', label='Signal')
plt.plot(peak_locs, peak_mags, 'ro', label='Peaks')
plt.plot(trough_locs, trough_mags, 'bo', label='Troughs')
# plt.xlim(300, 340)
plt.legend()
plt.show()
```

---