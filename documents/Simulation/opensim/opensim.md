https://github.com/opensim-org/opensim-core?tab=readme-ov-file
https://opensimconfluence.atlassian.net/wiki/spaces/OpenSim/overview
### [[opensim Download]]
### Terms
- anthropometry:人體測量學
- **PCSA** 是 **Physiological Cross-Sectional Area（生理橫截面積）**
### file and data structure
1. `.trc`: Marker trajectories
2. `.sto`: GRF, COP(center of pressure), EMG data
3. `.mot`: GRF, COP, Joints angle, EMG data, 基本用途:SIMM (Software for Interactive Musculoskeletal Modeling)
4. `.osim`: Load model
5. `.mot`: Load motion
6.  [C3D (.c3d) Files](https://opensimconfluence.atlassian.net/wiki/spaces/OpenSim/pages/53090837/C3D+.c3d+Files)，Mocap, OpenSim 4.0可以轉檔成`.trc`, `.mot`

### [[Workflow of opensim]]

![[Coordinate Systems.png|300]]
### Analysis
- Body Kinematics
- Point Kinematics: 追蹤特定位置
- Muscle Analysis: 長度、速度、歸一化、羽狀角度、主被動纖維力和肌腱力
- Joint Reactions: 負載，來自地面的反作用力
- Induced Acceleration: 肌肉個別力量所產生的加速度
- Force Reporter: 沿路徑的張力, 質心合力

Coordinate controller


主要功能：用於模擬肌肉
- CMC 是基於追蹤已知運動的「控制」
- Forward Dynamics 是從已知的力量推導運動。
- 靜態優化則是一種優化方式，根據特定目標計算每個時間點的最佳肌肉力分佈，但不一定符合生理真實的肌肉激活模式
## Static Optimization(SO)
#### Goal
muscle activations and muscle forces that satisfy 
- positions
- velocities
- accelerations
- external forces

>***"static" means without integrating the equations of motion between time steps***

ignore activation dynamics and tendon compliance

---
#### Core Method
reduce actuation from reserve and residual actuators: 引入虛擬actuators來solve the dynamic equations
#### Requirements
- smooth
- realistic accelerations
- all external forces

#### Example
1. U got:
```
.
├── __MACOSX
│   └── WorkingWithStaticOptimization
└── WorkingWithStaticOptimization
    ├── addAnkleSpring.py
    ├── gait10dof18musc_Strong_actuators.xml : Actuators and External Loads
    ├── opensim.log
    ├── readme.txt
    ├── ResultsSO
    │   ├── Scaled_Model_StaticOptimization_activation.sto
    │   ├── Scaled_Model_StaticOptimization_controls.xml
    │   └── Scaled_Model_StaticOptimization_force.sto
    ├── ResultsSO_StrongActuators
    │   ├── Scaled_Model_StaticOptimization_activation.sto
    │   ├── Scaled_Model_StaticOptimization_controls.xml
    │   └── Scaled_Model_StaticOptimization_force.sto
    ├── StaticOptimization_Setup.xml
    ├── subject01.osim
    ├── subject01_walk_grf.mot
    ├── subject01_walk_grf.xml : 作為external loads
    ├── subject01_walk_IK.mot : 已經mocap轉成IK的檔案
    └── subject_adjusted_Kinematics_q.sto
```

#### OPEN static optimization tools:
Filter Coordinates box??
**_subject01_walk_grf.xml_** as the **External Loads**, [more settings](https://opensimconfluence.atlassian.net/wiki/spaces/OpenSim/pages/53090053/How+to+Use+the+Inverse+Dynamics+Tool)
**setup file**: `.xml`
`Optimizer Failed`可能是模型資料做不到

#### Actuactors
如果關注的是特定肌肉，那就模擬就好
- filtering the input kinematics
- [Residual Reduction Algorithm](https://opensimconfluence.atlassian.net/wiki/spaces/OpenSim/pages/53089669/Residual+Reduction+Algorithm) (RRA) to smooth the kinematics. 會產生`_q.sto`

優化器代價提高，可以使得優先使用肌肉
 $optimal\_force \times activation = force$ 

---
## Computed Muscle Control
用於還原動作
Input
- Desire Kinematics`.mot`
- Tracking Tasks`.xml`
- Actuator Constraints`.xml`
- **Set CMC look-ahead window.** A time window of 0.01 is generally sufficient for muscle activations to change enough to produce the desired accelerations.動作肌肉激活需要時間完成