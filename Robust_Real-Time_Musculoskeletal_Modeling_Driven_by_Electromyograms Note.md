---
bg: "[[NTKLab_white bg.png]]"
autoSlide: 
cssclasses:
  - reveal
---


<grid drag="70 10" drop="-3 40">
level of fatigue from EMG
<!-- element style="font-size: 40px;align: left; text-align: left;color: white"-->
</grid>

<!-- slide bg="NTKLab_white bg_cover_resize.png"-->

---

ref. Robust_Real-Time_Musculoskeletal_Modeling_Driven_by_Electromyograms.pdf, 
6DOF下肢模型，比較實時和離線方法
>"predicting joint moments from motor tasks"
>"framework can operate online on low power embedded systems"
==表示目前沒有的技術成分==

---
## software components:
使用ANSI C++
- external recording devices
- OpenSim API
>"real-time inverse kinematics (IK) and inverse dynamics (ID) performed using the OpenSim API"
>"The IK problem in OpenSim is solved via static optimization"
>root mean squared error (RMSE) to check marker between virtual and MOCAP
>=="Kalman filter to process IK-generated joint angles"==
>>parameters: [Kalman smoothing improves the estimation of joint kinematics and kinetics in marker-based human gait analysis - ScienceDirect](https://www.sciencedirect.com/science/article/pii/S0021929008004685)
>
>6 lower extremity DOFs defining the kine matics of the 13 selected MTUs
- computation of musculotendon kinematics(Multidimensional Cubic BSpline (MCBS) method) [nihms342948.pdf](https://pmc.ncbi.nlm.nih.gov/articles/PMC3264840/pdf/nihms342948.pdf)
- CEINMS
## Hardwares
- TCP/IP direct connection to external EMG amplifiers -> ~~amplitude-normalized linear envelopes~~(一致) -> filter沒有用帶通，其它都一樣
	- ~~high-pass filtering, full-wave rectification, and low-pass filtering~~
		- 256-channelEMGamplifier (OTBioelettronica, Italy)
		- SR: 2048Hz
		- high-passfilter: second-order Butterworthfilter; 30Hz cut-off
		- low-pass filter: second-order Butterworth with; 4Hz cut-off
		- EMG signals channels: 10 muscle groups
	- amplitude normalization: ==peak-processed values== for ==musculotendon unit (MTU) force-production modeling==
		- isometric maximal voluntary contractions (MVCs)
		- dynamic trials
- TCP/IP direct connection to MOCAP(retroreflectives markers)
- different threads within a multi-stage pipeline
	- Computation time histograms是執行real-time運算需要考量的

## 結論與討論
- 預測踝部屈伸力矩方面優於膝部屈伸力矩，這是由於膝部有更多的主動肌肉參與，而踝部的肌肉數量較少。
- EMG激發與產生力量之間的非比例關係
- "real-time multi-DOF modeling formulation provides a unique MTU force solution that satisfies all DOFs simultaneously and is therefore more generalizable across novel conditions." 解決傳統模型上一次只考慮單一DOF會導致的多模擬MTU解之問題。

---
Detailed staged of using OpenSim API

1) BSpline coefficients necessary for the estimation of Lmt and MA
2) Lmt nominal values for all MTUs spanning the anklesubtalar-flexion, ankle flexion-extension andkneeflexion extension DOFs.
3) subject-specific val ues of optimal fiber length and tendon slack length, each MTU
4) constraint optimization -> EMG-to-activation shape factor parameter
>Parameters are varied using a simulated annealing procedure