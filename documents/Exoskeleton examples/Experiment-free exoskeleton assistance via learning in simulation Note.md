[[Experiment-free exoskeleton assistance via learning in simulation.pdf]]
North Carolina State University, Embry-Riddle Aeronautical University,
已有資源
- 翰林：了解肌肉那部份的建模
- 博維：RL可以問

用詞
- handcrafted
- tethered
- substantial labour and time required 
- Human-in-the-loop optimization [8]
- locomotion
- synergistic

*"Goal of NN is decoupling the measurable states (that is, wearable sensor inputs) and unmeasurable states (for example, human joint moments and muscle activations) "*

---
- 虛擬
	- 10s的個人mocap kinematic trajectory data
	- dynamics-aware components of our approach incorporate a 50 d.f.full-body musculoskeletal model with 208 skeletal muscles of lower and upper limbs
	- 使用模擬的機器物理模型"mechanical model of a custom hip exoskeleton used in this study"
	- linear elastic model
	- Hill-type model
	- 
- 資料預處理
	- first classify different locomotion activities and then discretize the gait cycle into several phases
		- segmented gait phase -> manual tuning
		 - transitions
	 - Our previous work imposed predefined kinematic trajectories to drive the steady-state walking of a human in simulation [23]  [24]
- 模型優化
	- 人體 and exoskeleton model 同步訓練為了high-fidelity高保真
- 硬體細節
	- 大腿上的IMU, (IMU) sensor (LPMS-B2, LP-Research)
- 模型細節
	- NN透過Simulink Real-time實現
	- 系統頻率: 100 Hz, namely, 0.01 s using the current thigh angle and thigh angular velocity plus the history data from the past 0.03 s (corresponding to three time steps).
- 驗證方法
	- myoelectric control [9] optimized assistive torque to minimize metabolic rate,

---
### 疑問：
- 怎麼將mocap導入到虛擬？
	- imitation model的reward
- ==All in simulation==
	- "three neural networks in our framework are trained simultaneously in the simulation"
	- "This level of individualization is achieved purely through computer simulation without any online tuning process or human subject training with the device."

實做重點
- 外骨骼跟人的連接方式（現有工具，不然要==自製物理引擎==）
- 人與外骨骼的交互作用力（自己建構算式 or 現有工具）

用跑步機，
可以一併解決KV260暫時沒辦法攜帶的問題

用t-SNE產生視覺化工具
https://www.mropengate.com/2019/06/t-sne.html

模擬：先有動作再有電訊號
實際人體機制：先有電訊號再有動作

opensim training DL model可行嗎
- opensim API 
- simulink 環境

本質上是從肌肉到外骨骼，nature是外骨骼物理量要反推肌肉
八條肌肉，電腦運算量
確定虛擬的EMG是可行的

多交互 simulink
- 考量機械建模, 人體, 多交互 simulink
- EMG模你的文獻
足底感測？


1. mocap
2. motion imitation model -> muscle coordination
3. muscle coordination -> EMG
4. EMG -> EXO
