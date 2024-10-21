[[CEINMS a toolbox to investigate the influence of different neural control solutions on the prediction of muscle excitation and joint moments during dynamic motor tasks.pdf]]
Our Tssk is dynamic model
### Terms
- Personalized neuromusculoskeletal (NMS) models
- CEMINMS: Calibrated EMG-Informed NMS Modelling Toolbox
- **模擬退火（simulated annealing）**:一種優化算法，隨機優化算法，逐步減少搜索範圍和隨機擾動的「溫度」，以更大概率找到全局最優解
- Co-contraction Ratio(CCR): 兩肌肉同時激活，提高關節穩定性，患者數值較高（骨關節炎Osteoarthritis或前十字韌帶重建術後Anterior cruciate ligament (ACL) reconstruction）

2015: ***"restricted to static and dynamic optimisation methods, or limited to isometric tasks only"***

EMG-driven and EMG-informed algorithms
- EMG-driven: EMG signals and three-dimensional (3D) joint angles
- EMG-assisted
- static optimisation neural control solutions 

effection
- estimated joint moments
- muscle forces
- muscle excitations, including muscle co-contraction.

optimisation methods cannot predict the muscle co-contraction evident in EMG

***"software developed for research is often tuned to a particular project"***
這正好是我們需要的

---
### IO
In:
- excitation primitives and weighting factors as inputs rather than estimating muscle excitations directly from EMG
- MTU kinematics
- external joint moments calculated with OpenSim

Out:
- with OpenSim musculoskeletal models possessing any number of degrees of freedom (DOF) and musculotendon units (MTU) and can be calibrated to the individual to predict joint moments

Validation:
- Joint moments
- Joint contact forces

---
### workflow
1. calibration
2. neural mapping
3. execution

雙向轉換
$E_i(t) = \sum_{j=1}^{m} w_{ij} P_j(t)$
$E \approx W \times P$

https://simtk.org/projects/motonms: 
## In: C3D file

- Muscle inputs
	- raw EMG data (zero-lag fourth-order recursive Butterworth filter)
		- Pre-processing
			- high-pass filtered(30Hz)
			- full-wave-rectified
			- low-pass filtered (6Hz)
			- Maximum Voluntary Contraction, MVC
			- normalised using data from multiple maximum voluntary contraction trials
		- extract muscle synergies and weighting factors
			- factorisation algorithms
		- synthesise: muscles which EMG data were unavailable（我只要八條肌肉是實際算出來的就好）
			- inearly combining any number of time varying input signals.
- marker trajectories inputs  (zero-lag fourth-order recursive Butterworth filter)
	- cutoff frequency of 8 Hz
- Derivation the information from mocap and EMG
	- external joint moments.: ground reaction forces(GRF) 
	- MTU lengths: musculotendon dynamics
	- moment arms: musculoskeletal
- Intergration to correct each other
	- Neural control solution algorithms: improve the tracking of experimental joint moments
		- EMG-driven
		- EMG-assisted mode
		- Static optimization mode
	- Activation dynamics: muscle excitations -> muscle’s twitch response.
		- a critically-damped linear second-order differential system solutions
			- Lloyd and Besier
			- Manal and Buchanan
	- Musculotendon dynamics: solved by using three computational methods
		- Hill-type muscle
			- a set of ordinary differential equations (ODE) with a Runge-Kutta-Fehlberg algorithm
			- Wijngaarden-DekkerBrent optimisation routine: root of the equilibrium equation between the force produced by the muscle fibres and the tendon
			- consider tendon as an element of infinite stiffness
## Out: files compatible with OpenSim
- .trc
- .mot

---
## Example
34 MTUs and 3 DOF
- hip
- knee flexion-extension
- ankle plantar-dorsi flexion (FE)

Neural mapping: 16 channels of EMG data were mapped to 32 MTUs
musculotendon dynamics: equilibrium elastic tendon, $l_o^m$, $l_s^t$
$A [-3, 0]$, $C_1$ ,$C_2$ $[-1,1]$ globally
activation dynamics: equation 3
MTUs: 11 groups based, posteriorly or anteriorly, lower limb segment
strength coefficient $[0.5, 2.5]$: for scaling peak isometric force of the different muscle groups.

---
### Training and Validation
### EMG-assisted mode:
$\alpha$, $\beta$, $\gamma$, lowest tracking errors
### examination:
goal: the effect of different neural control solution
##### muscle co-contraction
co-contraction ratios (CCR) of FE moments (Mf and Me respectively)
$$CCR = 
\begin{cases} 
1 - \frac{M_e}{M_f}, & \text{if } M_f > M_e \\
\frac{M_f}{M_e} - 1, & \text{otherwise}
\end{cases}
\tag{6}
$$
### Validation Result
RMSE 0.18 Nm/kg and 0.24 Nm/kg
Problem: 因為 iliopsoas 肌肉的激發信號, 髖關節的屈曲力矩沒有被準確預測

---
## Idea from disscusion
##### CCR
loading phase: 髖關節和膝關節, CCR較高
late stance phase: 單方向動作（屈曲或伸展）
##### Preprocessing
amplitude-normalised EMG 
- normalizing to maximum EMGs recorded from a variety of maximum exertion isometric and dynamic tasks.

##### Muscle selection
CSA，Cross-Sectional Area
each neuro-anatomical group

- EMG-assisted mode (as Sartori et al.)
	- 縫匠肌（gracilis）
	- 裁缝肌（sartorius）
	- 股內側肌（vastus medialis）
	- 腓腸肌內側頭（gastrocnemius medialis）
	- 腓骨肌群（peroneus group）
- The EMG-assisted mode
	- 對深度肌肉有EMG
	- 交叉干擾（cross-talk）和雜訊
- multiple-DOF EMG-driven mode
	- knee and ankle joints,
- EMG-informed modes
	- static optimisation
	- individual’s neural solution to generate movement: predict knee joint contact forces(tibiofemoral joint best)

ANS: EMG-assisted mode
CAUTION:
- 肌肉招募策略的簡化
	- **多次迭代校準和激發預測**
	- **同時校準和預測激發**
MOtoNMS 用來做預處理
https://myaidrive.com/eDwLLFLted2mjpbMuMw4uW/CEINMS_-a-to.pdf

![[CEINMS data preparation pipeline in MATLAB.png|500]]

Adjusted muscle excitations in conjunction with MTU lengths and moment arms from OpenSim are used as inputs to estimate MTU forces and joint moments from a single experimental trial.
![[Adjusted muscle excitations in conjunction with opensim output.png]]