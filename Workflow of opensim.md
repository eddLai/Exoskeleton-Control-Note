![[opensim workflow.png]]
1. [[opensim data collection]]
2. The OpenSim Model
3. Simulation Pipelines (Workflows)
4. Common Pre-Processing Steps
	1. Importing Experimental Data
	2. Scaling: 現在mocap已經整合了scaling:mass properties (mass and inertia tensor)
5. The Inverse Problem
	1. Inverse Kinematics: "best match" is expressed as a **weighted least-squares** problem
	2. Inverse Dynamics: ID -> forces, 解方程by Simbody™
	<div style="background-color: white; padding: 10px;">
  <img src="D:\Notes\Exoskeleton-Control-Note\Inverse Dynamics (ID) Tool.png" alt="ID Tool" width="300"/></div>

	1. [[Static Optimization(SO)]]
		1. 根據特定目標計算每個時間點的最佳肌肉力分佈，但不一定符合生理真實的肌肉激活模式
	2. [[Computed Muscle Control]], 無法使用Scripting?
		1. 用途:用來讓muscle逼近輸入的物件座標 `==` 基於追蹤已知運動的「控制」，
		3. 特性:適合較高能量的運動(肌腱動態和彈性儲能，例如跑步)，
		4. 指標:residuals from the CMC
	3. EMG-Informed Methods: [[CEINMS app.]]
6. The Forward Problem:從已知的力量推導運動。
	1. Forward Dynamics with Known Controls: 需要adding a controller
	2. [[Shooting Methods]]
	3. Reinforcement Learning (RL)  [Reinforcement learning with musculoskeletal models](https://osim-rl.kidzinski.com/)
	4. Direct Collocation: [OpenSim Moco](https://opensim-org.github.io/opensim-moco-site/)
7. Frequently Asked Questions About Choosing a Simulation Pipeline
8. [[opensim analysis simulation]]
