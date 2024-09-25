| Date  | Duration length | task                                                     | check |
| ----- | --------------- | -------------------------------------------------------- | ----- |
| 10/2  | 1 week          | [[mocap+emg standing and walking sim]]                   |       |
| 10/11 | 1 week          | 導入Exoskeleton 的model                                     |       |
| 10/20 | 1 week          | D4PG + CMA-ES 整合進 Scone                                  |       |
| 11/2  | 1 weeks         | HMI, 4 indexs to evalution                               |       |
| 11/9  | 1 week          | trasistion                                               |       |
| 11/16 | 1 week          |                                                          |       |
| 12/6  | 3 weeks         |                                                          |       |
| 12/13 | 1 week          | KV260, model par進python, NPU acc., EMG轉muscle activation |       |
| 12/24 | 2 weeks         | week fine-tuning 繼續跑跑步機                                  |       |
| 12/25 | -               | application and EMG filter                               |       |

| Date  | Duration length | task                                                     | check |
| ----- | --------------- | -------------------------------------------------------- | ----- |
| 10/13 | 1 month         | [[mocap+emg standing and walking sim]]                   |       |
| 10/20 | 1 week          | running and climbing                                     |       |
| 11/2  | 2 weeks         | trasistion                                               |       |
| 11/9  | 1 week          | 導入Exoskeleton 的model                                     |       |
| 11/16 | 1 week          | D4PG + CMA-ES 整合進 Scone                                  |       |
| 12/6  | 3 weeks         | HMI, 4 indexs to evalution                               |       |
| 12/13 | 1 week          | KV260, model par進python, NPU acc., EMG轉muscle activation |       |
| 12/24 | 2 weeks         | week fine-tuning 繼續跑跑步機                                  |       |
| 12/25 | -               | application and EMG filter                               |       |

把成果提前到11月前
病理的目標：平衡的很好


7 Days
1. make model fit an object
	1. difference between our EMG data and Gold standard
	2. mocap trc -> opensism IK 
		1. API
		2. Full body muscle skeleton model (考慮用opensim creator)
	3. `_q.sto` Scone mimic measure
		1. Training is Scone
		2. Meaning of the muscle .activation in scone
		3. Transform the Real EMG to muscle activation
2. Validation by collect a new data
