ref.
[opensim-org/opensim-core: SimTK OpenSim C++ libraries and command-line applications, and Java/Python wrapping.](https://github.com/opensim-org/opensim-core?tab=readme-ov-file)
[OpenSim Documentation - OpenSim](https://opensimconfluence.atlassian.net/wiki/spaces/OpenSim/overview)
- [[opensim Download]]
- [[Workflow of opensim]]

Coordinate controller


主要功能：用於模擬肌肉
- CMC 是基於追蹤已知運動的「控制」
- Forward Dynamics 是從已知的力量推導運動。
- 靜態優化則是一種優化方式，根據特定目標計算每個時間點的最佳肌肉力分佈，但不一定符合生理真實的肌肉激活模式

## Computed Muscle Control
用於還原動作
Input
- Desire Kinematics`.mot`
- Tracking Tasks`.xml`
- Actuator Constraints`.xml`
- **Set CMC look-ahead window.** A time window of 0.01 is generally sufficient for muscle activations to change enough to produce the desired accelerations.動作肌肉激活需要時間完成