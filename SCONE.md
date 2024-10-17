### Tasks
- Movement Duration??
- [[SCONE Download]]

---
https://github.com/tgeijten/scone-studio
### Structure
feed-forward or back-forward
- [[Model]]
- [[Variable]]
- [[Contorller]]
	- open-loop
	- closed-loop
	- includev `ScriptController`
- [[Objective(Goad task)]]
	- Combination of Measures
- Optimizer

File name:
- `.scenario`, based on **[zml](https://github.com/tgeijten/zml)**
- `.osim`contains the rule of the forces, such as Slippery Slope
- `.lua`[[lua self-defined script]] for Controller, Measure, 

---
### Keywords in SCONE 
**case sensitive**.
Predictive simulations

[SimulationObjective](https://scone.software/doku.php?id=ref:simulation_objective "ref:simulation_objective")
[JumpMeasure](https://scone.software/doku.php?id=ref:jump_measure "ref:jump_measure")

`^E`：查看這別權重
`^f5`：開始訓練

---
[[SCONE API python based]]
SCONE的核心是怎麼實現的?
從MESSAGE LOG去回推他的code
先找到完整的src