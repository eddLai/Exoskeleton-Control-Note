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
			2. [ ] quantize the [[level of fatique from EMG]]? ***sean, eddlai***
		2. Transform the Real EMG to muscle activation
			1. [x] mocap [[opensim]] [SO](https://opensimconfluence.atlassian.net/wiki/spaces/OpenSim/pages/53085189/Working+with+Static+Optimization), [CMC](https://opensimconfluence.atlassian.net/wiki/spaces/OpenSim/pages/53088683/Example+-+Computed+Muscle+Control ) -> muscle activation ***eddlai***
			3. [x] meaning of muscle activation in [[opensim]] and scone [CEINMS](https://pubmed.ncbi.nlm.nih.gov/26522621/) [[CEINMS - a toolbox to investigate the influence of differentneural control solutions on the prediction of muscle excitationand joint moments during dynamic motor tasks Note]] ***eddlai, sean***, 
				1. [x] read the papers
		3. [ ] into Scone controller parameters like tension and length, possible? ***sean***
2. ==Validation by collect a new data==




[[Python and C integration]]


opensim下載：
https://github.com/sk413025/sci-competition/issues/59
libgconf-2-4下載, https://blog.csdn.net/lingzhou0909/article/details/139708197


Full body, 11初過後再說

opensim裡頭都有各種組合的code不知道為什麼

130紅燈亮，131紅燈暗，140綠燈亮, 141綠燈暗
02 右腳
其他 左腳起步

detrend?

![[RAW EMG data.png]]