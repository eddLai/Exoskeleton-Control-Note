
<style>
    .reveal {
        font-family: 'Times New Roman', '標楷體';
        font-size: 30px;
        text-align: left;
        color: black;
        background-size: cover;
        background-position: center;
    }
	.reveal h1,
	.reveal h2,
	.reveal h3,
	.reveal h4,
	.reveal h5,
	.reveal h6 {
	  font-family: 'Times New Roman', '標楷體';
	  color: black;
	  %%text-transform: lowercase%%;
	  text-transform: capitalize;
	}
	.with-border{
		border: 1px solid red;
	}
</style>
<grid drag="60 10" drop="-3 40">
Control  muscleskeletal model using 
<!-- element style="font-size: 35px;align: left; text-align: left;color: white"-->
</grid>

<grid drag="50 10" drop="40 70">
賴宏達、劉智翔、葉亘祐、曾峻魁、Aaron Wang
<!-- element style="font-size: 30px;align: right; text-align: right"-->
</grid>

<!-- slide bg="../NTKLab_white bg_cover_resize.png"-->

---
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
