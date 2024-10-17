### Tasks
- Movement Duration??
- [[SCONE Download]]

---
https://github.com/tgeijten/scone-studio
### Structure
feed-forward or back-forward
- [[Model]]
- [[Variable]]
- [[Contorller]]
	- open-loop
	- closed-loop
	- includev `ScriptController`
- [[Objective(Goad task)]]
	- Combination of Measures
- Optimizer

File name:
- `.scenario`, based on **[zml](https://github.com/tgeijten/zml)**
- `.osim`contains the rule of the forces, such as Slippery Slope
- `.lua`[[lua self-defined script]] for Controller, Measure, 
- `.par`包含
	- 骨骼關節
		- offset資訊
	- 肌肉
		- 剛度係數 KL: linear stiffness
		- 初始長度（L0）：靜止狀態
		- 彎曲剛度係數（K）：flexural stiffness
	- 骨骼+肌肉
		- KL
		- KF

---
### Keywords in SCONE 
**case sensitive**.
Predictive simulations

[SimulationObjective](https://scone.software/doku.php?id=ref:simulation_objective "ref:simulation_objective")
[JumpMeasure](https://scone.software/doku.php?id=ref:jump_measure "ref:jump_measure")

`^E`：查看這別權重
`^f5`：開始訓練

---
[[SCONE API python based]]
SCONE的核心是怎麼實現的?顯示出來就是標準的RL畫面
從MESSAGE LOG去回推他的code
```
Created model H0918v3; dofs=9 muscles=18 mass=74.5314
Could not convert folder Documents: 0000022ED925B540
Could not get SCONE data folder, using /SCONE instead
Created model H0918v3; dofs=9 muscles=18 mass=74.5314
Loaded Tutorial 4b - Fast Gait - OpenSim.scone; dim=62; time=0.192
Terminating simulation at 1.600
Result             = 100.683
  Gait             = 98.0547 <- 100 * (0.980547 > 0.05)
    step_velocity  = 0.0291802
    step_count     = 5
  Effort           = 0.748368 <- 0.1 * 7.48368
    effort         = 966.573
    distance       = 1.73293
  MuscleActivation = 1.09562 <- 2000 * 0.000547811
    effort         = 1.27357
    distance       = 1.73293
  DofLimits        = 0.202038
    ankle_angle_l  = 0 <- 0.1 * 0
    ankle_angle_r  = 0 <- 0.1 * 0
    knee_angle_l   = 0.0883834 <- 0.02 * (4.41917 > 1)
    knee_angle_r   = 0.113655 <- 0.02 * (5.68273 > 1)
  GRF              = 0.582764 <- 10 * 0.0582764
Evaluation took 1.86822s for 1.6s (0.856429x real-time)
```
先找到完整的src