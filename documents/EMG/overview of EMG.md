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
<grid drag="60 10" drop="-3 40">
Overview of our EMG processing procedure
<!-- element style="font-size: 35px;align: left; text-align: left;color: white"-->
</grid>

<grid drag="50 10" drop="40 70">
賴宏達、劉智翔
<!-- element style="font-size: 40px;align: right; text-align: right"-->
</grid>

<!-- slide bg="../../NTKLab_white bg_cover_resize.png"-->

---
# Summary
1. Cygnus, protocol:BT 
2. high-pass filter: `filted_emg = self.h_filter.filtfilt(signal)`
3. notch filter:`filted_emg = self.n_filter.filtfilt(filted_emg)`
4. Rectification: `rect_emg = np.abs(filted_emg)`
5. Get the envelope using low-pass filter: `envelope = self.l_filter.filtfilt(rect_emg)`
6. normalize_data to `[0,1]`==標準差不會是1==

---
# Data collection
>- Cygnus version: 0.28.0.7
>- Operative system: Windows
>- Device ID: STEEG_DG819202
>- Device bandwidth: DC to 131 Hz
>- Device sampling rate: 1000 samples/second
>- Data type / unit: non-EEG / micro-volt (uV)
>- Bandpass filter: None
>- Notch filter: None

New hardware options
- [ultimaterobotics/uMyo](https://github.com/ultimaterobotics/uMyo)
- Intan RHD2000 series
- 大型儀器：[Delsys – Wearable Sensors for Movement Sciences - Delsys](https://delsys.com/)

---
# Analysis methods
background: [[recall signal and system]],
list: https://web.ntnu.edu.tw/~algo/Signal.html
- [[frequency analysis]]
- [[signal decomposition]] -> [[applications of EMD using emd library]] <!-- element class="with-border"-->
- [[statistics methods]]
- [[entropy]]

---
==EMG is dynamic or non-sinusoidal signals.==

[[Comparison between EMD and Transforms]]<!-- element class="with-border"-->

儘管傅立葉能夠拆解，harmonics can create interpretation issues
>ref. [EMD Tutorials — emd 0.6.2 documentation](https://emd.readthedocs.io/en/stable/emd_tutorials/index.html)
>傅立葉轉換會為了還原某些信號而產生低頻信號的諧波，卻無法跟高頻波分離

---
### Denoising Methods
- muscle artifact (MA)
- ocular artifacts
- Baseline wander
- CEEMDAN

---
# EMG onset detection
MUAPs:肌肉基本運動單元，包含肌肉纖維及神經元
ref. [EMG signal filtering based on Empirical Mode Decomposition - ScienceDirect](https://www.sciencedirect.com/science/article/pii/S1746809406000085?ref=pdf_download&fr=RR-2&rr=8f55c59e1863843f)

採用的signal characteristics
- Standard Deviation (SD)
- Period of time
- % Maximum Voluntary Contraction
- % Maximum EMG Amplitude

ref. [[Review of electromyography onset detection methods for real-time control of robotic exoskeletons.pdf]]

---
對於從訊號到動作的轉換：用EMG偵測動作的啟動，會比實際動作早。
- Visual inspection
- threshold: SNR or energy value
	- Single Threshold (ST)
	- Double T hreshold (DT) 
	- Adaptive Threshold (AT)
- statistics
	- Approximated Generalized Likelihood Ratio (AGLR)
	- Cumulative Sum (CUSUM)
- ML

---
# 更進一步的pattern分析
目前分成三個面向正在研究中 2024/12/21
- [[neurologic disorders and sEMG]], 引入EMD classifier
- [[level of fatigue from EMG]]
- [[musculoskeletal modeling in simulation]] <!-- element class="with-border"-->


---
目前EMG處理方向
1. 利用新的EMG分析方法重新理解SCONE生成的結果，以及收到的資料(資料分析中)
	1. 初步的分析方法實施(需要從數學到coding)
	2. 建立EMG手部資料之實驗建置以活用`libemg`工具(1~2天)，[Feature Extraction — libemg 1.0.0 documentation](https://libemg.github.io/libemg/documentation/features/features.html)
2. 用線上資料庫測試fatigue方案，回報LibEMG的使用結果
3. 嘗試用EMD這個新的數學工具去重新檢查大波動的資料在哪裡

---
新的Modeling方向
1. 重新按照這個文獻[[Robust_Real-Time_Musculoskeletal_Modeling_Driven_by_Electromyograms Note]](影片在Linux本機上), [EMG video](https://youtu.be/W168hIQggFs?si=Bp_D66jkOJBNaAu2) 的做法做一次，至少會完成inversed-problem的整合
	- Calibration procedure
	- BSpline coefficients
	- EMG-data driven
	- 確認Kalman filter to process IK-generated joint angles
>	parameters: [Kalman smoothing improves the estimation of joint kinematics and kinetics in marker-based human gait analysis - ScienceDirect](https://www.sciencedirect.com/science/article/pii/S0021929008004685)

2. 想辦法結合Muscle Fatigue Analysis Using OpenSim