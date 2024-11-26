ref. https://scone.software/doku.php?id=doc:sconepy
# model
input: `array`
都會跟一個對於對應elements，都會有個s的項目。joint有joints
### LOAD
- adjust state
- actuator
### INFO
- name
- com
	- `com_pos`
	- `com_vel`
- contact
	- force
	- load
	- power
- [[actuator]]
	- `actuators
- [[body]]
	- `bodies`
- [[muscle]]
	- muscles
	- activation
	- excitation
	- fiber
		- length
		- velocity
	- force
- [[dof]]
	- position
	- velocity
	- dofs
- gravity
- [[joint]] -> joints
- [[leg]] -> legs
- mass
- state
- time
### Setup
- reset
- simulation_end_time
- inputs
	- actuator
	- delayed_actuator
- dof
	- positions
	- velocities
	- 
- delay
	- dof 
		- position
		- velocity
	- muscle
		- fiber length
		- fiber velocity
		- force
		- vestibular
- init
	- muscle_activations
	- state_from_dofs
- log_measure_report
- state
- store_data
### GET
- step_size
- measure
	- measure
	- current_measure
	- final_measure
- simulation
	- `has_simulation_ended`
- write_results

---
# builtins.PyCapsule instance
### Setup
- `evaluate_par_file`
- `replace_string_tags`
- `set_log_level`
- version
- array_dtype
	- float32
	- float64
- dir
	- scone_dir
	- scone_results_dir
### GET
- `load_model`
- is_array_dtype'
	- float32
	- float64
- is_supported

---
# Data Structure
### Quaternion
圖形學和機械模擬中，避免「萬向鎖」問題和更平滑地進行插值（slerp）方面。
$$Q=w+xi+yj+zk$$

`sconepy.Quat`
- `array()`
轉換成不同座標
- `to_euler_???`
- `to_rotation_vector()`

### Vec3
x, y, z描述
`__repr__`, `__str__`