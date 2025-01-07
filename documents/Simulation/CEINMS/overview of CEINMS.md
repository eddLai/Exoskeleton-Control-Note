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
	  text-transform: capitalize;
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
- moment $\tau$ , experiment moment $\tilde{\tau}$ 
- excitation for MTU $e$

---
parameters for each musculotendon unit.
- musculotendon unit’s activation dynamics: excitation $\rightarrow$ activation
- musculotendon contraction dynamics: activation and kinematics $\rightarrow$ force

![[data processing flow showing dynamics.png]]
check<!-- element class="with-border"-->

---
## Activation dynamics
preprocessing 流程跟我們不一樣
- zero-lag fourth-order recursive Butter worthfilter(30Hz)
- full wave rectified 
- Butterworth low-pass filter with 6Hz cutoff  frequency

neural activation to muscle activation model
- non-linear
- one-parameter

---
### muscle’s twitch response in the activation dy namicmodel
- $critically\ damped\ linear\ differential\ system^2$
- discrete form (backward differences)

$$u_j(t) = \alpha e_j(t - d) - \beta_1 u_j(t - 1) - \beta_2 u_j(t - 2) \tag{1.1}
$$

---
#### Constraints
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

### Neural activation to muscle activation
1. one-parameter neural activation to muscle activation model

$$a_j(t) = \frac{e^{A_j u_j(t)} - 1}{e^{A_j} - 1}
$$

$A_j$:non-linear shape factor(-3,0)

>ref. ***An emg-driven musculoskeletal model to estimate muscle forces and knee joint moments in vivo***

---
2. 

$$a_j(t) = \alpha_j^{\text{act}} \ln(\beta_j^{\text{act}} u_j(t) + 1), 0 \leq u_j(t) \leq u_0,$$

$$ a_j(t)= m_j u_j(t) + c_j, u_0 \leq u_j(t) \leq 1.
$$

$A$ constained in 0~0.12

>ref. ***A one-parameter neural activation to muscle activation model: estimating isometric joint moments from electromyograms***

---
# Contraction dynamics
Hill-type muscle model
- muscle fiber: active force generating component
- tendon: passive one

factors of  fibre force
- $active$ produce force at different lengths
- $passive$ fibres to strain
- $fibres\ contraction\ velocity$

three types of model


---
$$F^{mt} = F^t = F^{\text{max}} \left[f_a(\tilde{l}_m) \cdot f_v(\tilde{v}_m) \cdot a + f_p(\tilde{l}_m) + d_m \cdot \tilde{v}_m \right] \cdot \cos \varphi
$$

$$\varphi = \sin^{-1} \left( \frac{L_m^0 \sin \varphi_0}{l_m} \right)
$$

$$l_m = \frac{l_{mt} - l_t}{\cos \varphi}
$$

- pennation:羽狀肌
- $\varphi$ pennation angle of the fibres; $a$ activation; $d_m$ damping element
- functions:$f_a$, $f_v$, $f_p$
![[forceLengthCurves.png]]

---
### Tendon models
1. .integration elastic tendon (IET) model

透過Runge-Kutta-Fehlberg algorithm設定初始值<!-- element class="with-border"-->

numerically integrating a set of ordinary differential equations.，透過$v_m$迭代

$$\epsilon=\frac{l_t-l_{ts}}{l_t}$$

but, stiff MTU equations and robust solutions are not always found

---
2.  equilibrium elastic tendon (EET)

Van Wijngaarden-Dekker-Brent optimization

tendon force-strain relation
求解$$F^{mt}(l_m) = F^t(l_m)$$

, core: $\tilde{v_m}=\frac{d\tilde{l_m}}{dt}$
保證肌腱-肌纖維單元的平衡

3. stiff tendon model:with length equal to the slack length

直接視為一樣$$F^{mt} = F^t$$

---

| 模型類型 | 特性                                | 優點          | 缺點            | 適用場景              |
| ---- | --------------------------------- | ----------- | ------------- | ----------------- |
| IET  | 使用數值積分計算 $$(l_m)、(v_m)$$          | 模型精確，適合彈性肌腱 | 計算成本高，數值不穩定   | 模擬動態系統，如快速運動或劇烈變化 |
| EET  | 使用數值優化求解 $$(F_{MT} = F_T)$$ 的根    | 穩定可靠，適用範圍廣  | 需要數值優化，計算成本中等 | 模擬多種肌腱-肌纖維單元動態    |
| ST   | 假設 $$l_T = l_{TS}$$，直接計算$$(l_m)$$ | 計算簡單，快速     | 無法模擬彈性行為      | 肌腱長度固定或剛性很高的場合    |


