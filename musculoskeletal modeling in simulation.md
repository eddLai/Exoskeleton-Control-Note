![[pipeline of building Digital Twins.png]]
![[correct the pipeline]]
tools: [[SCONE]]用來RL training, [[overview of opensim]]用來進行IK推測, [[CEINMS app.]], EMG-informed methods or EMG-driven methods?
target: [[mocap+emg standing and walking sim]], [[level of fatigue from EMG]]

ref. [[Robust_Real-Time_Musculoskeletal_Modeling_Driven_by_Electromyograms.pdf]]
>"predicting joint moments from motor tasks"
>"framework can operate online on low power embedded systems"

使用ANSI C++
components:
- external recording devices
- OpenSim API
- computation of musculotendon kinematics(Multidimensional Cubic BSpline (MCBS) method)
- CEINMS

### Terms
- physiological electromechanical delay (EMDs).


需要muscle-tendon kinematics