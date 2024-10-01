[[CEINMS a toolbox to investigate the influence of different neural control solutions on the prediction of muscle excitation and joint moments during dynamic motor tasks.pdf]]
Our Tssk is dynamic model
### Terms
- Personalized neuromusculoskeletal (NMS) models
- CEMINMS: Calibrated EMG-Informed NMS Modelling Toolbox
- **模擬退火（simulated annealing）**:一種優化算法，隨機優化算法，逐步減少搜索範圍和隨機擾動的「溫度」，以更大概率找到全局最優解

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

https://simtk.org/projects/motonms: 
## In: C3D file
- Muscle inputs
	- MTU lengths
	- moment arms
	- external joint moments.
	- raw EMG data (zero-lag fourth-order recursive Butterworth filter)
		- Pre-processing
			- high-pass filtered(30Hz)
			- full-wave-rectified
			- low-pass filtered (6Hz)
			- normalised using data from multiple maximum voluntary contraction trials
		- extract muscle synergies and weighting factors
			- factorisation algorithms
		- synthesise: muscles which EMG data were unavailable（我只要八條肌肉是實際算出來的就好）
			- inearly combining any number of time varying input signals.
- marker trajectories inputs  (zero-lag fourth-order recursive Butterworth filter)
	- cutoff frequency of 8 Hz
- ground reaction forces(GRF) 
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
activation dynamics: equation 3