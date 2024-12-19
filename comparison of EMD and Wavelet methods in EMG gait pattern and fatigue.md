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
很棒的工具庫`emd`

用`emd.sift.get_padded_extrema()`來抓peak??一樣是用`from scipy.signal import argrelextrema`的實現
[[Speed_analysis]]中的做法接近
![[peak from emd tool.png]]

透過IA可以得到envelope

---
Application: AM

高頻載波信號的振幅，實現低頻調製信號的嵌入，從而達成訊息傳輸的目的。
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

---
```python
plt.figure(figsize=(16, 10))

# Plot a section of the time-course
plt.axes([.325, .7, .4, .25])
plt.plot(t[:sample_rate*5], x[:sample_rate*5], 'k', linewidth=1)
plt.xlim(0, 5)
plt.ylim(-2.5, 2.5)
plt.title('Original Time-series')

# Plot the 1d Hilbert-Huang Transform
plt.axes([.075, .1, .225, .5])
plt.plot(spec, fcarrier)
plt.plot((0, spec.max()*1.05), (5, 5), 'grey', linewidth=.5)
plt.text(spec.max()/2, 5.5, '5 Hz', verticalalignment='bottom')
plt.plot((0, spec.max()*1.05), (37, 37), 'grey', linewidth=.5)
plt.text(spec.max()/2, 41, '37 Hz', verticalalignment='bottom')
plt.title('1D HHT Spectrum')
plt.yscale('log')
plt.xlabel('Power')
plt.ylabel('Frequency (Hz)')
plt.yticks(2**np.arange(7), 2**np.arange(7))
plt.ylim(fcarrier[0], fcarrier[-1])
plt.xlim(0, spec.max()*1.05)

# Plot a section of the Hilbert-Huang transform
plt.axes([.325, .1, .4, .5])
plt.pcolormesh(t[:sample_rate*5], fcarrier, shht[:, :sample_rate*5], cmap='ocean_r', shading='nearest')
plt.yscale('log')
plt.plot((0, t[sample_rate*5]), (5, 5), 'grey', linewidth=.5)
plt.plot((0, t[sample_rate*5]), (37, 37), 'grey', linewidth=.5)
plt.title('2-D HHT Spectrum')
plt.xlabel('Time (seconds)')
plt.yticks(2**np.arange(7), 2**np.arange(7))

# Plot a the Holospectrum
plt.axes([.75, .1, .225, .5])
plt.pcolormesh(fam, fcarrier, sholo, cmap='ocean_r', shading='nearest')
plt.yscale('log')
plt.xscale('log')
plt.plot((fam[0], fam[-1]), (5, 5), 'grey', linewidth=.5)
plt.plot((fam[0], fam[-1]), (37, 37), 'grey', linewidth=.5)
plt.plot((.5, .5), (fcarrier[0], fcarrier[-1]), 'grey', linewidth=.5)
plt.plot((5, 5), (fcarrier[0], fcarrier[-1]), 'grey', linewidth=.5)
plt.title('Holospectrum')
plt.xlabel('AM Frequency (Hz)')
plt.yticks(2**np.arange(7), 2**np.arange(7))
plt.xticks([.1, .5, 1, 2, 4, 8, 16], [.1, .5, 1, 2, 4, 8, 16])
```

