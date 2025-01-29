---
bg: "[[NTKLab_white bg.png]]"
autoSlide:
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
	}
	.with-border{
		border: 1px solid red;
	}
</style>
<grid drag="70 10" drop="-3 40">
Robust Real-Time Musculoskeletal Modeling Driven by Electromyograms 
<!-- element style="font-size: 40px;align: left; text-align: left;color: white"-->
</grid>

<grid drag="70 10" drop="-3 70">
Guillaume Durandau , Student Member, IEEE, Dario Farina, Senior Member, IEEE, and Massimo Sartori
</grid>

<!-- slide bg="../../NTKLab_white bg_cover_resize.png"-->

---

## 摘要
ref. [[Robust_Real-Time_Musculoskeletal_Modeling_Driven_by_Electromyograms.pdf]] 

6DOF下肢模型
- 比較IK, ID實時和離線方法的結果
- 比較modeling的EMG與真實的sEMG結果
>"predicting joint moments from motor tasks"
>"framework can operate online on low power embedded systems"

==螢光筆表示目前我們沒有的技術==

---
## 主要成果
real-time modeling在嵌入式系統上的可行性
![[Real-time ID results.png|800]]

---
![[Comparison of EMG-excitation from sEMG and modeling.png]]

---
## software components:
使用ANSI C++
- external recording devices
- OpenSim API
- computation of musculotendon kinematics(Multidimensional Cubic BSpline (MCBS) method) [nihms342948.pdf](https://pmc.ncbi.nlm.nih.gov/articles/PMC3264840/pdf/nihms342948.pdf)
- CEINMS

---
## Modeling Framework
![[Modeling framework I of real-time system modeling.png|900]]

---
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

---

## Discussion  and Conclusion
- 預測踝部屈伸力矩方面優於膝部屈伸力矩，這是由於膝部有更多的主動肌肉參與，而踝部的肌肉數量較少。
- EMG激發與產生力量之間的非比例關係
- "real-time multi-DOF modeling formulation provides a unique MTU force solution that satisfies all DOFs simultaneously and is therefore more generalizable across novel conditions." 解決傳統模型上一次只考慮單一DOF會導致的多模擬MTU解之問題。

---
Detailed staged of using OpenSim API

附件: 請點選[[comparison of our pipeline to others]]
![[data generated from the pipeline.png|900]]

---
1. BSpline coefficients necessary for the estimation of Lmt and MA
2) Lmt nominal values for all MTUs spanning the anklesubtalar-flexion, ankle flexion-extension andkneeflexion extension DOFs.
3) subject-specific val ues of optimal fiber length and tendon slack length, each MTU
4) constraint optimization -> EMG-to-activation shape factor parameter
	- Parameters are varied using a simulated annealing procedure

---
## Opensim建置流程之討論
- "real-time inverse kinematics (IK) and inverse dynamics (ID) performed using the OpenSim API"
- "The IK problem in OpenSim is solved via static optimization"
- root mean squared error (RMSE) to check marker between virtual and MOCAP
	- =="Kalman filter to process IK-generated joint angles"==, parameters: [Kalman smoothing improves the estimation of joint kinematics and kinetics in marker-based human gait analysis - ScienceDirect](https://www.sciencedirect.com/science/article/pii/S0021929008004685)
- 6 lower extremity DOFs defining the kine matics of the 13 selected MTUs