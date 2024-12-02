tools: [[SCONE]]用來RL training, [[overview of opensim]]用來進行IK推測, [[CEINMS app.]]

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
			2. [ ] (quantize the [[level of fatigue from EMG]]? ***sean, eddlai***)
		2. Transform the Real EMG to muscle activation
			1. [x] mocap [[overview of opensim]] [SO](https://opensimconfluence.atlassian.net/wiki/spaces/OpenSim/pages/53085189/Working+with+Static+Optimization), [CMC](https://opensimconfluence.atlassian.net/wiki/spaces/OpenSim/pages/53088683/Example+-+Computed+Muscle+Control ) -> muscle activation ***eddlai***
			3. [x] meaning of muscle activation in [[overview of opensim]] and scone [CEINMS](https://pubmed.ncbi.nlm.nih.gov/26522621/) [[CEINMS - a toolbox to investigate the influence of differentneural control solutions on the prediction of muscle excitationand joint moments during dynamic motor tasks Note]] ***eddlai, sean***, 
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

##### 資料同步
- [x] 用光學對齊檢查，應該要差不多綠光開始走動??
	- [x] EMG event_marker開始，跟video紅燈frame對齊
	- [x] (gait_analysis)沒時間->時間點附近最靠近的heel，(水平校正trc, x, y ,z成有意義的資料)看analysis，但丟進去opensim可能不需要
	- [x] 透過肌肉，heel座標關係去對齊(可以double check)
- [x] 下次收案一起把Cygnus TTL完成, `sync_marker.npz`（等測試）

##### 修改
- 統一改用opensim 4.1，需要嫁接Callibrated Emg Informed NMS
- 要多一個maximally contracted isometrically (no motion occurring)

---
### 收斂目標
1. opensim把肌肉資料***轉換為模擬***資料
2. SCONE***生成***更多模擬資料

方法:
- Inversed: 計算出模擬->EMG-informed 校正
- Forward: 需要Objective Function(有三種方法，應該都去試試看)
<div style="background-color: white; padding: 10px;">
  <img src="D:\Notes\Exoskeleton-Control-Note\documents\Simulation\opensim\opensim_Forward Problem.png" alt="ID Tool" width="500"/></div>

但都需要得到excitation資料，所以什麼是excitation
應該是先用資料校正模型，再透過校正後的模型去生成

### 問題
SCONE, shooting methods跟RL的差別?
什麼是[[數值優化]]?

[Simulating ideal assistive devices to reduce the metabolic cost of walking with heavy loads | PLOS ONE](https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0180320)
[Simulating Ideal Assistive Devices to Reduce the Metabolic Cost of Running | PLOS ONE](https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0163417)

apply torques between two bodies: TorqueActuator
apply generalized forces and torques to a specific coordinate: CoordinateActuators

cupy

有對肌肉模型進行縮放嗎，參考以及使用的方法是?

- [ ] 確認mocap端的opensim scaling 流程
- [ ] 需要確認joint/coordinate definitions match

[[GCBME呈現]]

![[pipeline of building Digital Twins.png]]

---
## Deadline: 11/12 (二)
Sean
1. CENIMS到底校正了什麼，關節與
	1. 關節力臂
	2. 肌肉長度變化
	3. ==關節力矩(ID)==
	4. EMG
	5. 疑問:
		- [x] 應該要選擇的model做校正?雖然沒有身高，但有丟肌肉長度
1. CENIMS應該要跟CMC相似，跟Trajectory做校正
2. [x] Scaling
3. SCONE嘗試調整各種權重
4. [x] 改Model 4不能用在SCONE中，

eddlai
4. Find Heel挖Maurice code
5. Opensim API(窒礙難行)
6. SCONE API
7. CEINMS API

跟YY確認
1. MVC
2. Faitgue
3. ID需要反作用力 30Hz以上
4. SCONE改權重

- [ ] 為什麼左腳先，但是右腳先有速度?
- [ ] 為什麼AnYu那幾筆資料的軌跡很奇怪
整個左標系統是反的
![[AnYu data path2 right first.png]]
![[AnYu data path4 left first.png]]
![[Sean data path1 left first.png]]

---
## Deadline: 11/26 (二)
- sean
	1. 釐清CENIMS功能，sean, eddlai，CENIMS應該要跟CMC相似，跟Trajectory做校正
	2. 等長等張，不用負重
	3. K fold
	4. faitgue偵測與量化文獻
- eddlai
	- 檢查為什麼CENIMS會讀不到對的資料 `/lib/FileIO/EMGDataFromFile.cpp`
		1. `emg.mot`
		2. `path1_01_EMG_cut.sto`
		3. visual studio編譯
		4. 量化比較步態擬合
		5. 用速度去大致定位，回到座標去抓起來的確切時間否則會是錯的
- 等maurice一起開會
	1. 問牧華可不可以兩個人選一個
	2. 要開始收病患，建立流程，等跟maurice他們開會
	3. 為什麼要除三，目的是，對抓起點沒有幫助阿

---
調整資料工程的工作不能全丟給sean，一定要有其他人
可以試試看大家一起專攻一個方向，但他一定比我早嘗試
## Deadline: 12/03 (二)
- together
	- 搞懂SCONE的本質，建立資料常模？方可資料生成（還沒看）
		- dep-RL
		- opensim-RL
	- opensim_CMC, CEINMS怎麼資料結合: 釐清CENIMS功能，CENIMS應該要跟CMC相似，跟Trajectory做校正
	- 討論faitgue偵測與量化文獻
- sean
	- 用網路資料驗證流程
	- MVC要等長等張，不用負重，至少一篇文獻
- eddlai
	- 檢查為什麼CENIMS會讀不到對的資料 `/lib/FileIO/EMGDataFromFile.cpp`
		1. `emg.mot`
		2. `path1_01_EMG_cut.sto`
		3. visual studio編譯
	- 量化比較步態擬合
- 等maurice一起開會（繼續等）

投影片中
- [ ] 速度不夠，推測的路徑
- [ ] 線上資料庫的量化資料（有需要），比較我們的資料是否正確（標準是？）振幅；頻譜
- [ ] 線上資料庫驗證流程失敗的原因
- CENIMS等我看完User Guide，再開始編譯
- 

[[Review of electromyography onset detection methods for real-time control of robotic exoskeletons.pdf]]

待辦問題：
- [ ] time_difference問題有待商榷，trc都從0.33..開始
- [ ] [[CEINMS User Guide 0.9.pdf]]
- [ ] [[Statistical Methods for Defining and Analyzing Declining Trends]]
- [ ] 系統需要能夠理解代償，或者要想辦法fit回去原始的步態，用各種方法
	- 關節角度
	- 振幅
	- 頻率
- [ ] 寫跑0~24，下降趨勢？，寫code去確認這件事情 交給sean
- [ ] path1_09

1. 不夠會用工具
2. 量化差異再開始解

理解了這些文獻，正在實踐這些方法（ 花了點時間），之後才會用來去量化生成資料差異
之後盡量做同一件事情