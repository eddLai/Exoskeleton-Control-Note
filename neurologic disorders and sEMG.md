fibrillation potentials, positive sharp waves, fasciculation potential

ref. https://pmc.ncbi.nlm.nih.gov/articles/PMC3831372/pdf/nihms439498.pdf
amyotrophic lateral sclerosis (ALS))
- 零星尖峰 (Sporadic spikes)： 以非常低的放電率隨機放電。
- 強直尖峰 (Tonic spikes)： 總是表現出一系列有規律的尖峰放電，類似於最小激活時的運動單位動作電位。
- 重複性放電 (Repetitive discharges)： 代表高頻、重複的動作電位放電，例如雙峰、三峰、多峰或長時間的迭代自發放電（即肌陣攣性或神經肌強直性放電）。

### Conclusion
- 病理sEMG會有較低的entropy, 
- 重複性自發性尖峰和正常表面肌電圖基線可以通過它們的最低和最高平均熵值輕鬆地區分
- MEMD 的 IMEn 分析在尺度 4可見顯著差異，而MSE需要尺度6
- 高尺度，強直尖峰具有更高的複雜性水平，並且比零星尖峰

---
characterize spontaneous motor unit firing properties

>based on SampleEn

- approximate entropy (ApEn) 
	- nonlinear complexity domain
- multiscale entropy
- intrinsic mode entropy (IMEn), empirical mode decomposition (EMD)\

decomposes a time series into multiple nonlinear scales representing its inherent oscillatory modes
mode-mixing and mode-misalignment problems of the original EMD algorithm