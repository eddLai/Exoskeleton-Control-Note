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
Application of EMD on Gait Analysis
<!-- element style="font-size: 40px;align: left; text-align: left;color: white"-->
</grid>

<grid drag="50 10" drop="40 70">
Comparison of Empirical Mode Decomposition (EMD) and Wavelet Transform Methods for EMG Gait Pattern and Fatigue Analysis
賴宏達
<!-- element style="font-size: 20px;align: right; text-align: right"-->
</grid>

<!-- slide bg="../../NTKLab_white bg_cover_resize.png"-->

---
## 測試是否可以用EMD方案取代以下幾點：
- Fatigue分析中的
	- 取代STFT: [Mean frequency derived via Hilbert-Huang transform with application to fatigue EMG signal analysis - ScienceDirect](https://www.sciencedirect.com/science/article/pii/S0169260706000472?ref=pdf_download&fr=RR-2&rr=8f3e26022ac98454), [EMG Mean Power Frequency Determination Using Wavelet Analysis](https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=757017)
	- Wavelet: [Frontiers | Comparison of Empirical Mode Decomposition, Wavelets, and Different Machine Learning Approaches for Patient-Specific Seizure Detection Using Signal-Derived Empirical Dictionary Approach](https://www.frontiersin.org/journals/digital-health/articles/10.3389/fdgth.2021.738996/full)
- Filter: [EMG signal filtering based on Empirical Mode Decomposition - ScienceDirect](https://www.sciencedirect.com/science/article/pii/S1746809406000085)

---
## 很棒的工具庫`emd`

用`emd.sift.get_padded_extrema()`來抓peak??一樣是用`from scipy.signal import argrelextrema`的實現
[[Speed_analysis]]中的做法接近
![[peak from emd tool.png]]

透過IA可以得到envelope

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
![[hht_by_phase.png|600]]
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
### EMD 用於分離Harmonic
- **時域分析**：
    - 檢查信號的波形結構，確定是否存在多個極值。
- **波形形狀指標**：
    - 使用指標（如尖銳程度、非正弦指數）來量化信號的非正弦性。
- **相位-振幅耦合分析**：
    - 結合低頻相位與高頻振幅的關係，檢查是否存在真實的跨頻交互。

---
- IF較低，代表waveform shape較平緩
- IF應該要是正值
- **良好的諧波結構**：
    - 信號有規律的波形（例如單一非正弦振盪），每個週期重複，沒有次要極值。
- **不良的諧波結構**：
    - 波形中存在額外的次要極值（secondary extrema），或每個週期波形不一致。

應用上可以用來確保LFP所得正確[Brain Oscillations and the Importance of Waveform Shape - ScienceDirect](https://www.sciencedirect.com/science/article/pii/S1364661316302182?via%3Dihub)