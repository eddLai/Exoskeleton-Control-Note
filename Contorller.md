### Example
**Reflex Balance Controller**
- 本體感覺反射（proprioceptive reflexes）
- 前庭反射（vestibular reflexes）


MuscleReflex
- muscle length reflex gains: KL
- offsets L0


---

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


參數格式：`mean~standard deviation<minimum, maximum>`
- setpoints
- time delta

肌肉激勵信號：
- `PieceWiseConstantFunction`
- `PieceWiseLinearFunction`
- `Polynomial`

backwards during the jump

Object defined by 高度, 角度
- Objective
- Measure: _fitness function_ of the objective.

---
Reflex entries:reflex arc
- with a specific gains, 
- offsets
- delay.

E.G.
- [MuscleReflex](https://scone.software/doku.php?id=ref:muscle_reflex "ref:muscle_reflex"): proprioceptive reflexes
- [BodyPointReflex](https://scone.software/doku.php?id=ref:body_point_reflex "ref:body_point_reflex"): vestibular