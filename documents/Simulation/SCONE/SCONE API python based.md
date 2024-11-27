- 可以用來控制外骨骼的力量？有Controller就可以吧，需要研究外骨骼物件，我需要command 跟 python作用在同個空間才行。

SCONEpy path
- windwos: `C:\Program Files\SCONE\bin\sconepy.cp39-win_amd64.pyd`
- ubuntu

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
### API characteristic
SCONE py
- Data format
	- biomechanical sensors and actuators via NumPy arrays
	- **neural delays** to sensors and actuators ?
	- **reward shaping** is possible
- `.sto`儲存權重，為什麼不像GUI版本儲存`.par`？
- `.scone`中定義`.osim`

---
### ENV setup
真的要用python3.9才行
```bash
(exo) eddlai@eddlai-ROG-Flow-X13-GV301RE-GV301RE:~/SCONE/SconePy$ /home/eddlai/miniconda3/envs/exo/bin/python /home/eddlai/SCONE/SconePy/sconetools.py                                                                                                  
sconepy found at /opt/scone/lib                                                                                             
19:10:20 Successfully initialized OpenSim3 version 3.3-2021-01-28                                                           
19:10:20 Loaded settings from /home/eddlai/.config/SCONE/scone-settings.zml 
```

### 寫入問題
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