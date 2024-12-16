![[pipeline of building Digital Twins.png]]

---
## Comparison to other research
![[correct the pipeline]]
tools: [[SCONE]]用來RL training, [[overview of opensim]]用來進行IK推測, [[CEINMS app.]], EMG-informed methods or EMG-driven methods?
target: [[mocap+emg standing and walking sim]], [[level of fatigue from EMG]]

---
[[Robust_Real-Time_Musculoskeletal_Modeling_Driven_by_Electromyograms Note]]

---
## Detailed staged of using OpenSim API
1. BSpline coefficients necessary for the estimation of Lmt and MA
2. Lmt nominal values for all MTUs spanning the anklesubtalar-flexion, ankle flexion-extension andkneeflexion extension DOFs.
3. subject-specific val ues of optimal fiber length and tendon slack length, each MTU
4. constraint optimization -> EMG-to-activation shape factor parameter
>Parameters are varied using a simulated annealing procedure



---
### Terms
- physiological electromechanical delay (EMDs).


需要muscle-tendon kinematics