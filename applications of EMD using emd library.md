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
applications of EMD using emd library
<!-- element style="font-size: 40px;align: left; text-align: left;color: white"-->
</grid>

<grid drag="50 10" drop="40 70">
賴宏達
<!-- element style="font-size: 40px;align: right; text-align: right"-->
</grid>

<!-- slide bg="../../NTKLab_white bg_cover_resize.png"-->

---
ref.[EMD Tutorials — emd 0.6.2 documentation](https://emd.readthedocs.io/en/stable/emd_tutorials/index.html)

用`emd.sift.get_padded_extrema()`來抓peak??一樣是用`from scipy.signal import argrelextrema`的實現
[[Speed_analysis]]中的做法接近
![[peak from emd tool.png]]

透過IA可以得到envelope

---
## 解讀IMFs
<split no-margin>
![[simple singals for EMD.png|450]]
![[EMD of nonlinear system output.png|450]]
</split>
This is as the non-linear system makes the peaks larger and the troughs smaller which shifts the mean of the signal away from zero, see IMF2

---
## Application: AM

高頻載波信號的振幅，實現低頻調製信號的嵌入，從而達成訊息傳輸的目的。
- 高頻carrier wave
- 低頻Baseband Signal or Modulating Signal

![[AM of IMFs.png|500]]

---
跨腦區資訊之判讀:
[[波中有波─談腦電波的跨頻跨腦區.pdf]]

```python
# Helper function for the second level sift
def mask_sift_second_layer(IA, masks, config={}):
    imf2 = np.zeros((IA.shape[0], IA.shape[1], config['max_imfs']))
    for ii in range(IA.shape[1]):
        config['mask_freqs'] = masks[ii:]
        tmp = emd.sift.mask_sift(IA[:, ii], **config)
        imf2[:, ii, :tmp.shape[1]] = tmp
    return imf2


# Define sift parameters for the second level
masks = np.array([25/2**ii for ii in range(12)])/sample_rate
config = emd.sift.get_config('mask_sift')
config['mask_amp_mode'] = 'ratio_sig'
config['mask_amp'] = 2
config['max_imfs'] = 5
config['imf_opts/sd_thresh'] = 0.05
config['envelope_opts/interp_method'] = 'mono_pchip'

# Sift the first 5 first level IMFs
imf2 = emd.sift.mask_sift_second_layer(IA, masks, sift_args=config)
```

---
![[HHT complex standard plotting.png]]
Holospectrum: Carrier Frequency, AM frequency, 能量分佈(集中好)

---
emd.spectra.holospectrum()
- `fcarrier`：載波頻率的中心點，即頻率軸的取樣點。
- `fam`：振幅調製頻率的中心點。
- `holo`：三維矩陣，表示每個載波頻率與振幅調製頻率組合處的平均功率（在整段時間內）。

```python
# Carrier frequency histogram definition
carrier_hist = (1, 100, 128, 'log')
# AM frequency histogram definition
am_hist = (1e-2, 32, 64, 'log')
# Compute the 1d Hilbert-Huang transform (power over carrier frequency)
fcarrier, spec = emd.spectra.hilberthuang(IF, IA, carrier_hist, sum_imfs=False)
# Compute the 2d Hilbert-Huang transform (power over time x carrier frequency)
fcarrier, hht = emd.spectra.hilberthuang(IF, IA, carrier_hist, sum_time=False)
shht = ndimage.gaussian_filter(hht, 2)

# Compute the 3d Holospectrum transform (power over time x carrier frequency x AM frequency)
# Here we return the time averaged Holospectrum (power over carrier frequency x AM frequency)
fcarrier, fam, holo = emd.spectra.holospectrum(IF, IF2, IA2, carrier_hist, am_hist)
sholo = ndimage.gaussian_filter(holo, 1)
```
[[HHT complex AM plotting code]]

---
## 跨頻相位-振幅耦合 (PAC)

有哪些信號是跨頻率的溝通。
例如:
在 5 Hz 信號的峰值或谷值時，特定高頻信號（如 32 Hz）的振幅可能更強。這種現象表明 5 Hz 信號的**特定相位對高頻振幅具有調制(modulation)效果**
```python
hht_by_phase, _, _ = emd.cycles.bin_by_phase(IP[:, 3], hht.T)
```

---
![[hht_by_phase.png|500]]
[On Holo-Hilbert spectral analysis: a full informational spectral representation for nonlinear and non-stationary data | Philosophical Transactions of the Royal Society A: Mathematical, Physical and Engineering Sciences](https://royalsocietypublishing.org/doi/10.1098/rsta.2015.0206)

---
高頻載波到底多寬多窄？如何量化？

![[phase bin of AM.png]]
x軸為phase，來自低頻訊號，透過`shft`取得
```python
ia_by_phase, ia_by_phase_var, phase_bins = emd.cycles.bin_by_phase(IP[:, 4], IA[:, 0], nbins=24)
```

---
也可經過HHT再分析`cycles.bin_by_phase`
```python
freq_edges, freq_centres = emd.spectra.define_hist_bins(10, 75, 75, 'log')
f, hht = emd.spectra.hilberthuang(IF, IA, freq_edges, mode='amplitude', sum_time=False)
```
![[HHT AM phase bin.png]]

---
## IF的意義
- IF較低，代表waveform shape較平緩
- IF應該要是正值
- **良好的諧波結構**：
    - 信號有規律的波形（例如單一非正弦振盪），每個週期重複，沒有次要極值。
- **不良的諧波結構**：不穩定
    - 波形中存在額外的次要極值（secondary extrema），或每個週期波形不一致。

---
![[secondary extrema.png]]
應用上可以用來確保LFP所得正確[Brain Oscillations and the Importance of Waveform Shape - ScienceDirect](https://www.sciencedirect.com/science/article/pii/S1364661316302182?via%3Dihub)

---
<split no-margin>
![[non-linearity 0.6.png|450]]
![[non-linearity 1.5.png|450]]
</split>
紅色代表不良的非線性結構

---
### EMD 用於分離Harmonic
傅立葉轉換一定會出現諧波，而EMD也會，但是可以分離
Harmonic的數學定義：
ref.[Understanding Harmonic Structures Through Instantaneous Frequency | IEEE Journals & Magazine | IEEE Xplore](https://ieeexplore.ieee.org/document/9854188)

$$x(t)=\sum_{n=1}^Na_ncos(\omega_nt+\phi_n)$$

因此

$$\omega_n=n\omega_0$$

$$\frac{d\phi_n}{dt}=0$$

由於其組成穩定，因此$IF \geq 0$

---
Example of Harmonic

![[Example of Harmonic.png]]

---
1. 極值計數（extrema counting）
	$$Phase DistCorr >> 0, p<0.05$$
$$f_{Ratio}\approx n$$
2. IMF方法可以判斷
$$Amplitude\ Ratio \times Frequency\ Ratio \leq 1$$

```python
df = emd.imftools.assess_harmonic_criteria(IP, IF, IA, num_segments=20, base_imf=2)

| IMF   |   Phase DistCorr |   p-value |   InstFreq Ratio |     p-value |   af Ratio |     p-value |
|-------+------------------+-----------+------------------+-------------+------------+-------------|
| IMF-0 |        0.0108423 |  0.555227 |          5.14905 | 6.73923e-05 |   1.19987  | 1           |
| IMF-1 |        0.394492  |  0        |          2.05304 | 1.03951e-06 |   0.449171 | 1.83191e-32 |
```

---
it would be valid to add IMF-2 and IMF-3.
![[sum of harmonic.png]]

---
## Cycle detection
>使用IP之間差距大於$1.5\pi$則為一個新的週期
```python
all_cycles = emd.cycles.get_cycle_vector(IP, return_good=False)

```
definition of good cycle

1. $$\frac{dIP(t)}{dt}>0$$確保沒有相位倒退
2. 相位包含完整的$2\pi$
3. 擁有 4 個控制點
	-  **上升零交點（Ascending Zero-Crossing）**
	- **峰值（Peak）**
	- **下降零交點（Descending Zero-Crossing）**
	- **谷值（Trough）**

---
放大看IMF 0~2秒
<split no-margin>
![[good cycle step1.png|450]]
![[good cycle step2.png|450]]
</split>

---
這是只顯示前20的cycle
```python
ctrl = emd.cycles.get_control_points(imf[:, 2], all_cycles[:, 2])
```
![[good cycle step3.png]]

---
第20
```
Cycle  0 - [0 5 8 13 16]
...
Cycle 19 - [0 2 4 nan 6]
```
![[good cycle step3 with bad one.png]]

---
lib已經寫好，可以透過增加一個參數就做到
```python
good_cycles = emd.cycles.get_cycle_vector(IP, return_good=True, phase_step=np.pi)

plt.figure(figsize=(10, 8))
plt.subplots_adjust(hspace=.3)
plt.subplot(311)
plt.plot(t[:sample_rate*4], imf[:sample_rate*4, 2], 'k')
plt.gca().set_xticklabels([])
plt.title('IMF-3')
plt.subplot(312)
plt.plot(t[:sample_rate*4], IP[:sample_rate*4, 2], 'b')
plt.gca().set_xticklabels([])
plt.plot((0, 4), (0, 0), label='0')
plt.plot((0, 4), (np.pi*2, np.pi*2), label='2pi')
plt.plot((0, 4), (np.pi*2-np.pi/12, np.pi*2-np.pi/12), ':', label='Upper Thresh')
plt.plot((0, 4), (np.pi/12, np.pi/12), ':', label='Lower Thresh')
plt.title('Instantanous Phase')
plt.ylabel('Radians')
plt.subplot(313)
plt.plot(t[:sample_rate*4], good_cycles[:sample_rate*4, 2])
plt.title('Good cycles')
plt.xlabel('Time (seconds)')
```

---
![[result of good cycle API.png|500]]
y軸代表第幾個環
```python
In:
percent = np.round(100*(good_count/all_count), 1)
Output:
IMF-3 contains 150 cycles of which  70 (46.7%) are good
IMF-4 contains  99 cycles of which  77 (77.8%) are good
```

---
### Statistics meaning of cycles
description of cycles
```python
emd.cycles.get_cycle_stat
cycle_amp = emd.cycles.get_cycle_stat(all_cycles[:, 2], IA[:, 2], out='samples', func=np.max)
```
![[cycle_amp stat.png]]

---
```python
cycle_mean_freq = emd.cycles.get_cycle_stat(all_cycles[:, 2], IF[:, 2], out='samples', func=np.mean)
```
![[cycle_mean_freq stat.png]]

---
### Masking
customise the parts of the signal in which we look for cycles by defining a mask
- signal with artefacts
- ==limit cycle detection to a specific period during a task==
- limit cycle detection to periods where there is a high amplitude oscillation.

example

對於特定域值以下去除
```python
thresh = np.percentile(IA[:, 2], 33)
mask = IA[:, 2] > thresh
mask_cycles = emd.cycles.get_cycle_vector(IP, return_good=True, mask=mask)
```

---
### Comparison between masked and unmasked
![[Comparison between masked and unmasked.png]]

---
```python
# Compute cycle average frequency for all cycles and masked cycles
all_cycle_freq = emd.cycles.get_cycle_stat(all_cycles[:, 2], IF[:, 2], func=np.mean)
mask_cycle_freq = emd.cycles.get_cycle_stat(mask_cycles[:, 2], IF[:, 2], func=np.mean)

# Compute cycle frequency range for all cycles and for masked cycles
all_cycle_amp = emd.cycles.get_cycle_stat(all_cycles[:, 2], IA[:, 2], func=np.mean)
mask_cycle_amp = emd.cycles.get_cycle_stat(mask_cycles[:, 2], IA[:, 2], func=np.mean)

# Make a summary figures
plt.figure()
plt.plot(all_cycle_freq, all_cycle_amp, 'o')
plt.plot(mask_cycle_freq, mask_cycle_amp, 'o')
plt.xlabel('Cycle average frequency (Hz)')
plt.ylabel('Cycle average amplitude')
plt.plot((9, 22), (thresh, thresh), 'k:')
plt.legend(['All-cycles', 'Masked-cycles', 'Amp thresh'])
```

---
### Degree of Non-linearity, DoN of cycles
```python
def degree_nonlinearity(x): return np.std((x - x.mean()) / x.mean())
all_cycle_freq_don = emd.cycles.get_cycle_stat(all_cycles[:, 2], IF[:, 2], func=degree_nonlinearity)
```
![[DoN of cycles.png|500]]

---
- **高振幅週期與非線性度的關係**：
    - 高振幅週期的頻率通常穩定（較低的非線性度）。
    - 非線性度可能隨頻率或噪聲的變化而增加。
- **遮罩週期與所有週期的比較**：
    - 遮罩後的週期分佈更集中，反映信號的主要振盪特徵。
    - 被排除的低振幅週期通常表現出更高的非線性度，可能包含更多噪聲。

---
more application
![[HHT with cycle threshold.png]]

more info. [Within-cycle instantaneous frequency profiles report oscillatory waveform dynamics | Journal of Neurophysiology](https://journals.physiology.org/doi/full/10.1152/jn.00201.2021)

---
Cycle class

`C = emd.cycles.Cycles(IP[:, 2])`，已經初始化
- `get_cycle_vect(phase, mode='augmented'))`-> cycle_vect，可以透過參數增加一個週期範圍
- `get_inds_of_cycle(circle的序號)`
- `C.pick_cycle_subset(['max_amp>1', 'duration>12', 'is_good==1'])`
- `C.compute_cycle_metric('max_ampORdurationORampSD', IA[:, 2], func=np.max)`對於每個cycle根據IA計算
- `C.metrics.keys()` -> `df = C.get_metric_dataframe(conditions=['is_good==1', 'duration>12', 'max_amp>1'])`

用於快速的**對一個複雜訊號拆解出來的一個IMF其中每個週期做分析**，並且透過`emd.cycles.phase_align`可以對齊不同cycle進行比較

---
### Cycle疊合的功用
![[hard to tell IMFs.png]]
IF幾乎看不出差異

---
![[IMF in cycle.png]]

---
```python
waveform_linear = np.zeros((30, cycles_linear.max()))*np.nan
instfreq_linear = np.zeros((30, cycles_linear.max()))*np.nan

for ii in range(1, cycles_linear.max()+1):
    inds = cycles_linear[:, 1] == ii
    waveform_linear[:np.sum(inds), ii-1] = imf_linear[inds, 1]
    instfreq_linear[:np.sum(inds), ii-1] = IF_linear[inds, 1]

ctrl_linear = emd.cycles.get_control_points(imf_linear[:, 1], cycles_linear[:, 1])

waveform_nonlinear = np.zeros((30, cycles_nonlinear.max()))*np.nan
instfreq_nonlinear = np.zeros((30, cycles_nonlinear.max()))*np.nan

for ii in range(1, cycles_nonlinear.max()+1):
    inds = cycles_nonlinear[:, 1] == ii
    waveform_nonlinear[:np.sum(inds), ii-1] = imf_nonlinear[inds, 1]
    instfreq_nonlinear[:np.sum(inds), ii-1] = IF_nonlinear[inds, 1]

ctrl_nonlinear = emd.cycles.get_control_points(imf_nonlinear[:, 1], cycles_nonlinear[:, 1])
```

---
### Cycle chain
- **時間連續性**： 如果當前週期與前一個週期在時間上連續（例如，時間差小於一個閾值），則將它分配到同一條鏈。
- **屬性穩定性**： 如果當前週期的屬性（如振幅、頻率）與前一個週期相似（例如，變化在允許範圍內），則繼續加入當前鏈。
- **不連續或屬性不穩定**：
    - 如果上述條件不滿足，則新建一條鏈，鏈的編號遞增。

---
- `C.pick_cycle_subset(['max_amp>1', 'duration>12', 'is_good==1'])`
- `C.subset_vect` ->`C.chain_vect`:只剩下存在的cycle
- `C.compute_chain_timings()`:引入原本訊號的時間屬性
- `C.compute_chain_metric('chain_max_amp', IA[:, 2], np.max)`

![[cycle chain.png|500]]


---
# EMD vs FT based methods

---

| 特性        | Fourier Transform      | 經驗模態分解 (EMD)                        |
| --------- | ---------------------- | ----------------------------------- |
| **基函數**   | 使用預先定義的正弦和餘弦函數作為基函數。   | 基於數據自身特徵，自適應地從數據中提取基函數（本徵模態函數，IMF）。 |
| **時頻局部性** | 提供全局頻率資訊，缺乏時域局部性。      | 提供良好的時頻局部性，能夠描述信號的瞬時頻率變化。           |
| **頻率分辨率** | 對於非平穩信號，頻率分辨率可能較差。     | 能夠有效分辨非平穩信號的不同頻率成分。                 |
| **數據驅動性** | 非數據驅動，需要預先選定基函數。       | 完全數據驅動，無需預先設定任何基函數。                 |
| **應用領域**  | 廣泛應用於各種線性信號處理，如音頻、通信等。 | 廣泛應用於地震資料分析、機械故障診斷、生物醫學信號處理等領域。     |

---

| **處理非平穩信號** | 可能需要短時傅立葉變換（STFT）或小波變換來獲得時頻資訊，但仍存在窗函數選擇等限制。   | 能夠直接處理非平穩信號，無需預先設定窗函數或基函數，具有自適應性。                      |
| ----------- | --------------------------------------------- | ------------------------------------------------------ |
| **頻譜混疊問題**  | 有                                             | 通過分解得到的IMF，可以分離                                        |
| **計算複雜度**   | FFT計算效率高，且有大量DSP元件支持                          | 需要迭代                                                   |
| **邊界效應**    | 在進行傅立葉變換時，信號的邊界可能引入假頻率成分，需要對信號進行窗函數處理以減少邊界效應。 | 在EMD中，邊界效應可能導致分解結果不準確，需要採用適當的邊界處理方法，如鏡像延拓等，以減少邊界效應的影響。 |

---

| **數據長度要求**  | 需要較長的數據段以獲得高的頻率分辨率，對於短時信號，頻率分辨率可能不足。          | 能夠處理短時信號，並提供良好的時頻分辨率，適合分析瞬態事件。                         |
| ----------- | --------------------------------------------- | ------------------------------------------------------ |
| **噪聲敏感性**   | 對噪聲較為敏感，特別是在高頻段，可能需要預先進行噪聲濾除。                 | 對噪聲具有一定的魯棒性，能夠將噪聲與信號的主要成分分離，但在高噪聲情況下，分解結果可能受到影響。       |
| **基線漂移處理**  | 對於存在基線漂移的信號，傅立葉變換可能無法有效分離低頻成分與基線漂移。           | EMD能夠有效分離信號中的基線漂移，將其作為低頻IMF提取出來，從而提高分析精度。              |
| **多分量信號分析** | 在多分量信號中，傅立葉變換可能無法區分頻率接近的成分，導致頻譜混疊。            | EMD能夠將多分量信號分解為不同的IMF，清晰地分離頻率接近的成分，避免頻譜混疊。              |




 
