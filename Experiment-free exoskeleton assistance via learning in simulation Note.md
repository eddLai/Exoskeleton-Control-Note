[[Experiment-free exoskeleton assistance via learning in simulation.pdf]]

了解肌肉那部份的建模，RL可以問博維

handcrafted,  tethered
substantial labour and time required 
Human-in- the-loop optimization [8] and myoelectric control [9] optimized assistive torque to minimize metabolic rate,
first classify different locomotion activities and then discretize the gait cycle into several phases
- segmented gait phase -> manual tuning
 - transitions

Our previous work imposed predefined kinematic trajectories to drive the steady-state walking of a human in simulation[23] [24]

three-layer fully connected network
(IMU) sensor (LPMS-B2, LP-Research) on each thigh


問題是怎麼做到人體端的模擬
North Carolina State University, 
Embry-Riddle Aeronautical University,

Goal of NN is decoupling the measurable states (that is, wearable sensor inputs) and unmeasurable states (for example, human joint moments and muscle activations) 

All in simulation
- "three neural networks in our framework are trained simultaneously in the simulation"
- "This level of individualization is achieved purely through computer simulation without any online tuning process or human subject training with the device."

系統頻率

10s的個人mocap kinematic trajectory data, 
dynamics-aware components of our approach incorporate a 50 d.f.full-body musculoskeletal model with 208 skeletal muscles of lower and upper limbs
使用模擬的機器物理模型"mechanical model of a custom hip exoskeleton used in this study"
linear elastic model: 
人體 and exoskeleton model 同步訓練為了high-fidelity高保真
硬體細節
大腿上的IMU, (IMU) sensor (LPMS-B2, LP-Research)
模型細節
- NN透過Simulink Real-time實現
- 100 Hz, namely, 0.01 s using the current thigh angle and thigh angular velocity plus the history data from the past 0.03 s (corresponding to three time steps).

---
### 疑問：
- 怎麼將mocap導入到虛擬？
