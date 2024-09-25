- Model
- Controller
- Contorller
	- open-loop
	- closed-loop
- Goad task(Objective), Combination of Measures
- Optimizer

`.scenario`, based on **[zml](https://github.com/tgeijten/zml)**
Predictive simulations

Keywords in SCONE are **case sensitive**.

Contror:
- include or exclude Actuator, 
- time 
- signature

code example:
```C
# Controller for the Model
FeedForwardController {
	symmetric = 1
 
	# Function for feed-forward pattern
	PieceWiseConstant {
		control_points = 2
		control_point_y = 0.3~0.01<0,1> # Initial y value of control points
		control_point_dt = 0.2~0.01<0,1> # initial delta time between control points
	}
}
```
feed-forward pattern? 


`Windows → Parameters`
參數格式：`mean~standard deviation<minimum, maximum>`
- setpoints
- time delta

肌肉激勵信號：
- `PieceWiseConstantFunction`
- `PieceWiseLinearFunction`
- `Polynomial`

backwards during the jump


