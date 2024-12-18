[[musculoskeletal modeling in simulation]]

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

投影片中新增：
- [ ] 線上資料庫的量化資料（有需要），比較我們的資料是否正確（標準是？）振幅；頻譜
- [ ] 線上資料庫驗證流程失敗的原因，速度不夠，推測的路徑
- CENIMS等我看完User Guide，再開始編譯

理解了這些文獻，正在實踐這些方法（ 花了點時間），之後才會用來去量化生成資料差異
之後盡量做同一件事情
- [x] 寫跑0~24，下降趨勢？，寫code去確認這件事情 交給sean
- [x] path1_09

---
## Deadline: 12/10 (二)
量化疲乏之後，再進scone生成的資料
- [x] 解決notebook merge問題
- [x] opensim moco 完全擬合，不能用
- [x] 把中間有休息的寫進簡報的圖裡 sean
- [x] time_difference問題有待商榷，trc都從0.33..開始 sean再次確認
- [x] 線上資料庫的量化資料（有需要），比較我們的資料是否正確（標準是？）振幅；頻譜 sean
- CENIMS等看完User Guide，再開始編譯 eddlai
	- [ ] [[CEINMS User Guide 0.9.pdf]]
- [x] [[Review of electromyography onset detection methods for real-time control of robotic exoskeletons.pdf]] sean, eddlai 找時間一起看
- [x] MSE:可以拿來量化pattern
- [x] 正在深入了解各種entropy的關係
- [ ] 小波分析, hilbert轉換 eddlai
- [x] Muscle Fatigue Analysis Using OpenSim.pdf sean可以先看，eddlai
- [ ] 回到多自由度的模型，加進halpe26手臂的模型，IK部份進opensim sean
- [x] 上肢的controller要survey，找到看過用SCONE的文 eddlai, sean
- [x] 研究一下RMS envelope，不行，因為最後要走到real-time

>以後多注意：
>sean 記得CC給大家
>eddlai 頻譜圖要注意範圍50Hz
>sensor重組的特規骨架，需要問物治的老師怎麼標記回對的人體model(先pass)

