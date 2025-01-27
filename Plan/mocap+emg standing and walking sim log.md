---
bg: "[[NTKLab_white bg.png]]"
---

<style>
    .reveal {
        font-family: 'Times New Roman', '標楷體';
        font-size: 30px;
        text-align: left;
        color: black;
        background-size: cover;
        background-position: center;
    }
	.reveal h1,
	.reveal h2,
	.reveal h3,
	.reveal h4,
	.reveal h5,
	.reveal h6 {
	  font-family: 'Times New Roman', '標楷體';
	  color: black;
	  %%text-transform: lowercase%%;
	  text-transform: capitalize;
	}
	.with-border{
		border: 1px solid red;
	}
</style>
<grid drag="60 10" drop="-3 40">
Develop log: From real world to simulation, Neuromusculoskeletal Modeling and Subject Specific Data Generation
<!-- element style="font-size: 35px;align: left; text-align: left;color: white"-->
</grid>

<grid drag="50 10" drop="40 70">
賴宏達、劉智翔
<!-- element style="font-size: 40px;align: right; text-align: right"-->
</grid>

<!-- slide bg="../NTKLab_white bg_cover_resize.png"-->

---
[[musculoskeletal modeling in simulation]]

# Overview
7 Days ~ 10/3 (Thursday)
1. make model fit an object
	1. mocap data input: 
		1. [x] API automatically do: ***eddlai***
			1. [x] `.trc` -> opensism IK 
			2. [x] opensism IK -> `.mot`
			3. [x] `.mot`-> `_q.sto`
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
				3. [x] 檢查各個鏡頭
			2. [x] (quantize the [[level of fatigue from EMG]]? ***sean, eddlai***)
		2. Transform the Real EMG to muscle activation
			1. [x] mocap [[overview of opensim]] [SO](https://opensimconfluence.atlassian.net/wiki/spaces/OpenSim/pages/53085189/Working+with+Static+Optimization), [CMC](https://opensimconfluence.atlassian.net/wiki/spaces/OpenSim/pages/53088683/Example+-+Computed+Muscle+Control ) -> muscle activation ***eddlai***
			3. [x] meaning of muscle activation in [[overview of opensim]] and scone [CEINMS](https://pubmed.ncbi.nlm.nih.gov/26522621/) [[CEINMS - a toolbox to investigate the influence of differentneural control solutions on the prediction of muscle excitationand joint moments during dynamic motor tasks Note]] ***eddlai, sean***, 
				1. [x] 使用者角度***sean***
				2. [x] 把API串接起來
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
# Develop log

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
## Deadline: 12/17 (二)
1. 利用新的EMG概念重新理解SCONE生成的結果，以及收到的資料(資料分析中)
	1. 初步的分析方法實施(需要從數學到coding)
	2. 建立EMG手部資料之實驗建置以活用`libemg`工具(1~2天)，[Feature Extraction — libemg 1.0.0 documentation](https://libemg.github.io/libemg/documentation/features/features.html)
2. 用線上資料庫測試fatigue方案，回報LibEMG的使用結果
3. 重新按照這個文獻[[Robust_Real-Time_Musculoskeletal_Modeling_Driven_by_Electromyograms.pdf]], https://youtu.be/W168hIQggFs?si=Bp_D66jkOJBNaAu2 的做法做一次，至少會完成inversed-problem的整合
	- Calibration procedure
		- 確認每個步驟
	- BSpline coefficients
	- EMG-data driven
	- 確認Kalman filter to process IK-generated joint angles
>	parameters: [Kalman smoothing improves the estimation of joint kinematics and kinetics in marker-based human gait analysis - ScienceDirect](https://www.sciencedirect.com/science/article/pii/S0021929008004685)

4. 想辦法結合Muscle Fatigue Analysis Using OpenSim

待討論：
- ==沒有進ID就沒有關節力量，也沒有肌肉(還是可以直接從IK進CMC?)，那怎麼做CEINMS的calibration沒有對應的生成阿?==
- 我其實很不確定要不要換成用EMD來做，可以跟YY討論 [[Comparison between EMD and Transforms]]
- [[musculoskeletal modeling in simulation]]
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
- [ ] 用EMD分析EMG的spectrum
- [ ] CUSUM, AGLR需要分析每個肌肉的資料，並比較與文獻的差異MSE
- [x] 熟悉EMD[EMD Tutorials — emd 0.6.2 documentation](https://emd.readthedocs.io/en/stable/emd_tutorials/index.html)+[The Hilbert-Huang Transform — emd 0.6.2 documentation](https://emd.readthedocs.io/en/stable/emd_tutorials/02_spectrum_analysis/emd_tutorial_02_spectrum_01_hilberthuang.html) -> MEMD -> CEEMDAN, 
- [ ] COM穩定度，MSE？？，一些簡單的統計工具就夠了吧， https://chatgpt.com/g/g-L2HknCZTC-scholar-ai/c/675512a8-533c-8013-8fbb-c547cc75485c

---
## Deadline: 12/24 (二)
確認
- BSpline
- EMG-driven的model

看了一系列文獻，也算是review了目前的整個EMG的方案

- [x] informed vs driven
為什麼文獻不用CEINMS工具，因為2012，那應該要有driven model在裡頭

現有模型怎麼去延展資料??SCONE的原理是?改用depRL，需要顯卡
- 多筆資料的Data要怎麼剪接
- `RajagopalLaiUhlrich2023.osim`

momentarm，裡頭有
subject_description需要有`<dofSet>`的設定

風險操作
- 發現opensim端，可以不用設定XML，會直接越過，還沒有找到官方文檔在講這個(原來是包含在C中)，用自己寫的python XML庫可操作性比較大(可以在GUI中複現)
```python
# scale_tool = osim.ScaleTool(base_path + path_to_scaling_setup_file)
scale_tool = osim.ScaleTool()
scale_tool.getGenericModelMaker().setModelFileName(base_path + model_file_path)
# scale_tool.getGenericModelMaker().setMarkerSetFileName()
scale_tool.getModelScaler().setMarkerFileName(base_path + marker_file)
scale_tool.getMarkerPlacer().processModel()
scale_tool.run()
```

- update XML 要改成 create
- scaling XML中的data的marker .trc要用相對路徑，

---
## Deadline: 12/31 (二)
本週成果：建立了整套的opensim API到CEINMS API的xml生成的建構流程
[Exoskeleton - Miro](https://miro.com/app/board/uXjVN8HYlg0=/)
流程圖...
有python API跟C++ API
官方建議從C++學python的, [API: API Guide](https://simtk.org/api_docs/opensim/api_docs/md_doc_APIGuide.html)
有選擇要用變數的資料傳遞，還是XML的，選擇用XML的進行
1. 先跑data_1009_EMG_steady_to_sto_for_CEINMS_calib.py
2. 再跑opensim_scaling_IK_MA.py
3. 再跑CEINMScalibration_file_gen_from_osim.py

>先在沒有GRF的情況下跑了ID

- 顯卡越高階越好，在看depRL
- CEINMS吃CPU
- RAM因為多人同時共用64GB會比較保險，上週有兩次閃退
- 吃了12GB左右

calibration沒辦法收斂

---
## Deadline: 1/7 (二)
目標：解決calibration沒辦法收斂的問題

1. calibration要用hybrid嗎
calibration不知道怎麼加入hybrid，XSD就已經限制不行
>NMSmodel: a collection of options for the simulation of the model (see the corresponding section NMSmodel in the execution description file)
2. 如何調參
3. calibration不夠好會怎麼樣
4. ExternalForce是個隱患

---

![[calibration debug.png|800]]

---
![[CEINMS workflow.png|800]]

---
測試過比較簡單的model，只有矢狀面，需要把我們的資料轉向
![[sagital_plane.png|200]]
結果1/4(六)
1. 有些參數比較接近了
2. 成功得到path_01的calibrated 4/11個
3. 開始執行execution
Execution問題
發現CEINMS window才可以跑
- [ ] github上版本不是最新的，試試看develop(建置太久了)
- [ ] 編譯環境有問題(等回覆)
- [x] 可以用wine(結果成功了)
- [ ] 研究CEINMS-RT

---
已經向作者們提問
- SCONE 現在模型相容，控制器方法、Hyfydy可以轉回來嗎
- [[overiew of depRL]] SCONE_gym mimic measure
- CEINMS 最新的code

---
下一步

驗證execution跟實際`path_02~path_24`的差距
著手研究要怎麼把execution所產生的放入forward_method(放到物理引擎裡頭)
- depRL
- SCONE
- opensim forward dynamics
- Genesis
- [NVIDIA/Cosmos: Cosmos is a world model development platform that consists of world foundation models, tokenizers and video processing pipeline to accelerate the development of Physical AI at Robotics & AV labs. Cosmos is purpose built for physical AI. The Cosmos repository will enable end users to run the Cosmos models, run inference scripts and generate videos.](https://github.com/NVIDIA/Cosmos)

---
forward methods
- [[Voluntary control of wearable robotic exoskeletons by patients with paresis via neuromechanical modeling.pdf]]
- [[碩論神經肌肉骨骼模型ntu-111-2 (2).pdf]]
- [[CEINMS-RT an open-source framework for the continuous neuro-mechanical model-based control of wearable robots.pdf]]
- [CEINMS-RT: an open-source framework for the continuous neuro-mechanical model-based control of wearable robots - TechRxiv](https://www.techrxiv.org/users/688663/articles/1250672-ceinms-rt-an-open-source-framework-for-the-continuous-neuro-mechanical-model-based-control-of-wearable-robots)
- [【20250102】Jan Peters团队新作：基于生成对抗模仿学习的人类肌骨模型拟人步行控制策略](https://mp.weixin.qq.com/s/rWBT5-Q5iPIvffBS9d3DQA)

---
Exoskeleton控制演算法
- [【20250103】AI驱动的通用下肢外骨骼机器人系统以实现社区步行辅助](https://mp.weixin.qq.com/s/jESleOjQCSeNW4seNOFjPQ)
- [[Development of a Real-Time Neural Controller using an EMG.pdf]]
- [[Soft robotic apparel to avert freezing of gait .pdf]]
- [[Comparison of Empirical and Reinforcement Learning (RL)-Based Control Based on Proximal Policy Optimization (PPO) for Walking Assistance Does AI Always Win.pdf]]

SCONE可以吃滿CPU
SCONE原理：
- [[A Muscle-Reflex Model that Encodes Principles of Note]]
- [[Predicting gait adaptations due to ankle plantarflexor muscle weakness and .pdf]]

DepRL
- [[DEP-RL EMBODIED EXPLORATION FOR REINFORCEMENT LEARNING IN OVERACTUATED AND MUSCULOSKELETAL SYSTEMS.pdf]]
- [[Natural and Robust Walking using Reinforcement Learning without Demonstrations in High-Dimensional Musculoskeletal Models.pdf]]

---
高中生教學內容

教案以及聯絡的內容
Aaron Wang, aaronwang0809@gmail.com

---
與耀哥討論之總結

確定緯宇用的規格是錯的，需要兩個MOSI沒錯，轉板轉成TTL
缺設備，需要
- LA：耀哥建議要有，側錄，解決方案：上下SPI互連
- adapter：可以先用ADS採集卡確認
- RHS晶片:可以先用ADS採集卡確認，或者用CMOS mode，如果距離夠的話，用現有的嗎(線的問題)
- 可以用假鼠做輸入，還有小的波形產生器，這樣就不會過飽和的問題


---
## Deadline: 1/20 (二)
%% 起手的規劃 %%
下下一步?外骨骼還需要用D4PG嗎，也許應該導入DepRL多制動器myocontrol的概念
- 等Sean 把API的流程以及原理，繼續搞 SCONE，一起把API寫出來(GUI似乎夠用)
- 同時做文獻survey

---
- 用RL讓肌肉骨骼模型自己學會走路：[[DEP-RL EMBODIED EXPLORATION FOR REINFORCEMENT LEARNING IN OVERACTUATED AND MUSCULOSKELETAL SYSTEMS.pdf]]
- SCONE團隊使用SCONE的方法：[[Predicting gait adaptations due to ankle plantarflexor muscle weakness and .pdf]]

RL如何使用先驗資料?
- transfemoral amputee model的差異分析：[[Deep_Reinforcement_Learning_for_Physics-Based_Musculoskeletal_Simulations_of_Healthy_Subjects_and Note]]
>- evolutionary algorithm CMA-ES
>- fitness and genes
>- shallowNN
>- Kidzinski

---
### RL的角色是?SCONE的角色又是?要怎麼選擇
- RL是用來強化model在虛擬環境中對於新增事件的資料衍生(Data Generation)能力
- SCONE則是基於evolutionary algorithm CMA-ES的方法
兩者本質上還是迭代優化方法
> Based on 擁有simulation model之後可以得到上帝視角的資料進行仿生模型agent的訓練

---
### 路線選擇：考慮開發成本
等於要訓練出一個小腦，但不一定要用NN做
- SCONE也是，but how?用depRL
- 直接用OsimRL，自己寫一套imitation learning(unSupervised)

成本
- SCONE
	- HyFyDy長期軟體開支
	- 需要把opensim model遷移進去SCONE
- OsimRL
	- 需要自己開發[[imitation learning]]或者其它RL架構
	- OsimRL有支援的架構?(無)[Deep Reinforcement Learning Workshop](https://neurips.cc/virtual/2022/workshop/49989)，一樣需要大量開發
		- [NeurIPS 2022 Tutorials](https://neurips.cc/virtual/2022/events/tutorial)
		- [AIcrowd | NeurIPS 2019: Learn to Move - Walk Around | Submissions](https://www.aicrowd.com/challenges/neurips-2019-learn-to-move-walk-around/submissions?page=1&q%5Bs%5D=score_display+asc)
		- [Reinforcement learning with musculoskeletal models](https://osim-rl.kidzinski.com/docs/models/interface/)
		- [How Forward Dynamics Works - OpenSim Documentation - OpenSim](https://opensimconfluence.atlassian.net/wiki/spaces/OpenSim/pages/53089643/How+Forward+Dynamics+Works)

---
結論：
1. (單獨訓練出一SCONE這個可解釋架構)
2. 用RL policy(同DepRL架構)串接低階控制器
>猜測可能需要DL的資料衍生能力
3. 要從Offline走到Online跟外骨骼做互動

---
任務：
- [x] SCONE H0918 導入CEINMS activation(SCONE API，暫時不用鑽研，GUI得到的參數可以直接用)
- [x] 驗證SCONE產生的資料 透過opensim Creator 驗證CEINMS(失敗)
	- [ ] on/off時間對上
	- [ ] activation vs CEINMS adjusted activation
	- [x] 切步態疊合，單純看資料，用速度抓之後再透過座標切(大致完成，剩下Debug)
- [ ] DepRL, SCONE gym搞懂怎麼做offline learning
- [ ] 外骨骼模型怎麼導入SCONE
- [x] 研究高中生的自學能力，Line上面聊天，學好東西後由我想怎麼接軌我們目前的開發進度

結論：
SCONE已經可以根據我們的EMG以及Mocap資料訓練出對應的模型
將使用CEINMS所產生的資料作為Opensim(inverse)與SCONE(forward)之間的串接媒介，**我們已經建立來自人體逆向工程的虛擬小腦**


---
### Strike slicing
腳尖離地，腳跟落地的範圍
各段步態之間的標準差，平均

$$gait_n\%=\frac{time-time_{start}}{time_{last} - time_{start}}\times100$$

$$gait\_mean\ at\ x\%= \sum^N_{n=1}\frac{gait\ at\ x\%}{n}$$

待討論
==直接開code==
- [ ] 最後的一組時間不準的問題，需要抓那麼準嗎?
- [ ] hip資料為什麼相反，如果是延遲就合理
- [ ] 其實應該在切strike的部分加上時間資訊

---
[[dataset standard tree]]
![[pelvis_ty_vs_pelvis_ty_overlaid.png]]
![[pelvis_tilt_vs_pelvis_tilt_overlaid.png]]

---
![[hip_flexion_r_vs_hip_r_overlaid.png]]
![[hip_flexion_l_vs_hip_l_overlaid.png]]

---
![[knee_angle_r_vs_knee_r_overlaid.png]]
![[knee_angle_l_vs_knee_l_overlaid.png]]

---
![[ankle_angle_r_vs_ankle_r_overlaid.png]]
![[ankle_angle_l_vs_ankle_l_overlaid.png]]

---
swing+stance