---
# App. implementation

---
## Simulation Annealing
Initial condition:
$$X = X_0, \quad T = T_0, \quad X_{\text{opt}} = X_0, \quad f_{\text{opt}} = f(X_0)$$
$$\textbf{Outer Temperature Loop:\ } \text{While } T > T_{\text{min}}:$$

$$\quad \textbf{For Each Temperature:\ }\text{For } i = 1 \text{ to } NT:$$
1. $$\quad \quad \textbf{Neighborhood Search:}$$
$$X'_k = X_k + r \cdot V_k, \quad r \sim \text{Uniform}[-1, 1)$$

2. $$\quad \quad \textbf{Metropolis Criterion:}$$
$$p = \exp\left(-\frac{f(X') - f(X)}{T}\right)$$

3. $$\quad \quad \textbf{Update Solution:}$$
$$X =
\begin{cases}
X', & \text{if } f(X') < f(X) \text{ or } p > p' \\
X, & \text{otherwise.}
\end{cases}$$

$$\quad \quad \textbf{Update Global Optimum:\ }X_{\text{opt}} = X', \quad f_{\text{opt}} = f(X_{\text{opt}})$$

---
step:
$$V_k = V_k \cdot \frac{\text{current acceptance rate}}{0.5}$$

temperature:
$$T = r_T \cdot T$$

Convergence Check:$$|f(X_{\text{opt}}^{(h)}) - f(X_{\text{opt}}^{(h-1)})| < \epsilon, \quad \forall h = H, H-1, \dots, H-N_\epsilon$$
- 引入 Metropolis 準則，讓算法能夠接受較差解，以跳出局部最小值。
- 透過溫度 T的逐漸降低，實現從全域搜索到局部搜索的轉變
- 收斂性：基於多次評估目標函數值的穩定性

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
`.sto`格式opensim使用的
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
[[CEINMS Install]]
## CEINMS Debug
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
1. 需要`.mot`檔案：no
2. 檔名要有_：no
3. 要用相對路徑：no沒有影響
4. subject中的mtu不能砍DOF對不上edl_l

`<trialSet>../../../trials/Rstance1/OvergroundGaitTrials_DM_ngait_og3.xml ../../../trials/Rstance1/OvergroundGaitTrials_DM_ngait_og4.xml ../../../trials/Rstance1/OvergroundGaitTrials_DM_ngait_og5.xml</trialSet>`
`<externalTorquesFile>..\..\..\inverseDynamics\Rstance1_R2L1_6\OvergroundGaitTrials_DM_ngait_og5\inverse_dynamics.sto</externalTorquesFile>`

`<trialSet>../../../trials/Rstance1/OvergroundGaitTrials_DM_ngait_og3.xml</trialSet>`
`<externalTorquesFile>../../../inverseDynamics/Rstance1_R2L1_6/OvergroundGaitTrials_DM_ngait_og3/inverse_dynamics.sto</externalTorquesFile>`

可以跑但結果異常
```
LmtMa: lmtMa DONE
CalibrationStepCfg 100
Return false
fLatest_.at(0) - fOpt_ = 63777.4 - 55633.3 > 1e-05
Reading subject file: /media/ntk/Exoskeleton/ExoskeletonPowerAsistance/simulation/XML_CEINMS_generator/CEINMS_calibration_XML/subject.xml .
Calibration time: 3676435ms
```

`<excitationsFile>`的位置沒有影響

[[CEINMS_standard_output]]
- Trial的次數
- 或者CEINMS_setup迭代的設定

```
algorithm_params = {
        "noEpsilon": 3,
        "rt": 0.3,
        "T": 200000,
        "NS": 30,
        "NT": 20,
        "epsilon": 1.E-4,
        "maxNoEval": 800000,
    }
```

T大，會在初期廣泛搜尋
$r_t: 0.1 \rightarrow 0.3$ 避免陷入局部最小值
maxNoEval: 800000，已經夠大
