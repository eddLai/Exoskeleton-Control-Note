- 可以用來控制外骨骼的力量？有Controller就可以吧，需要研究外股ㄍㄜ
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
The method of randomizing used in Example
```python
	rng = np.random.default_rng(random_seed)

	# Initialize muscle activations to random values
	muscle_activations = 0.1 + 0.4 * rng.random((len(model.muscles())))
	# 產生一個陣列，為每條肌肉設置隨機化
```
