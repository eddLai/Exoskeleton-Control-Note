---
bg: "[[NTKLab_white bg.png]]"
---

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
<grid drag="70 10" drop="-3 40">
musculoskeletal modeling in simulation
<!-- element style="font-size: 40px;align: left; text-align: left;color: white"-->
</grid>

<grid drag="50 10" drop="40 70">
賴宏達、劉智翔
<!-- element style="font-size: 40px;align: right; text-align: right"-->
</grid>

<!-- slide bg="../../NTKLab_white bg_cover_resize.png"-->

---
![[pipeline of building Digital Twins.png]]

---
## Comparison to other research
[[comparison of our pipeline to others]]<!-- element class="with-border"-->

tools: [[overview of SCONE]]用來RL training, [[overview of opensim]]用來進行IK推測, [[overview of CEINMS]], EMG-informed methods or EMG-driven methods?
target: [[mocap+emg standing and walking sim log]], [[level of fatigue from EMG]]

---
### Terms
- physiological electromechanical delay (EMDs).
- Digital human modeling
- mannequin 人體模型

---
Ref.
- [[Robust_Real-Time_Musculoskeletal_Modeling_Driven_by_Electromyograms Note]] MTU model，確認取得正確的opensim model，再投入SCONE
- [[Muscle Fatigue Analysis Using OpenSim Note]] 透過fatigability($k$值)透過empirical maximal endurance models，可以相互確認sEMG計算所得是否正確

---
正在確認
- [[BSpline model and musculoskeletal modeling]]
multidimensional spline function
- EMG-driven的model
- [[overview of CEINMS]]
- 需要muscle-tendon kinematics
