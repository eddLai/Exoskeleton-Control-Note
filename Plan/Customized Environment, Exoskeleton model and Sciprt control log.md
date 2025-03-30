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
Develop log: Customized Environment(Slope, Tripping obeject, Exoskeleton model and its control) needs better simulation cerebellum
<!-- element style="font-size: 35px;align: left; text-align: left;color: white"-->
</grid>

<grid drag="50 10" drop="40 70">
賴宏達、劉智翔、葉亘祐、曾峻魁、Aaron Wang
<!-- element style="font-size: 30px;align: right; text-align: right"-->
</grid>

<!-- slide bg="../NTKLab_white bg_cover_resize.png"-->

---
## Idea
HyFyDy, DepRL, SCONE gym都有**引入額外的場景物件**，展現其環境適應性
How?
1. 單獨訓練出一SCONE這個可解釋架構
2. ~~shooting method 學習到的結果轉移到 RL 策略~~
>猜測可能需要DL的資料衍生能力
3. 要從Offline走到Online跟外骨骼做互動
4. 用RL policy(同DepRL架構)串接多個低階控制器，訓練更高階的狀態切換控制器
>可擴展性到底多大?到極限的時候就需要，例如
>- 在平面上走、在斜坡上走?
>- 爬樓梯?
>- 參考外骨骼文獻所用的https://mp.weixin.qq.com/s/W0oQqiiPtTN8nXG0pYt5ww

---
shooting methods設計一個低階控制器，再透過RL設計一個高階控制器，從而實現一個類似大腦小腦協同控制subject specific neuromusculoskeletal model的policy嗎

由於現在外骨骼控制器是RL-based，所以==不行==

