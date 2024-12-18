
# 現在方案
1. Cygnus, protocol:BT 
>Cygnus version: 0.28.0.7
>Operative system: Windows
>Device ID: STEEG_DG819202
>Device bandwidth: DC to 131 Hz
>Device sampling rate: 1000 samples/second
>Data type / unit: non-EEG / micro-volt (uV)
>Bandpass filter: None
>Notch filter: None

1. high-pass filter: `filted_emg = self.h_filter.filtfilt(signal)`
2. notch filter:`filted_emg = self.n_filter.filtfilt(filted_emg)`
3. Rectification: `rect_emg = np.abs(filted_emg)`
4. Get the envelope using low-pass filter: `envelope = self.l_filter.filtfilt(rect_emg)`
5. normalize_data to `[0,1]`==標準差不會是1==
6. 
# Data collection
硬體突破：
- [無線EMG貼片](https://www.bio-translational-exoskeleton.com/)

可能要用來配合建立DQN的模型

---
# Models
MUAPs:肌肉基本運動單元，包含肌肉纖維及神經元
### Denoise方法
- muscle artifact (MA)
- ocular artifacts
- Baseline wander
- CEEMDAN

---
# Analysis methods
background: [[recall signal and system]]
注意是否為==EMG is dynamic or non-sinusoidal signals.==
儘管傅立葉能夠拆解，但是harmonics, can create interpretation issues
>ref. [EMD Tutorials — emd 0.6.2 documentation](https://emd.readthedocs.io/en/stable/emd_tutorials/index.html)
>傅立葉轉換會為了還原某些信號而產生低頻信號的諧波，卻無法跟高頻波分離

list: https://web.ntnu.edu.tw/~algo/Signal.html
- [[frequency analysis]]
- [[signal decomposition]]
- [[statistics methods]]
- [[entropy]]

---
# App.
- [[neurologic disorders and sEMG]]
- [[level of fatigue from EMG]]
- [[musculoskeletal modeling in simulation]]

ref. [[Review of electromyography onset detection methods for real-time control of robotic exoskeletons.pdf]]

EMG偵測動作的啟動，會比實際動作早。
- Visual inspection
- threshold: SNR or energy value
	- Single Threshold (ST)
	- Double T hreshold (DT) 
	- Adaptive Threshold (AT)
- statistics
	- Approximated Generalized Likelihood Ratio (AGLR)
	- Cumulative Sum (CUSUM)
- ML

signal characteristics
- Standard Deviation (SD)
- Period of time
- % Maximum Voluntary Contraction
- % Maximum EMG Amplitude