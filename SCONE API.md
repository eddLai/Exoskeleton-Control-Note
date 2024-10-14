- 可以用來控制外骨骼的力量？有Controller就可以吧，需要研究外骨骼物件，我需要command 跟 python作用在同個空間才行。
### API characteristic
SCONE py
- Data format
	- biomechanical sensors and actuators via NumPy arrays
	- **neural delays** to sensors and actuators ?
	- **reward shaping** is possible

---
### ENV setup
真的要用python3.9才行
```bash
(exo) eddlai@eddlai-ROG-Flow-X13-GV301RE-GV301RE:~/SCONE/SconePy$ /home/eddlai/miniconda3/envs/exo/bin/python /home/eddlai/SCONE/SconePy/sconetools.py                                                                                                  
sconepy found at /opt/scone/lib                                                                                             
19:10:20 Successfully initialized OpenSim3 version 3.3-2021-01-28                                                           
19:10:20 Loaded settings from /home/eddlai/.config/SCONE/scone-settings.zml 
```

---
ref. https://scone.software/doku.php?id=doc:sconepy
iterate `model.`
- `bodies()`
	- `name`
	- `mass`
	- `inertia_diag`
- `muscles()`
	- `name`
	- `fiber_length_norm`
	- `fiber_velocity_norm`
	- `force_norm`
- `dofs()`
- `actuators()`
- `status()`

`model.reset`, `.set_store_data`: 歸零，儲存資料，


---
## Simple Example
The method of randomizing used in Example
```python
	rng = np.random.default_rng(random_seed)

	# Initialize muscle activations to random values
	muscle_activations = 0.1 + 0.4 * rng.random((len(model.muscles())))
	# 產生一個陣列，為每條肌肉設置隨機化
```


```python
type(model): <class 'sconepy.Model'>
model: <sconepy.Model object at 0x7f71080359b0>
body ground mass=0.000 inertia=[ 0.000000 0.000000 0.000000 ]
body pelvis mass=11.777 inertia=[ 0.102800 0.087100 0.057900 ]
body femur_r mass=9.301 inertia=[ 0.133900 0.035100 0.141200 ]
body tibia_r mass=3.708 inertia=[ 0.050400 0.005100 0.051100 ]
body calcn_r mass=1.250 inertia=[ 0.001400 0.003900 0.004100 ]
body femur_l mass=9.301 inertia=[ 0.133900 0.035100 0.141200 ]
body tibia_l mass=3.708 inertia=[ 0.050400 0.005100 0.051100 ]
body calcn_l mass=1.250 inertia=[ 0.001400 0.003900 0.004100 ]
body torso mass=34.237 inertia=[ 1.474500 0.755500 1.431400 ]
muscle hamstrings_r L=1.306 V=0.000 F=0.137
muscle bifemsh_r L=0.891 V=0.000 F=0.009
muscle glut_max_r L=1.055 V=0.000 F=0.016
muscle iliopsoas_r L=0.547 V=0.000 F=0.002
muscle rect_fem_r L=0.620 V=0.000 F=0.005
muscle vasti_r L=1.106 V=0.000 F=0.028
muscle gastroc_r L=1.145 V=0.000 F=0.037
muscle soleus_r L=1.342 V=-0.000 F=0.171
muscle tib_ant_r L=0.606 V=0.000 F=0.005
muscle hamstrings_l L=1.306 V=0.000 F=0.137
muscle bifemsh_l L=0.891 V=0.000 F=0.009
muscle glut_max_l L=1.055 V=0.000 F=0.016
muscle iliopsoas_l L=0.547 V=0.000 F=0.002
muscle rect_fem_l L=0.620 V=0.000 F=0.005
muscle vasti_l L=1.106 V=0.000 F=0.028
muscle gastroc_l L=1.145 V=0.000 F=0.037
muscle soleus_l L=1.342 V=-0.000 F=0.171
muscle tib_ant_l L=0.606 V=0.000 F=0.005
```

```python
type(model): <class 'sconepy.Model'>
model: <sconepy.Model object at 0x7f71080326f0>
body tibia_r mass=3.708 inertia=[ 0.050400 0.005100 0.051100 ]
body tibia_l mass=3.708 inertia=[ 0.050400 0.005100 0.051100 ]
body torso mass=34.237 inertia=[ 1.474500 0.755500 1.431400 ]
muscle glut_max_r L=1.055 V=0.000 F=0.016
muscle gastroc_r L=1.145 V=0.000 F=0.037
muscle glut_max_l L=1.055 V=0.000 F=0.016
muscle gastroc_l L=1.145 V=0.000 F=0.037

```

---
# model setup:
input: `array`
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
- `actuators`
- `bodies`
- [[muscle]]
	- muscles
	- activation
	- excitation
	- fiber
		- length
		- velocity
	- force
- dof
	- position
	- velocity
	- dofs
- gravity
- joints
- legs
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