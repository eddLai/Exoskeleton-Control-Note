[[SCONE]]

7 Days
1. make model fit an object
	1. difference between our EMG data and Gold standard
		1. quantize the level of fatique from EMG
	2. mocap data input: `.trc` -> opensism IK 
		1. API
		2. Full body muscle skeleton model (考慮用opensim creator))
	3. EMG data input
		- [ ] opensim [SO](https://opensimconfluence.atlassian.net/wiki/spaces/OpenSim/pages/53085189/Working+with+Static+Optimization), [CMC](https://opensimconfluence.atlassian.net/wiki/spaces/OpenSim/pages/53088683/Example+-+Computed+Muscle+Control ) -> muscle activation
		- [ ] into Controller parameters like tension and length
	5. `_q.sto` Scone mimic measure
		1. Training is Scone
		2. Meaning of the muscle .activation in scone
		3. Transform the Real EMG to muscle activation
2. Validation by collect a new data


1. 理解mot資料意含
4. SCONE中activation的單位是甚麼，需不需要轉肌肉參數tension, length之類的
5. 影片長度不夠，不用特別去拼接，把用上一段影片訓練好的參數，丟給要用下一個影片訓練的，要寫出API調用腳本
6. 動作捕捉影片掉點的預處理，問牧華
7. 人體模型建置?(目前看到的沒有同時包含全身肌肉的