---
## Implementation steps
5. Control the EXO in simulation
	1. 怎麼導入物件 e.g.[(82) Tripping and Slipping Simulations (short) - YouTube](https://www.youtube.com/watch?v=MudlYgzAxro), [[overview of SCONE]]全部功能
	2. 怎麼導入虛擬模型
	3. 怎麼控制
6. 簡單測試外骨骼資料串接
	1. if assisting or obstacle from current and $\omega$ 
	2. level of fatigue

---
## Import an Object
線索：HyFyDy
- Treadmill直接加在hfd的model檔案中
- `slope.scone`加在script中
反之SCONE，應該加在osim檔案中

如果SCONE中創造物件的接口沒有做出來的話，那就用Gym，怎麼把已經可以走路的模型串接上來?
繼承參數?控制?

---
### Options
- HyFyDy可以
- SCONE: 嘗試用OpenSim Creator跟Lua Script創造外骨骼機器人model
- opensim creator有點麻煩
- 使用Gym，~~移植來自SCONE的`.par`，先想辦法在gym中做物件，我跟sean都調整成這個~~
	- 在OpenAI Gym中創造MoJuCo機器人模型與OpenSim人體模型的互動環境
	- MuJuCo中做人體模擬 [MyoHub/myoconverter: A tool to convert opensim 4.0+ MSK models into MuJoCo format with optimized muscle kinematics and kinetics](https://github.com/MyoHub/myoconverter?tab=readme-ov-file)，有限制 [Natural Walking RL](https://sites.google.com/view/naturalwalkingrl)
	- HyFyDy+RL: DepRL
- 直接用Opensim與python做對接: OsimRL
	- [Policy Design for an Ankle-Foot Orthosis Using Simulated Physical Human–Robot Interaction via Deep Reinforcement Learning](https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=9849514)
- 直接用Opensim與Simulink做對接
	- [A Simple OpenSim-Simulink Interface for Cascaded Zero-Force Control of Human-Robot Interaction in a Hip Exoskeleton Robot](https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=10025309)

---
### Our Decision
選了SCONE，又選了SCONEgym
在HyFyDy中創造物件非常簡單
- .osim中的(過於麻煩)
	- opensim文件中的model檔案描述呢，有提到其它物件嗎
	- 看之前加威留下的資料夾
- lua model，建立簡單的物件可能可以，但是如果要具有制動器的機器人也許就不行了
- 使用Gym，再使用SCONEgym，移植來自SCONE的`.par`，先想辦法在gym中做物件，我跟sean都調整成這個

[[Overview of OpenAI gym]]

---
## Workflow
7. SCONE API
8. SCONEgym with hyfydy
	1. Gym怎麼跟scone-py結合
	2. [[Overview of Hyfydy]]: Mujoco, render
9. DepRL導入資料，把所有mimic都用上

---
疑問：
- 需要用opensim做外骨骼模型?
%% - 為什麼SCONEpy只需要用加的?
	- **初始化執行器輸入值**：
		- 使用肌肉的當前力量（`muscle_force_array`）作為初始值。
	- **調整執行器輸入值**：
		- 加入纖維長度的偏移（相對於基準長度）。
		- 加入纖維速度的影響（加權影響）。 %%
- DepRL為什麼還需要SCONE環境模擬，他的優勢是?原本的SCONE Controller怎麼在SCONEgym中被實現?
- 參數能不能互通

---
## Conclusion
這是SCONE團隊起初開發SCONE的用途 [Predicting gait adaptations due to ankle plantarflexor muscle weakness and contracture using physics-based musculoskeletal simulations - PubMed](https://pubmed.ncbi.nlm.nih.gov/31589597/)
我們現在可以用SCONE跑出模擬，但跟subject(現在是智翔的資料)的相近程度有限制，因為提供的Mimic function並不多
```
<< measures/Gait10.scone >>
<< measures/EffortWangCubed2000.scone >>
<< measures/DofKnee1.scone >>
<< measures/Grf14.scone >>
<< measures/mimic_dofs_path1_01_hfd.scone >>
<< measures/mimic_path1_01_activations_hfd.scone >>
<< measures/torso_ang_vel_z.scone >>
```
SCONE做出來的行走模型泛用性應該有限制(只能在平地行走，不能走其它地形)
SCONE環境下沒有提供API接口，只能使用內部的Lua Script去開發evolutionary learning的外骨骼Controller來進行模擬

---
### 外骨骼模擬
移到MuJoCo中人體模型會因此失真，所以應該還是會用SCONE這個使用Opensim物理引擎的方案
### HyFyDy
SCONE本質上是對Opensim物理引擎forward dynamic插件，HyFyDy是優化過後的SCONE，創造物件或環境很方便，目前打算用他來做外骨骼的model，否則就要用Opensim去做model但相對複雜很多，MuJuCo則是會造成人體模型失真

---
### SCONEgym+DepRL
[[2206.00484] DEP-RL: Embodied Exploration for Reinforcement Learning in Overactuated and Musculoskeletal Systems](https://arxiv.org/abs/2206.00484)
SCONEgym是SCONE的RL python API，但是Controller跟Measure function無法沿用因為用的ML方法不同沒有轉移過來。
DepRL文獻是直接不使用訓練資料，卻擁有比SCONE還真實的模擬數據
開發Mimic function相對SCONE容易很多
目前會嘗試用Dep這個Hebbian learning的方法可以用來off policy的預訓練model，未來如果要移到患者資料可能就不需要像SCONE方案那樣修改控制器
但現在的運算設備可能不夠train model做出用戶專一的模型->使用H100平台
- [[Gym migration guide]]
- [[DepRL run issule]]

---
## DepRL方案

---
## Deadline：2025/2/10
目標：引入資料集來訓練DEP
為什麼會沒辦法執行出連續的結果，明明已經load policy的權重了
- 解析play code: 作者說checkpoint已經不能用\
確認有沒有電腦可以裝4090
- [[HPC environment]]: 重建python環境，確認環境可以用
```bash
(temp) eddlai.be10@DGX-CN01:~/Downloads$ python depRL/check_pytorch.py 
Checking PyTorch installation...
PyTorch version: 2.5.1
CUDA available: True
Number of GPUs available: 1
GPU 0: NVIDIA H100 80GB HBM3
GPU tensor computation test passed.
```

- 考慮先進行Dep預訓練

已經幾乎理解環境相互依賴的關係

---
### 一些測試結果
修改了`scone_wrapper.py`，沒有解決問題
```python
        ) >= self._max_episode_steps
        info = {
            "termination_reason": "goal_reached" if done else "max_steps_reached",
            "current_time": self.unwrapped.time,
            "total_reward": self.unwrapped.total_reward,
        }
        return obs, reward, done, truncated, info
```

但是myosuite真的可以用

- 失敗`python -m deprl.play --path .\baselines_DEPRL\myoLegWalk_20230514\myoLeg\`
- 可以`python  d:/depRL/examples/example_load_baseline_myosuite.py`

---
train看看model，如果不行的話，要走lua script
已經在嘗試操作HyFyDy，創建新的外骨骼模型\
詢問內容：
- 廠商要外骨骼STL檔案
- 鞋墊

有新同學想加入，給老師看他做的專題

---
## Deadline：2025/2/20
討論分工
- 創建虛擬外骨骼將現有算法寫入(Eric)
	- SCONE or HyFyDy [[Predicting gait adaptations due to ankle plantarflexor muscle weakness and .pdf]]
	- SCONEgym https://scone.software/doku.php?id=doc:sconegym, DEPRL
	- D4PG
		- [[Experiment-free exoskeleton assistance via learning in simulation.pdf]]
		- [[Real-Time_NN_Gait_Phase_Estimation_Using_a_Robotic_Hip_Exoskeleton.pdf]]
		- [[DMP-Based_Motion_Generation_for_a_Walking_Exoskeleton_Robot_Using_Reinforcement_Learning.pdf]]
- 確認CEINMS的詳細分析原理 -> EMG疲乏分析(葉Mark)
	- Opensim
		- [[Muscle Fatigue Analysis Using OpenSim.pdf]]
		- https://opensimconfluence.atlassian.net/wiki/spaces/OpenSim/overview
	- CEINMS 
		- [[documents/Simulation/papers/CEINMS User Guide 0.9.pdf|CINMS User Guide 0.9]]
		- [[CEINMS a toolbox to investigate the influence of different neural control solutions on the prediction of muscle excitation and joint moments during dynamic motor tasks.pdf]]
		- [[Robust_Real-Time_Musculoskeletal_Modeling_Driven_by_Electromyograms.pdf]]

---
![[depRL raw results.png]]SCONE可以用，已經足夠，雖然訓練速度相對緩慢

---
- 下一步要怎麼訓練出像是人的模型˙
	- Generative Adversarial Imitation Learning
	- MAML (Model-Agnostic Meta-Learning)

\
HyFyDy license問題如果用acadamic就不用擔心硬體綁定，正在跟HPC管理員討論
可以先買3萬的方案，但是就要綁定兩個在HPC，管理員覺得OK，再來就是CPU的問題
排隊的問題，他們那邊正在解決

---
![[division of work with new members 20250217.png]]

---
絕對需要進去HyFyDy建模+新的電腦做fine-tuning\
Resources
- Ubuntu+mamba+conda+git
- Data of motion capture and EMG(sean1009): [mocap_EMG_EEG_data - Google Drive](https://drive.google.com/drive/u/3/folders/1d8PC6TvaRWXRju_GHbBgCVanqYTLGN0C)
- github code: https://github.com/eddLai/ExoskeletonPowerAsistance.git
- pls find out these download link on [SimTK: Welcome](https://simtk.org/)
	- Download: python3.11+opensim_python+opensim4.4+CEINMS
	- Download: python3.9+peotry+SCONEpy+SCONE+HyFyDy

---
分工細節\
開會時間
- 大家：15:00(週五)
- Aaron的時間21:00(每兩週的週三)

[[外骨骼_20250222討論,分工及其時程規劃.pdf]]

---
探討fine-tuning
1. 逆向出來的資料，導進depRL，SCONEgym(由sean創分支，把其它code都清掉)
2. reward function and imitation learning

週一下午確認Eric and Mark的進度。
[[imitation learning]]：主要是在解決reward難以定義的問題，但是我們沒有這個問題(如果逆向出來的資料可以用的話)，除非資料不夠多，那就可以用一個輸入的expert資料，把actor換成現在這個

---
[[project download sciprt]]

\
無標記動作捕捉系統建立患者虛擬分身步態模型虛擬分身之客製化長者外骨骼系統

---
## Deadline：2025/3/7
週四晚上前把code跑出東西來，
- Mark, Eric幫我再遠端創額外兩個不同的資料夾放你們跑完code的資料
- 週五開會報告一下你們會做的開發分別是哪部分(對應你們準備修改的code的位置)
- 把圖片更新成給福寶的那個投影片，Motion capture的素材我週五再丟上去，先幫我留文字的title就好

---
修理`data_1009_EMG_steady_to_sto_for_CEINMS_calib`
![[exoskeleton milestone20250307.png]]

---
### 討論結果
開會時間：
- 週五 1200 先沒有老師的會
- 週五 1530 有YY的
>大家開會在進行介紹時，要有圖文說明

多工化開會，分配還沒做的事情去做
- 阻力
- Low_activity的階段

---
## Deadline：2025/3/14\~2025/3/21
### Mark Tasks
CEINMS, **6種不同參數的可能性**，用以之後對接fatigue方法學
- [x] 生理機制兩本書
- 數學模型以及預期差異(function block diagram)
- fatigue模型

---
### Eric Tasks
**大方向上**，只拿opensim IK出來的結果，根據第二點寫一個外骨骼仿人動作，外骨骼的觸發
- LIPM and LPM機器人模型
- 外骨骼獨立模型的可視化mujuco>gazibo>pybullet
- IMU偵測到的low activity(來自步態自發，而非抵抗的狀態)
- 提供一個類似暫停的按鈕的介面
- 透過Myo-Control取代按鈕機制

>共同研究項目：CEINMS預測的資料，預測長度?
[[overview of CEINMS]]

---
### Sean and eddie Tasks
- 挖eddie原本的實驗資料步態同步(以SCONE為主體的對齊)
- 去掉實驗數據的outlier，但是做標記做統計分析(切步態方法不夠準，需要再做到自動化，實驗的時候需要接觸地面壓力的鞋墊)
- 比較虛擬端跟實際資料的差異
- 提供比賽計劃書，需要再跟mocap要資料

討論結論：放棄丟進去驗證，因為需要回饋控制，先驗證虛擬與實驗資料夠相近才能合在一起，再進reward
>畢竟同樣的動作變化會有不同的肌肉組合，此時以實驗資料為標準

---
### Phases of robot walking
![[LIPM and LPM model.png]]

---
SCONE則有
![[phases of SCONE.png]]

---
![[LIPM formula.png]]
2D要改3D

---
ZMP另一個倒立擺行走的方法
![[ZMP foot strike model.png]]
用能量去算

---
第一篇跟第二篇的差異表格

---
#### SCONE倒立擺相關的文獻
[[A Muscle-Reflex Model that Encodes Principles of.pdf]]
![[inverted pendulum model of SCONE.png]]

---
### SCONE 驗證區間
為了進行mimic的fine-tuning\
![[SCONE validation formula1.png|400]]![[SCONE validation formula2.png|500]]

---
![[SCONE validation formula3.png]]

---
#### Opensim跟SCONE比較相近程度
opensim vs scone
![[SCONE Opensim comparison result.png]]

---
#### CEINMS跟SCONE比較相近程度
得到CEINMS結果很糟糕
CEINMS vs SCONE
![[SCONE CEINMS comparison result rect_fem.png]]

---
![[SCONE CEINMS validation result hamstrings.png]]
軟體：可能需要多跑CMC\
硬體：需要壓力感測墊

---
python直接控制外骨骼\
SCONE更新

---
### 架設P100使用環境
%% mv /home/110261026/CEINMS /home/110261026/Exoskeleton %%
GUI很難架\
1.OpenVPN連線
```
2025-03-11 14:54:51 --cipher is not set. Previous OpenVPN version defaulted to BF-CBC as fallback when cipher negotiation failed in this case. If you need this fallback please add '--data-ciphers-fallback BF-CBC' to your configuration and/or add BF-CBC to --data-ciphers.
2025-03-11 14:54:51 OpenVPN 2.5.10 [git:v2.5.10/fccae1fa71140bd6] Windows-MSVC [SSL (OpenSSL)] [LZO] [LZ4] [PKCS11] [AEAD] built on Mar 22 2024
2025-03-11 14:54:51 Windows version 10.0 (Windows 10 or greater) 64bit
2025-03-11 14:54:51 library versions: OpenSSL 1.1.1w  11 Sep 2023, LZO 2.10
2025-03-11 14:54:52 TCP/UDP: Preserving recently used remote address: [AF_INET]140.113.98.129:1194
2025-03-11 14:54:52 UDP link local (bound): [AF_INET][undef]:0
2025-03-11 14:54:52 UDP link remote: [AF_INET]140.113.98.129:1194
2025-03-11 14:54:52 WARNING: this configuration may cache passwords in memory -- use the auth-nocache option to prevent this
2025-03-11 14:54:52 [VPN-S] Peer Connection Initiated with [AF_INET]140.113.98.129:1194
2025-03-11 14:54:54 open_tun
2025-03-11 14:54:54 tap-windows6 device [OpenVPN TAP-Windows6] opened
2025-03-11 14:54:54 Notified TAP-Windows driver to set a DHCP IP/netmask of 192.168.252.10/255.255.255.252 on interface {5C931EA4-AB44-4CDC-9448-FA749B90B025} [DHCP-serv: 192.168.252.9, lease-time: 31536000]
2025-03-11 14:54:54 Successful ARP Flush on interface [10] {5C931EA4-AB44-4CDC-9448-FA749B90B025}
2025-03-11 14:54:54 IPv4 MTU set to 1500 on interface 10 using service
2025-03-11 14:54:59 Initialization Sequence Completed
2025-03-11 20:11:26 [VPN-S] Inactivity timeout (--ping-restart), restarting
2025-03-11 20:11:26 SIGUSR1[soft,ping-restart] received, process restarting
2025-03-11 20:11:31 TCP/UDP: Preserving recently used remote address: [AF_INET]140.113.98.129:1194
```
2.解除P100 Docker容器最小化\
3.GNOME需要開啟Docker的X11設定\
4.問中心怎麼載

---
### HyFyDy綁運算節點
```
(base) eddlai.be10@DGX-CN01:~$ sconecmd --hyfydy id
22:42:28 SCONE version 2.4.0.2990
22:42:28 Successfully initialized OpenSim3 version 3.3-2021-01-28
22:42:28 Could not initialize Hyfydy: License key is not supported on this computer (96a0d4bf385e74c2)

Hardware ID: 96a0d4bf385e74c2
```

```
(base) eddlai.be10@DGX-CN02:~$ sconecmd --hyfydy id
22:43:39 SCONE version 2.4.0.2990
22:43:39 Successfully initialized OpenSim3 version 3.3-2021-01-28
22:43:39 Could not initialize Hyfydy: License key is not supported on this computer (96a0d4bf385e74c2)

Hardware ID: 96a0d4bf385e74c2
```

```
(base) eddlai.be10@login:~$ sconecmd --hyfydy id
22:48:10 SCONE version 2.4.0.2990
22:48:10 Successfully initialized OpenSim3 version 3.3-2021-01-28
22:48:10 Could not initialize Hyfydy: License key has expired (2025-03-06)

Hardware ID: 8e6056df55deaa82
```

---
Fatigue團隊討論, 3月底\
6月四周美國醫學生\
如果explanable方法花太多時間，就先暫停\
一定要去查一下別人做過的\
一定要有虛擬端的馬達電流、IMU之類的，scaling factor
ASAP
肌肉圖到人造unit，跟安妤要

下週二要準備demo畫面介紹

---
要搞硬體，那好像要把別人的設計給偷過來，如果買下來我們能把他拆了自己搞嗎?其實應該不錯
- 把Mark, Cheng給找來一起研究要不要買hypershell來逆向工程(我出錢)
- 自己複刻一條福寶的產線出來


---
## Deadline2025/04/04
本周目標：
- 跟台科大團隊報告的內容
	- 用[Part I: Leg Muscle Force Estimation in Swing - OpenSim Documentation - OpenSim](https://opensimconfluence.atlassian.net/wiki/spaces/OpenSim/pages/53088647/Part+I+Leg+Muscle+Force+Estimation+in+Swing), `B. Simulate swing phase with manually selected excitations`去驗證想法，
	- 目標是肌肉疲乏，看出來是否肌肉疲乏
		- 模擬的全身能量
		- 模擬的步態，EMG到CEINMS計算出來的肌肉控制
		- 從motion的反推結果
- [2025 gSIC 全球學生復健工程與輔助科技創新競賽-臺灣選拔賽 – 健康福祉領域教學推動中心](https://phhw.kmu.edu.tw/2025-gsic-%E8%87%BA%E7%81%A3%E8%B3%BD/)
	- 名稱：~~患者虛擬化神經肌肉骨骼外骨骼輔助模型基於無標記動作捕捉~~ (數位孿生)
	- [Project Description 1000.docx](https://nycu1-my.sharepoint.com/:w:/g/personal/sean950521_be13_m365_nycu_edu_tw/EU-ojMrh4TdLgpPN6Zz-jfEBlUn9weM5RUVkMOaO7zuWcA?rtime=YFAb35Rt3Ug)
	- Teep圖
- Mimic的程度
	- 架好P100環境
	- 怎麼改reward code

[[simulation]]

---
要操作model有哪些事情要做
>The controller is defined by a set of control nodes (time and value pairs) that are linearly interpolated over time to form the muscle excitation signal.

雖然在SCONE的forward失敗了，但是[[opensim forward problem]]應該值得一試
先部分用GUI然後再整合成code的流程
>找解，用不到Static Optimization (SO) and CMC

---

1. 有一個新的CEINMS+Mark的Fatigue模型理論論述 (週二中午)
2. 透過simulink的檔案生成以及數據結果演示 (週三)
3. 透過opensim的簡單展示成果 (週四)
4. 透過punish的DL reward架構 理論論述 (週五)
5. CPG環境的fatigue項目模擬 理論論述 (週五)

---
- [Using Simulink with Python - MATLAB](https://www.mathworks.com/videos/using-simulink-with-python-1683218506123.html)
- Mimic方法是首要任務(但其實說不定可以不用)
- 需要快進到外骨骼的