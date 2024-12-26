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
	}
	.with-border{
		border: 1px solid red;
	}
</style>
</style>
<grid drag="70 10" drop="-3 40">
overview of CEINMS
<!-- element style="font-size: 40px;align: left; text-align: left;color: white"-->
</grid>

<!-- slide bg="../../../NTKLab_white bg_cover_resize.png"-->

---

EMG-informed method
>"***Fundamental to these calibrated methods was the ability to validate the outputs against other data not used for calibra tion.***"

ref.
- [[documents/Simulation/papers/CEINMS User Guide 0.9.pdf|CEINMS User Guide 0.9]]
- [[CEINMS - a toolbox to investigate the influence of differentneural control solutions on the prediction of muscle excitationand joint moments during dynamic motor tasks Note]]
- https://github.com/CEINMS/CEINMS

---
## Modes
- Full-predictive open-loop mode(EMG-driven): 
	- EMG signals and 3D joint angles input $\rightarrow$musculotendon forces

![[CEINMS Full-predictive open-loop mode.png]]

---
- Hybrid mode(EMG-driven+SO):
	- optimization algorithms
	- excitation patterns of 不可能有的深層資料
	- 再第一點的資料
- EMG-assisted mode(EMG-informed)
	- optimization to 全部資料
- Static optimisation mode(EMG-informed)
	- 不需要recorded資料

可以使用不同mode到同一個model上

---
## Calibration
non-linearly optimization for different individuals: Simulated Annealing
- close tracking
	- experimental joint moments
	- excitations derived from EMG signals

minimize maximum activation, minimize maximum joint contact forces etc
with predefined boundaries

---
![[CEINMS Calibration.png]]

objective function:

$$F_{\text{obj}} = \alpha \cdot \sum_{k \in DOFs}(\tau_k - \tilde{\tau}_k) ^2+\beta \cdot \sum_{j \in MTUs}( e_j - \tilde{e}_j)^2+\gamma \cdot \sum_{j \in MTUs}( e_j^2)$$

- Joint $k$
- moment $\tau$ , experiment moment$\tilde{\tau}$ 
- excitation for MTU $e$

---
parameters for each musculotendon unit.
- musculotendon unit’s activation dynamics: excitation $\rightarrow$ activation
- musculotendon contraction dynamics: activation and kinematics $\rightarrow$ force

![[data processing flow showing dynamics.png]]
check<!-- element class="with-border"-->

---
### Activation dynamics
preprocessing 流程跟我們不一樣
- zero-lag fourth-order recursive Butter worthfilter(30Hz)
- full wave rectified 
- Butterworth low-pass filter with 6Hz cutoff  frequency

---
muscle’s twitch response in the activation dy namicmodel
- $critically\ damped\ linear\ differential\ system^2$
- discrete form (backward differences)

$$u_j(t) = \alpha e_j(t - d) - \beta_1 u_j(t - 1) - \beta_2 u_j(t - 2) \tag{1.1}
$$

---
Constraints
$$
\beta_1 = C_1 + C_2$$

$$\beta_2 = C_1 \cdot C_2,
$$

$$|C_1| < 1, |C_2| < 1,$$
$$\alpha - \beta_1 - \beta_2 = 1
$$



ref.
- Neuromusculoskeletal modeling: estimation of muscle forces and joint moments and movements from measurements of neural command
- An emg-driven musculoskeletal model to estimate muscle forces and knee joint moments in vivo
- Neuromusculoskeletal modelling and simulation of tissue load in the lower extremities

---
### contraction dynamics

---
### Tendon models


---
## Data Description
- preprocessing 得到 _geometrical_ state
- _musculo-tendon lengths_ 肌腱-肌肉單位的長度
	- By opensim scaling流程
- _moment arms_ 肌肉力矩臂
- _muscle excitations_ sEMG signals
	- 現有已經濾波過

file type: `.mot`, `.sto`

---
### Data input:
- `endheader`
- `nColumns=15` or `dataColumns 15`
- `nRows=1264` or `dataRows 1264`
多列stamps，第一列是`time`
格式要求: 
- muscle names <- `subjectDescFile`
- muscle activation <- excitationsDescFile`inputSignals

`<prefix>_Length.sto`
`<prefix>_MomentArm_<dof_name>.sto`
MuscleAnalysis
`compute_moments`, 
`muscle_list`:需要include all muscles
`moment_arm_coordinate_list`

需要透過MATLAB MOtoNMS轉檔

---
### File hierarchy
background: [[XML file]]
toc
.. toctree::
   :maxdepth: 2

   xsd/ceinmsCalibrationSetup.xsd
   xsd/calibration.xsd

   xsd/subject.xsd
   xsd/inputData.xsd
   xsd/excitationGenerator.xsd

XSD用於驗證XML可否使用

---
### CEINMS modes
`CEINMS -S <path to main XML setup file>`
### optimization algorithm goal: 
`trackedMuscles在實驗中測量的肌肉  || predictedMusclesao沒有在實驗中測量的肌肉`
objective function weightings alpha, beta and gamma

- _openLoop_: means _full-predictive_ 不需要外部反饋e.g. joint moments file
- _Hybrid mode_
> alpha = 1, beta = 0, gamma > 0
> 
> trackedMuscles = none
> 
> predictedMuscles = every muscle without experimental excitations

- _EMG-assisted mode_
> alpha = 1, beta > 1, gamma > 1
> 
> trackedMuscles = every muscle with experimental excitations
> 
> predictedMuscles = remaining muscles

- _Full optimization-driven closed-loop mode_
> alpha = 1, beta = 0, gamma > 0
> 
> trackedMuscles = none
> 
> predictedMuscles = every muscle


### tendon setting:
equilibriumElastic more acc. but stiff less comput. time

---
### CEINMScalibrate
用途: refining muscle parameters(用於muscles->force轉換)
定義:
- cost function: ***error between the estimated and the measured joint moments during a set of tasks.***

---
### 在Linux上編譯
```bash
mkdir build
cd build
cmake ..
make -j4
make install
```

1. 可以一個分兩個：沒影響，但是意義==有待商榷==
```xml
<excitation id="bflh_l">
      <input weight="0.5">LBF</input>
</excitation>
<excitation id="bfsh_l">
      <input weight="0.5">LBF</input>
</excitation>
```

2. subject的mtu要對照到excitation的所有肌肉? -> 剩下的所有mtu可能都要有?，砍掉舊有的一部分做測試。對，必須要完全一樣
	1. 所以把mtu改成跟emg一樣(不行，dof對不上)
```xml
    <excitation id="vas_int_r"/>如果這行刪掉就會報錯
        <!-- <input weight="1">vas_lat_r</input>
    </excitation> -->
    <excitation id="vas_lat_r"/>
        <!-- <input weight="1">vas_lat_r</input>
    </excitation> -->
    <excitation id="vas_med_r"/>
        <!-- <input weight="1">vas_lat_r</input>
    </excitation> -->
```
1. 需要`.mot`檔案
2. 檔名要有_
3. 要用相對路徑

edl_l