- Body Kinematics
- Point Kinematics: 追蹤特定位置
- Muscle Analysis: 長度、速度、歸一化、羽狀角度、主被動纖維力和肌腱力
- Joint Reactions: 負載，來自地面的反作用力
- Induced Acceleration: 肌肉個別力量所產生的加速度
- Force Reporter: 沿路徑的張力, 質心合力

- [[Induced Acceleration Analysis(IAA)]]: 個別肌肉力量對模型質心加速度
- [Probes - OpenSim Documentation - OpenSim](https://opensimconfluence.atlassian.net/wiki/spaces/OpenSim/pages/53089593/Probes): 評估指標
	- SystemEnergyProbe: 總能
	- Umberger2010MuscleMetabolicsProbe: 肌肉代謝功率
	- OpenSim Actuator and Joint internal power Probe: Actuator

---
input:
- states
	- generalized coordinates (e.g., joint angles))
	- speeds (e.g., joint angular velocities)
	- Muscle activation and fiber length
- controls: control parameters in optimization problems
	- Muscle excitations are an example
- external loads:  forces or torques applied between the ground (or world) and the bodies of a model