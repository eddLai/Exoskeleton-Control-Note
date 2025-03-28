從已知的力量推導運動。
1. Forward Dynamics with Known Controls: 需要adding a controller
2. [[Shooting Methods]]
3. Reinforcement Learning (RL)  [Reinforcement learning with musculoskeletal models](https://osim-rl.kidzinski.com/)
4. Direct Collocation: [OpenSim Moco](https://opensim-org.github.io/opensim-moco-site/)

---
### manually selected excitations
[Opening and Restoring Excitation Editor - OpenSim Documentation - OpenSim](https://opensimconfluence.atlassian.net/wiki/spaces/OpenSim/pages/53089919/Opening+and+Restoring+Excitation+Editor)\
可以用Excitation editor去處理CEINMS生出的檔案\
Save the excitations to a controls file (e.g., **leg69_Forward_Controls_<muscle_name>.xml**).\
怎麼把CEINMS的結果輸入到這裡頭?

![[manually excitation.png]]

---
需要自動轉檔
```
<?xml version="1.0" encoding="UTF-8" ?>
<OpenSimDocument Version="30000">
	<ControlSet name="SwingControls">
		<defaults />
        <objects>
			<ControlLinear name="bifemlh_r.excitation">
				<is_model_control>true</is_model_control>
				<extrapolate>true</extrapolate>
				<default_min>0.02</default_min>
				<default_max>1</default_max>
				<filter_on>false</filter_on>
				<x_nodes>
					<ControlLinearNode>
						<t>0</t>
						<value>0.02</value>
					</ControlLinearNode>
					<ControlLinearNode>
						<t>0.0666666666666667</t>
						<value>0.02</value>
					</ControlLinearNode>
					<ControlLinearNode>
						<t>0.133333333333333</t>
						<value>0.02</value>
					</ControlLinearNode>
					<ControlLinearNode>
						<t>0.2</t>
						<value>0.02</value>
					</ControlLinearNode>
					<ControlLinearNode>
```

---
### Static Optimization (SO)
找解，應該用不到

---
