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
list: https://web.ntnu.edu.tw/~algo/Signal.html
# Recall system and signals
- $h(t)_{系統衝擊響應}$，為$\delta(x)_{Dirac\ delta單位脈衝函數}$輸入$LTI$系統所得到的響應
- LTI系統：線性響應, 時不變性（系統輸出與響應有相同位移）
- 系統響應：標準信號的輸出
- 系統輸出是信號與系統函數的卷積
$$y(t) = x(t) \ast h(t) = \int_{-\infty}^{\infty} x(\tau) h(t - \tau) \, d\tau.
$$
- [[Analytic signal and Hilbert Transform]]

---
MSE
經驗模態分解法：
瞬時頻率：透過analytic signal

https://www.entropyhub.xyz/_downloads/40d9c1910993d9509e60865d940bb066/EntropyHubGuide.pdf

intrinsic mode function
intrinsic mode entropy (IMEn):based on the recently developed multivariate empirical mode decomposition (MEMD) method
IMF: 波動是0，上下差小於1

- [[neurologic disorders and sEMG]]
- [[level of fatigue from EMG]]