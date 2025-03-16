是用來做RL的SCONE API，SCONE本身有一些已有的模擬參數可使用

# Env setup
SCONEpy path
- windwos: `C:\Program Files\SCONE\bin\sconepy.cp39-win_amd64.pyd`
- ubuntu

真的要用python3.9才行
```bash
(exo) eddlai@eddlai-ROG-Flow-X13-GV301RE-GV301RE:~/SCONE/SconePy$ /home/eddlai/miniconda3/envs/exo/bin/python /home/eddlai/SCONE/SconePy/sconetools.py                                                                                                  
sconepy found at /opt/scone/lib                                                                                             
19:10:20 Successfully initialized OpenSim3 version 3.3-2021-01-28                                                           
19:10:20 Loaded settings from /home/eddlai/.config/SCONE/scone-settings.zml 
```

---
SCONE_Data:
- `.scone`
	- H0918_hfd.scone
	- H0918_osim3.scone
	- H0918_osim4.scone
- `.osim`
	- H0918M_osim3.osim
	- H0918M_osim4.osim
	- H0918v3.osim
- `.hfd`
	- H0918.hfd
	- H0918v3.hfd
- `.zml`
	- InitStateGait10.zml
	- InitStateJump.zml
	- neural_delays_FEA_v3.zml
	- neural_delays_FEA_v4.zml
## API characteristic
SCONE py
- Data format
	- biomechanical sensors and actuators via NumPy arrays
	- **neural delays** to sensors and actuators ?
	- **reward shaping** is possible
- `.sto`儲存權重，為什麼不像GUI版本儲存`.par`？
- `.scone`中定義`.osim`

---
## Basic workflow
```python
import os
if store_data:
    dirname = 'sconepy_example_' + model.name()
    filename = model.name() + f'_{random_seed}_{model.time():0.3f}_{model.com_pos().y:0.3f}'
    model.write_results(dirname, filename)
    current_directory = os.getcwd()
    print(f'Results written to {current_directory}/{dirname}/{filename}. Please use SCONE Studio to replay the .sto file.', flush=True)
```
沒有出現.sto，不確定model.write_results(dirname, filename)的效果，需要確認該函數
會預設存在`\SCONE\results`中

---
# Simple Example
### [[SCONE API reference]]
### Example
The method of randomizing used in Example
```python
	rng = np.random.default_rng(random_seed)

	# Initialize muscle activations to random values
	muscle_activations = 0.1 + 0.4 * rng.random((len(model.muscles())))
	# 產生一個陣列，為每條肌肉設置隨機化
```
### [[How to wrap SCONE C src to python]]

---
### UNKNOWN
如何`.par`，`write_results`會跳過

---
# SCONEgym
就是已經幫你把SCONEpy串進gym了
ABC庫
```
class Animal(ABC):
    @abstractmethod
    def make_sound(self):
        """每個動物都必須實作這個方法來發出聲音"""
        pass

    def sleep(self):
        """非抽象方法，可選擇性覆蓋"""
        print("Sleeping...")
```
## `__init__`
- Progress
	- `self.episode`：當前的 episode 編號。
	- `self.total_reward`：當前 episode 的累計獎勵。
	- `self.total_steps / self.steps`：模擬的總步數和當前 episode 的步數。
	- `self.has_reset`：是否已經重置過環境。
	- `self.init_dof_pos_std` / `self.init_dof_vel_std`：關節初始位置和速度的標準差。
	- `self.init_load`
	- `self.store_next`
- environment
	- `self.obs_type`：觀察空間類型。
	- `self.left_leg_idxs` / `self.right_leg_idxs`：左腿和右腿的關節索引。
- scone related
	- set_log_level(3)
	- load_mode
	- dof_position_array()
	- dof_velocity_array()


==SCONErelated==
## `__step__`
- action(原本是透過muscle_force_array, muscle_fiber_length_array(), muscle_fiber_velocity_array())
	- clip_action
	- ==use_delayed_actuators==
		- model.set_delayed_actuator_inputs(action)
		- model.set_actuator_inputs(action)
	- model.advance_simulation_to(self.time + self.step_size)
- status
	- reset

```
reward = self._get_rew()
obs = self._get_obs()
done = self._get_done()
reward = self._apply_termination_cost(reward, done)
```

store_next
## `__reset__`
- 自動set_store_data
- ==set_dof_positions==
- ==set_dof_velocities==
- ==muscle_excitation_array()==
- ==init_activations_std==
- ==adjust_state_for_load==

## 特殊
- `model_velocity`
- `_find_head_body`
- `_switch_legs`
- `_apply_termination_cost`

---
# GaitGym
實例化`SCONEgym class`
- `_get_obs(self)`整合SCONE API取得之前的model
	- `_get_feet_relative_position()`
>特殊
>- 不考慮x,y
>- 有分成2D or 3D

作者未來可能會把measure都寫成python的版本
可以引入SCONE本身的`measure.scone`
```python
class GaitGymMeasureH0918(GaitGym):
    """
    Shows how to use custom measures from the .scone files in
    python.
    """

    def __init__(self, *args, **kwargs):
        self.delay = False
        super().__init__(find_model_file("H0918_hfd_measure.scone"), *args, **kwargs)

    def custom_reward(self):
        self.rwd_dict = self.create_rwd_dict()
        return self.model.current_measure()

```


---
# Next
[[overiew of depRL]]，用於提供action，透過policy轉換activation 到actuator
```python
action = policy(state)
state, reward, done, info = env.step(action)
# in the step
self.model.set_actuator_inputs(action)
```

```python
for t in np.arange(0, max_time, 0.01):
		# Set actuator_inputs based on muscle force, length and velocity
		mus_in = model.muscle_force_array()
		mus_in += model.muscle_fiber_length_array() - 1
		mus_in += 0.2 * model.muscle_fiber_velocity_array()
		model.set_actuator_inputs(mus_in)
 
		# Advance the simulation to time t
		# Internally, this performs as many simulations steps as required
		# The internal step size is variable, and determined by the 'accuracy'
		# setting in the .scone file
		model.advance_simulation_to(t)
 
		# Abort the simulation if the model center of mass falls below 0.3 meter
		com_y = model.com_pos().y
		if com_y < min_com_height:
			print(f'Aborting simulation at t={model.time():.3f} com_y={com_y:.4f}')
			break
```