>相關資料
>extension://efaidnbmnnnibpcajpcglclefindmkaj/[https://www.biorxiv.org/content/biorxiv/early/2024/09/10/2024.09.06.611594.full.pdf](https://www.biorxiv.org/content/biorxiv/early/2024/09/10/2024.09.06.611594.full.pdf "https://www.biorxiv.org/content/biorxiv/early/2024/09/10/2024.09.06.611594.full.pdf")
>病理的需要CPG [https://pmc.ncbi.nlm.nih.gov/articles/PMC10544733/](https://pmc.ncbi.nlm.nih.gov/articles/PMC10544733/ "https://pmc.ncbi.nlm.nih.gov/articles/pmc10544733/")
未來用MUST來做，避免犧牲EMG高頻資訊

- [ ] 系統需要能夠理解代償，或者要想辦法fit回去原始的步態，用各種方法
	- 關節角度
	- 振幅
	- 頻率

---
1. 利用新的EMG概念重新理解SCONE生成的結果，以及收到的資料(資料分析中)
	1. 初步的分析方法實施(需要從數學到coding)
	2. 建立EMG手部資料之實驗建置以活用`libemg`工具(1~2天)，[Feature Extraction — libemg 1.0.0 documentation](https://libemg.github.io/libemg/documentation/features/features.html)
2. 用線上資料庫測試fatigue方案，回報LibEMG的使用結果
3. 重新按照這個文獻[[Robust_Real-Time_Musculoskeletal_Modeling_Driven_by_Electromyograms.pdf]], https://youtu.be/W168hIQggFs?si=Bp_D66jkOJBNaAu2 的做法做一次，至少會完成inversed-problem的整合
	- Calibration procedure
	- BSpline coefficients
	- 確認Kalman filter to process IK-generated joint angles
>	parameters: [Kalman smoothing improves the estimation of joint kinematics and kinetics in marker-based human gait analysis - ScienceDirect](https://www.sciencedirect.com/science/article/pii/S0021929008004685)

4. 想辦法結合Muscle Fatigue Analysis Using OpenSim

待討論：
- ==沒有進ID就沒有關節力量，也沒有肌肉(還是可以直接從IK進CMC?)，那怎麼做CEINMS的calibration沒有對應的生成阿?==
待辦：
- 找找看fatigue的資料庫

量化疲乏：
- MSE下降趨勢
- STFT時頻中位下降
- ankle flexion來判斷腳底的先後+疲乏分析
	- 腳踝的背屈角度變小
	- Knee會變得平滑，關節角度變小

- [ ] 如何取得SCONE座標，分析每條肌肉
SCONE分析項目
- 步長
- 速度
- 達穩定步態花費時間
- [ ] WT
- [ ] CUSUM, AGLR需要分析每個肌肉的資料，並比較與文獻的差異MSE
- [ ] 熟悉EMD[EMD Tutorials — emd 0.6.2 documentation](https://emd.readthedocs.io/en/stable/emd_tutorials/index.html)+[The Hilbert-Huang Transform — emd 0.6.2 documentation](https://emd.readthedocs.io/en/stable/emd_tutorials/02_spectrum_analysis/emd_tutorial_02_spectrum_01_hilberthuang.html) -> MEMD -> CEEMDAN, 
- [ ] COM穩定度，MSE？？， https://chatgpt.com/g/g-L2HknCZTC-scholar-ai/c/675512a8-533c-8013-8fbb-c547cc75485c


測試是否可以用EMD方案取代
- DTFT: [doi:10.1016/j.cmpb.2006.02.009](https://pdf.sciencedirectassets.com/271322/1-s2.0-S0169260706X02018/1-s2.0-S0169260706000472/main.pdf?X-Amz-Security-Token=IQoJb3JpZ2luX2VjEIv%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLWVhc3QtMSJIMEYCIQC4uoUxqb73BtgrCbHzjF2CWC%2FTXmSkNXNPbP8P%2BYrY9QIhAO7RJwjCGiQn08lt76m0bSBx6yzxkY4jFgEjGksL%2B9KyKrMFCFMQBRoMMDU5MDAzNTQ2ODY1IgwqvkmfXWNfMnBTUMcqkAWQBnNfyss53ubfOC9wHe0G7N%2FhJfgX6%2FQlYXTL4C8Lt9Iqp%2BuZur24G%2Bv20wpLMaRdRUCwK7rQjO45sua5T7PMsK%2FaLOm7DKPLM9yO4YJ8TKUnRpss%2F%2B2sc70WTpdwIoQqR8Ka1HY1BsSzX303Nj8lIUWV0tuMKbVGoc3FUjPQvXLUNHf74Ig5b72zOZSH36nvCYEEMtAl2sEVnc7GOTIP%2B4FQGGdS1WQZHuz%2Fkm7iCWs5dZjQY7rt8UI8fuW%2F8%2FejkJsxH7ypJfxqY%2FmgZaPuTrP0cmMV0AEZEFHsz4WKEq6Ft%2FaPczYd6aTsl0QrVDzxABITMq2kN8p6aMcwAUnaSHbQuNOiFtqozMuX0dbmI0Z%2BYKtxX7e5wAoewpUgGXuna03sBJPu8yBwX859Cvt4AYw%2FaWm1diHuIuCvKVBjy6QeRpXBfl0F57j0n%2BQ5Z03H1IPIulMXBAr2JhDf7LZC0DuyKN%2FXqXu1ghFbWFxIJOkpHAfGXpHtbNvF1cus5Rz2lirbnsIEdiwMib37LPFODA05%2FslogViGqIHDPFH6YHKuei2vj8AosmVfUxbBm6c4BmKUBzlL5dLzi63V0dHBqLDhRZN63PPwOG2ALyOVfTZJ37XTpuau3x%2FlY%2FRKcCxMttnL1iZbyN3XDT98yfIbGRyRTG6xWWWzqVZLVQl6%2BmPqzcYPnA2%2FcWNhDnG0R6OLvyw%2FY2SWMHj3Ybx%2BoPt5hnylBusY5J7Y3DA6a%2FbpUnSYO11l%2BPi4jMgkFOfCJjKnFTZm%2FWyIlL6UZ0X1YFSLwlIbEVjCKE%2BU1yszwqZYxyyIl786wG1aasjjRK%2F29FdfZHRxs9sSLv6S%2BXXq0F7JrRoAn6fHQQ8pE5gQ7iy%2FmjCo3oi7BjqwAfv7uRwYCy2I%2F5FN5veSl07tIJE0WjwctqrviR%2FKOvCds24FfrU6RYLFSv%2F8WH5Imth3PunNqw3WC53E%2FIJcMBd5jYf0UokI64I2aTLgrLUrKyTceTkdJ0N6Bb9btycjjN1dcFs%2FoG9XIXpblgObYTHfVDDEe7TnU50ZplkJfy5C4ILV3yWA1o9Y8bhwHD5XRftS%2FriXTHBDWGODWqEBajc%2F2LNJuxq8cqZndNOD3d1f&X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20241218T021833Z&X-Amz-SignedHeaders=host&X-Amz-Expires=300&X-Amz-Credential=ASIAQ3PHCVTY76D4DQS7%2F20241218%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Signature=49503872418b40d77d429af9ec69ae23aa2f1fa1be448844d5acb9d405d87da9&hash=728c1774fc6339b669fa757ab4ff85364205d897d1b8a1b78cb28b3fb57a815f&host=68042c943591013ac2b2430a89b270f6af2c76d8dfd086a07176afe7c76c2c61&pii=S0169260706000472&tid=spdf-55fe67a5-a0c4-4d64-b31c-a7cac5b6f7b2&sid=f722ed328e000945b1488927e27ed9b16b23gxrqa&type=client&tsoh=d3d3LnNjaWVuY2VkaXJlY3QuY29t&ua=161259035104005e07&rr=8f3ba9b8b95449fb&cc=tw), [EMG Mean Power Frequency Determination Using Wavelet Analysis](https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=757017)
- Filter: [EMG signal filtering based on Empirical Mode Decomposition - ScienceDirect](https://www.sciencedirect.com/science/article/pii/S1746809406000085)
- Wavelet: [Frontiers | Comparison of Empirical Mode Decomposition, Wavelets, and Different Machine Learning Approaches for Patient-Specific Seizure Detection Using Signal-Derived Empirical Dictionary Approach](https://www.frontiersin.org/journals/digital-health/articles/10.3389/fdgth.2021.738996/full)
