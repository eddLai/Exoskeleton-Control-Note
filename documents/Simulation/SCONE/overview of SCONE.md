[[Predicting gait adaptations due to ankle plantarflexor muscle weakness and .pdf]]
# SCONE core idea
使用演化學習CMA-ES方法對各個步態階段所需達成的狀態進行數值優化，以達到符合生物學的人體動作模擬。

forward dynamic of neuromuscleskeleton model propulsion
>原本的用途 ***"gait adaptations arise from weakness or contracture of the plantarflexor muscles."*** 

用作小差異的資料衍生

---
# Keywords in SCONE 
- **case sensitive**.
- Predictive simulations
- Evaluate Scenario: 本質上就是做forward simulation
- Optimize Scenario: 配合[JumpMeasure](https://scone.software/doku.php?id=ref:jump_measure "ref:jump_measure")：用於控制優化算法的跌代行為
- [SimulationObjective](https://scone.software/doku.php?id=ref:simulation_objective "ref:simulation_objective")

`^E`：查看這別權重
`^f5`：開始訓練

---
# SCONE operating options
***SCONE is simulator-agnostic***，可以自己開發simulator介面使用C++
optimize both model and control parameters

model fall at the end of a gait simulation，為了遵守最低能量使用
- max_duration 調大
- disable the effortMeasure
- noise is added to the system

加入額外物件：加在模型檔裡頭model requirements
- actuator
- collision shapes
- contact force models
- limit force(structural resistance)
- forward simulation performance(OpenSim model需要檢查)

---
# Environment
- Movement Duration??
- [[SCONE Download]]

---
ref. https://github.com/tgeijten/scone-studio
# Components Structure
## feed-forward or back-forward components
- [[Model]]
- [[Variable]]
- [[Contorller]]
	- 分類
		- open-loop
		- closed-loop
		- include `ScriptController`
	- 列表
		- FeedForwardController 回饋系統
		- TrackingController 附帶PID追蹤的回饋系統
		- PerturbationController模擬擾動
		- ExternalController
		- MirrorController用於對稱動作
		- GaitStateController根據步態階段進行部署
		- SequentialController可以做到動作間的transition
		- ReflexControllera模擬神經放電到肌肉的過程，delayed actuator 的功用 https://www.youtube.com/watch?v=pgaEE27nsQw
- [[Objective(Goad task)]]
	- Combination of Measures
- Optimizer

## File types
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
# SCONE script control
Feedforward Controller
一個事先控制好的excitation, `ScriptControllerJump.lua`
$$excitation = offset[i] + t * slope[i]$$


---
# More info
[[SCONE python based API and SCONE gym]]
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
