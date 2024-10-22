tools: [[SCONE]]用來RL training, [[opensim]]用來進行IK推測

7 Days ~ 10/3 (Thursday)
1. make model fit an object
	1. mocap data input: 
		1. [ ] API automatically do: ***eddlai***
			1. [ ] `.trc` -> opensism IK 
			2. [ ] opensism IK -> `.mot`
			3. [ ] `.mot`-> `_q.sto`
			4. [ ] optimizing: mimic measure
			5. [ ] optimizing -> trained weights
			6. [ ] go back to 1. with trained weights
		2. [ ] Long Head Biceps femoris muscle model ***sean***
		3. [x] (Full body muscle skeleton model (opensim creator) ***sean***)
		4. [x] (points lost issue, interpolation? ***sean***) (暫時已經使用mocap team的優化)
	2. EMG data input
		1. [x] difference between our EMG data and Gold standard: 安於data, standard: sean 檢查前幾筆，已經同步，對照[Full body mobile brain-body imaging data during unconstrained locomotion on stairs, ramps, and level ground](https://www.nature.com/articles/sdata2018133)這篇的內容
			1. [x] sync, 沒辦法用16Hz去處理吧？因為相機的殘留
				1. [x] 因為會有人移動，所以不能開啟鏡頭移動的code
				2. [x] 需要手動校準燈泡位址
				3. [ ] 檢查各個鏡頭
			2. [ ] (quantize the [[level of fatique from EMG]]? ***sean, eddlai***)
		2. Transform the Real EMG to muscle activation
			1. [x] mocap [[opensim]] [SO](https://opensimconfluence.atlassian.net/wiki/spaces/OpenSim/pages/53085189/Working+with+Static+Optimization), [CMC](https://opensimconfluence.atlassian.net/wiki/spaces/OpenSim/pages/53088683/Example+-+Computed+Muscle+Control ) -> muscle activation ***eddlai***
			3. [x] meaning of muscle activation in [[opensim]] and scone [CEINMS](https://pubmed.ncbi.nlm.nih.gov/26522621/) [[CEINMS - a toolbox to investigate the influence of differentneural control solutions on the prediction of muscle excitationand joint moments during dynamic motor tasks Note]] ***eddlai, sean***, 
				1. [ ] 使用者角度***sean***
				2. [ ] 把API串接起來
				3. [x] read the papers
		3. [ ] into Scone controller parameters like tension and length, possible? ***sean***
2. ==Validation by collect a new data==


[[Python and C integration]]
opensim下載：
https://github.com/sk413025/sci-competition/issues/59
libgconf-2-4下載, https://blog.csdn.net/lingzhou0909/article/details/139708197


opensim裡頭都有各種組合的code不知道為什麼

---
### 實驗數據採集:與maurice and 安妤進行討論
130紅燈亮，131紅燈暗，140綠燈亮, 141綠燈暗
02 右腳
其他 左腳起步
detrend?
下次收案一起把Cygnus TTL完成
EMG貼片要加GND，左右腳的問題已經校正

資料同步
- [x] 用光學對齊檢查，應該要差不多綠光開始走動??
	- [x] EMG event_marker開始，跟video紅燈frame對齊
	- [x] (gait_analysis)沒時間->時間點附近最靠近的heel，(水平校正trc, x, y ,z成有意義的資料)看analysis，但丟進去opensim可能不需要
	- [x] 透過肌肉，heel座標關係去對齊(可以double check)
- [x] 下次收案一起把Cygnus TTL完成, `sync_marker.npz`（等測試）

統一改用opensim 4.1，需要嫁接Callibrated Emg Informed NMS

---
### 收斂目標
1. opensim把肌肉資料***轉換為模擬***資料
2. SCONE***生成***更多模擬資料

方法:
- Inversed: 計算出模擬->EMG-informed 校正
- Forward: 需要Objective Function
<div style="background-color: white; padding: 10px;">
  <img src="D:\Notes\Exoskeleton-Control-Note\documents\Simulation\opensim\opensim_Forward Problem.png" alt="ID Tool" width="500"/></div>
有三種方法，應該都去試試看

但都需要得到excitation資料，所以什麼是excitation

### 問題
SCONE, shooting methods跟RL的差別?
什麼是[[數值優化]]?

[Simulating ideal assistive devices to reduce the metabolic cost of walking with heavy loads | PLOS ONE](https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0180320)
[Simulating Ideal Assistive Devices to Reduce the Metabolic Cost of Running | PLOS ONE](https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0163417)

apply torques between two bodies: TorqueActuator