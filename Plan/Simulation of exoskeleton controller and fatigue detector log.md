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

計劃書的重點「我們的東西(新理論)+對於應用上的論述」\
*"Deploying ==rehabilitation== exoskeleton with ==digital twins== in synthetic data generation on neuro-musculoskeletal modeling"*
data generation 改成 data synthesis

800~850的字差不多
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
## 環境與開發工具 eddie
- 已經統一環境(在HPC上還沒辦法做出CEINMS需要的環境)
simulink，本質上還是開發第三方庫，而非融合
- python：需要把python打包成src庫才可以這樣使用
- C：可以打包自己的個人庫

---
## 外骨骼模型與控制 eddie, eric
我想要建立一個自己的外骨骼硬體模型，並可以透過腳本直接控制他
[Documentation - Hyfydy](https://hyfydy.com/documentation/)

>討論：現在已經可以用的policy人體行走模型應該也可以用到人身上吧

---
# Deadline2025/04/11