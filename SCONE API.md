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
iterate `model.`
- bodies
- muscles()
- dofs()
- actuators()