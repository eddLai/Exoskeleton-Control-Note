***SCONE is simulator-agnostic***，可以自己開發simulator介面使用C++
optimize both model and control parameters

propulsion

***"gait adaptations arise from weakness or contracture of the plantarflexor muscles."***
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
- `.par`包含，需要經過`evaluatie`才能變成`.sto`
	- 骨骼關節
		- offset資訊
	- 肌肉
		- 剛度係數 KL: linear stiffness
		- 初始長度（L0）：靜止狀態
		- 彎曲剛度係數（KF）：flexural stiffness
	- 骨骼+肌肉
		- KL
		- KF
	- 動作控制
		- 增益
			- Kp
			- Kv

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
### Message
[[Message LOG example]]
產生`.par`，儲存的機制是？
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
載入動畫
```
Loaded 0023_1.505_1.214.par; dim=53; time=0.055
get_thread_priority() is not implemented for this platform
Terminating simulation at 20.000
Result             = 1.21434
  Gait             = 0 <- 100 * (0.00031097 > 0.05)
    step_velocity  = 1.09222
    step_count     = 38
  Effort           = 0.601143 <- 0.1 * 6.01143
    effort         = 9798.52
    distance       = 21.8697
  MuscleActivation = 0.422046 <- 2000 * 0.000211023
    effort         = 6.19135
    distance       = 21.8697
  DofLimits        = 0.0816146
    ankle_angle_l  = 0 <- 0.1 * 0
    ankle_angle_r  = 0 <- 0.1 * 0
    knee_angle_l   = 0.0416741 <- 0.02 * (2.0837 > 1)
    knee_angle_r   = 0.0399406 <- 0.02 * (1.99703 > 1)
  GRF              = 0.109541 <- 10 * 0.0109541
Evaluation took 12.3344s for 20s (1.62148x real-time)
Results written to /home/eddlai/SCONE/results/241007.175746.H0918v3.RS2.S10WA3K1G14.D20/0023_1.505_1.214.par.sto in 0.223776s
```

---
### UNKNOWN