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
賴宏達、劉智翔
<!-- element style="font-size: 40px;align: right; text-align: right"-->
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
- 下一步要怎麼訓練出像是人的模型˙
	- Generative Adversarial Imitation Learning
	- MAML (Model-Agnostic Meta-Learning)

---
![[division of work with new members 20250217.png]]