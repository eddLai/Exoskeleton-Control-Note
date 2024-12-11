#### Goal
muscle activations and muscle forces that satisfy 
- positions
- velocities
- accelerations
- external forces

>***"static" means without integrating the equations of motion between time steps***

ignore activation dynamics and tendon compliance

command: `analyze -S subject01_Setup_StaticOptimization.xml`
XML setting: [Static Optimization Settings Files and XML Tags - OpenSim Documentation - OpenSim](https://opensimconfluence.atlassian.net/wiki/spaces/OpenSim/pages/53089631/Static+Optimization+Settings+Files+and+XML+Tags)


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
