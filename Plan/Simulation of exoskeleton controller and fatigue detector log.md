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
Develop log: EXO in simulation, better fatigue detector
<!-- element style="font-size: 35px;align: left; text-align: left;color: white"-->
</grid>

<grid drag="50 10" drop="40 70">
賴宏達、劉智翔、葉亘祐、曾峻魁、Aaron Wang
<!-- element style="font-size: 30px;align: right; text-align: right"-->
</grid>

<!-- slide bg="../NTKLab_white bg_cover_resize.png"-->

---
# 速記
HMI, 4 indexs to evalution
也許外骨骼與虛擬人體小腦可以合併在同一個模型中

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
# Deadline2025/04/04
本周目標：
- [ ] 跟台科大團隊報告的內容
	- 用[Part I: Leg Muscle Force Estimation in Swing - OpenSim Documentation - OpenSim](https://opensimconfluence.atlassian.net/wiki/spaces/OpenSim/pages/53088647/Part+I+Leg+Muscle+Force+Estimation+in+Swing), `B. Simulate swing phase with manually selected excitations`去驗證想法，
	- 目標是肌肉疲乏，看出來是否肌肉疲乏
		- 模擬的全身能量
		- 模擬的步態，EMG到CEINMS計算出來的肌肉控制
		- 從motion的反推結果
- [x] [2025 gSIC 全球學生復健工程與輔助科技創新競賽-臺灣選拔賽 – 健康福祉領域教學推動中心](https://phhw.kmu.edu.tw/2025-gsic-%E8%87%BA%E7%81%A3%E8%B3%BD/) 完成初稿
	- 名稱：~~患者虛擬化神經肌肉骨骼外骨骼輔助模型基於無標記動作捕捉~~ (數位孿生)
	- [Project Description 1000.docx](https://nycu1-my.sharepoint.com/:w:/g/personal/sean950521_be13_m365_nycu_edu_tw/EU-ojMrh4TdLgpPN6Zz-jfEBlUn9weM5RUVkMOaO7zuWcA?rtime=YFAb35Rt3Ug)
	- Teep圖
- [ ] Mimic的程度，先暫停因為不是那麼必要
	- [x] 架好P100環境(放棄，因為不能用hyfydy GUI)
	- [ ] 怎麼改reward code(等智翔的一篇介紹)

[[simulation draw]]

---
## 計劃書撰寫sean, eddie
計劃書的重點「我們的東西(新方法)+對於應用上的論述」\
*"Deploying ==rehabilitation== exoskeleton with ==digital twins== in synthetic data generation on neuro-musculoskeletal modeling"*
data generation 改成 data synthesis\
800~850的字差不多

### 大綱
- 專案背景 -> 點出想要解決的問題
- 方法
- (不用把技術細節都講出來，只要講技術的流程點)
- 詳細介紹對於醫療上的用途以及規劃，用於老人行走等日常需求
- 技術難點(以及我們計畫的完整性)
	- Fatigue
	- HMI人機互動的困難
	- 對於患者長時間訓練會出現的問題
	- 建出本人的Mimic方法

---
## 規劃異動
如果要盡快進入demo
- Mimic方法不是首要任務(但其實說不定可以不用)
- 需要快進到外骨骼的控制
	- 外骨骼的模型怎麼做(Eddie and Sean)
	- CPG加上docker環境的SCONE改動(Eric and Sean) 放棄因為沒有要用CMA，直接透過sconegym, lua或hyfydy

---
## 要操作人體model有哪些事情要做
>The controller is defined by a set of control nodes (time and value pairs) that are linearly interpolated over time to form the muscle excitation signal.

雖然在SCONE的forward失敗了，但是[[opensim forward problem]]應該值得一試
先部分用GUI然後再整合成code的流程
>找解，用不到Static Optimization (SO) and CMC

---
1. 有一個新的CEINMS+Mark的Fatigue模型理論論述(作圖) (週二中午)
2. 透過simulink的檔案生成以及數據結果演示 (週三)
	- 怎麼把CEINMS包裝成simulink可以接的結構?
	- [[Overview of simulink]]
3. 透過opensim的簡單展示成果 (週四)
4. 透過punish的DL reward架構 理論論述 (週五)
5. CPG環境的fatigue項目模擬 理論論述 (週五)

---
## 環境與開發工具 eddie
- 已經統一環境(在HPC上還沒辦法做出CEINMS需要的環境)
simulink，本質上還是開發第三方庫，而非融合
- python：需要把python打包成src庫才可以這樣使用
- C：可以打包自己的個人庫

---
## 外骨骼模型與控制 eddie, eric
我想要建立一個自己的外骨骼硬體模型，並可以透過腳本直接控制他

>控制方法的討論：現在已經可以用的policy人體行走模型應該也可以用到人身上吧

---
## 初步規劃
討論CEINMS跟opensim的關係\
要重構一個全身性的模型應該沒有那麼簡單\
發展神經肌肉一套轉換系統，是為了應對臨床端的需求，那就獨立框架\
DepRL則是對於用於通用外骨骼系統的最終願景
- 跟YY說可以約時間，簡單介紹一下投影片內容
- 要STL的外骨骼建模檔案，並完成外骨骼模型的功能驗證
- 進入sim 2 real

---
## Lua
物件行為
[Script Examples [SCONE]](https://scone.software/doku.php?id=tutorials:script)\
[[overview of SCONE]]

Controller: 用作控制
>**Feedforward Controller**相反於feedback:
是一種控制方法，它根據**預先知道的系統模型或預期的輸入**，直接計算出需要施加的控制輸出，**不依賴於當前輸出的反饋來修正行為**

Measure: 用作基因演算優化
偏離解的問題：
- `par:create_from_mean_std(...)`可以設定
- Regularization 項（偏好特定模式）
- penalty（懲罰不想要的動作）
```lua
local deviation = 0
for i = 1, #actuators do
    local current = actuators[i]:activation()
    local expected = reference_excitation[i][model:time()]
    deviation = deviation + (current - expected)^2
end

fitness = fitness - weight * deviation

```

---
## Hyfydy
[[Overview of Hyfydy]]\
[Documentation - Hyfydy](https://hyfydy.com/documentation/)\
透過建模了解物件組成結構
- target_ori
- target_vel
- troque_offset
- joint_force_pnld
- joint_force_pd
- contact_force_hunt_crossley

---
### EXO_model
![[exo_in_hyfydy.png|400]]
雖然看起來是對的，但是座標位置導致Joint位置錯誤(上圖)，修改CAD STLfile(下圖)，不知道geometry怎麼樣\
![[Exo_sim_1.png|300]]![[Exo_sim_2.png|300]]

---
### 沒有寫在SCONE範例中的內容：
總共有五份文件可以參考
- ScriptControllerTreadmill.lua
- ScriptControllerFeedForward.lua
- ScriptControllerGyroBalance.lua
- ScriptControllerNeuralDelays.lua
- ScriptControllerReflexModulation.lua
- ScriptMeasureBodyHeight.lua

---
創建Vec3 and quat找了很久，設定錯誤的參數會導致SCONE 軟體crash
[ScopePy Reference Manual [SCONE]](https://scone.software/doku.php?id=doc:sconepy&s[]=vec3#quat)
- `vec3:new(1 1 1)`
- `quat:new(1 1 1 1)`
- `set_motor_target_vel()`要搭配`joint:set_motor_target_ori`不能單獨使用，本質上是PD控制器
- 現在看起來torque是最好的

---
必須的結構\
`function init(model, par) end`\
`function update(model) end`\
如果是Measure.lua則多了\
`function result( model ) end`\
`function store_data( frame ) end`，要儲存成資料只能寫在這裡，畢竟沒有優化就不用

---
HyFyDy:==在Lua實現中並非class，分散各地==\
PD控制器\
$$q=\cos\left({\frac{\theta}{2}}\right)+\sin\left({\frac{\theta}{2}}\right)\left(x i+y j+z k\right)$$\
$$q={\left[\begin{array}{l}{w}\\ {x}\\ {y}\\ {z}\end{array}\right]}={\left[\begin{array}{l}{\cos(\theta/2)}\\ {u_{x}\cdot\sin(\theta/2)}\\ {u_{y}\cdot\sin(\theta/2)}\\ {u_{z}\cdot\sin(\theta/2)}\end{array}\right]}$$\
$$T=K_{p}\cdot(q_{t a r g e t}-q_{\mathrm{current}})+K_{d}\cdot(\bar{q}_{t a r g e t}-\bar{q}_{\mathrm{curemt}})$$\
$$\begin{array}{l}{{K_{p}:s\mathrm{tiffness}}}\\ {{K_{d}:\mathrm{damping}}}\end{array}$$

---
Controller本質上是Actuator的一個控制節點，可作權重優化\
Actuator or LuaDelayedActuator
- point_path_muscle
- joint_point_path_muscle
- joint_motor

ScriptController是一個可以調控的開關的結構\
model: 就是用來建立sensor

---
Luascone:
- LuaQuat quat_from_euler_deg(double x, double y, double z)	create quaternion from Euler angles (xyz degrees)
- LuaQuat quat_from_euler_rad(double x, double y, double z)

LuaParams:
- LuaNumber create_from_mean_std(LuaString name, LuaNumber mean, LuaNumber stdev, LuaNumber minval, LuaNumber maxval)
- LuaNumber create_from_string(LuaString name, const std::string &value)

LuaFrame:  進入scone Analysis window

---
# Deadline2025/04/11
無論如何當然還是要有展示的科學數據
- 4/10Vivian專案募資討論
- 討論SCONE script語法，幫所有人快速入門
- 週四晚上跟YY討論第二版本的計畫書
- 4/12交醫工創新比賽
- 4/15台科大團隊討論
- 4/20要給Vivian Business Plan
- 5/10
- 5/22到美國募資

---
## 面試問題
現在有這些神經模型，\
要怎麼建立一個虛擬外骨骼。\
猜圖

---
## 虛擬外骨骼控制器訓練
- 把步態資料抓出來
- 設計簡單的控制器
- 測試Measure優化方法
- CPG Script控制器
- 簡單demo 人在行走vs外骨骼擺動 同步
- 包裝進sconepy
- 建模人體與外骨骼的相互作用力
- 透過模擬的上帝視角，驗證這個方法是否提前給力，達到輔助效果
- 測試不同環境，跑步機之類的
- 整合D4PG進去depRL

---
## CEINMS資料訓練
- 把

---
商業模式\
像是Android上的各種APP一樣\
未來，如果外骨骼是一個通用的人手一個的\
透過ROS，我們可以廣泛的推廣這樣的服務\
當初手機市場怎麼出現Android，這個生態圈的
[Android 滿 10 歲了！4 個歷史 重要里程碑 帶你一起回顧 - 電腦王阿達](https://www.koc.com.tw/archives/219189)
最一開始需要有一個夠好的硬體去提供這個

---
## 預期的結果圖
- EMG的圖數值出了點問題


---
要改在Joint上還是DOF上去做控制?
- hinge（鉸鏈）joint
- ball（球形）joint

---
發散一點不要限縮在一個特定的應用。都拿出來討論


---
ROS
- 現在市場普及
- 硬體層怎麼設計的
- 多吃效能