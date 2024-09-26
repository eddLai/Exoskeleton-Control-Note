	.### Example
**Reflex Balance Controller**
- 本體感覺反射（proprioceptive reflexes）
- 前庭反射（vestibular reflexes）

---
### S
- name
- symmentric
- Reflex
	- Muscle length: proprioceptive
	- Body point: vestibular
		- target 
		- source
		- KP
		- KV
		- delay

```
ReflexController {
	name = Balance  # 控制器名稱：平衡
	symmetric = 1   # 控制是否對稱

	# 肌肉長度反射 (proprioceptive reflexes)
	MuscleReflex { target = iliopsoas L0 = $L0 KL = $KL delay = 0.010 }
	MuscleReflex { target = glut_max L0 = $L0 KL = $KL delay = 0.010 }
	...
	# 前庭反射 (vestibular reflexes)
	BodyPointReflex { target = iliopsoas source = torso KP = $KP KV = $KV delay = $VDELAY offset = $OFS direction = $DIR }
	...
}
```

---
### Objective

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