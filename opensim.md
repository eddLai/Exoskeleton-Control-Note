### Terms
- anthropometry:人體測量學

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
    ├── gait10dof18musc_Strong_actuators.xml
    ├── opensim.log
    ├── readme.txt
    ├── subject01.osim
    ├── subject01_walk_grf.mot
    ├── subject01_walk_grf.xml
    ├── subject01_walk_IK.mot
    └── subject_adjusted_Kinematics_q.sto
```

2. OPEN static optimization tools:
Filter Coordinates box??
**_subject01_walk_grf.xml_** as the **External Loads**

---
## CMC