![[pipeline of building Digital Twins.png]]
![[correct the pipeline]]
tools: [[SCONE]]用來RL training, [[overview of opensim]]用來進行IK推測, [[CEINMS app.]], EMG-informed methods or EMG-driven methods?
target: [[mocap+emg standing and walking sim]], [[level of fatigue from EMG]]

---
ref. [[Robust_Real-Time_Musculoskeletal_Modeling_Driven_by_Electromyograms.pdf]]
>"predicting joint moments from motor tasks"
>"framework can operate online on low power embedded systems"
==表示目前沒有的技術成分==
## software components:
使用ANSI C++
- external recording devices
- OpenSim API
>"real-time inverse kinematics (IK) and inverse dynamics (ID) performed using the OpenSim API"
>"The IK problem in OpenSim is solved via static optimization"
- computation of musculotendon kinematics(Multidimensional Cubic BSpline (MCBS) method)
- CEINMS

## Hardwares
- TCP/IP direct connection to external EMG amplifiers -> ~~amplitude-normalized linear envelopes~~(一致) -> filter沒有用帶通，其它都一樣
	- ~~high-pass filtering, full-wave rectification, and low-pass filtering~~
	- amplitude normalization: ==peak-processed values== for ==musculotendon unit (MTU) force-production modeling==
		- isometric maximal voluntary contractions (MVCs)
		- dynamic trials
- TCP/IP direct connec tion to MOCAP

---
### Terms
- physiological electromechanical delay (EMDs).


需要muscle-tendon kinematics