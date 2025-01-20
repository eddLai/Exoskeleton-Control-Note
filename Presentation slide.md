<style>
    .reveal {
        font-family: 'Times New Roman', '標楷體', serif;
        font-size: 40px;
        text-align: left;
    }
	.with-border{
		border: 1px solid red;
	}
</style>

**髖關節外骨骼暨****AR****交互運動輔助裝置**

**Hip Exoskeleton and AR Interactive Motion Assistance Device**
<!-- element style="font-family:Time new roman; font-size: 80px;"-->
<grid  drag="40 25" drop="20 70" border="thick dotted blue">
***IDEA：雙腳永遠比輪子更具適應性***
</grid>
<!-- element class="with-border fragment fade-up"-->

<br><br><br>

<grid drag="60 35" drop="50 65">
![[1_宣傳示意圖.png]]
</grid>

==%% 輔助而非驅動 %%==

---
核心算法
<!-- element style="; font-size: 60px;"-->
Deep Reinforment learning for <br>
EXO controlling and EMG data mining
<!-- element class="with-border fragment fade-up" style="font-size: 35px; align: left; text-align: left;" -->

%% ==監督式學習需要標註，對於機器人系統這種快速變化，高維度的問題是不足夠的== %%

%%==從環境中學習、自動探索，後面有詳細推導，經過探討確定model free對於劇烈運動是有優勢的==%%


<grid drop="middle">
![[Pasted image 20240522145155.png|700]]
</grid>

---

材料

<split no-margin>
![[Pasted image 20240522175344.png|600]] 
![[Pasted image 20240522175404.png|250]]
![[Pasted image 20240522175425.png|200]]
![[Pasted image 20240522175455.png|200]]
![[Pasted image 20240522175518.png|550]]
</split>

---
模塊關係圖<br>
![[Pasted image 20240522145129.png]]
ESP32 FreeRTOS, Pytorch, C API, BTSerial, WiFi, UnityAR, TensorboardX
<!--element style="; font-size: 25px;"-->
==%% 經過很多實驗才發現很多問題 %%==

---
系統操作流程
![[Pasted image 20240522145705.png]]

---
<grid drag="60 35" drop="18 55">
![[15_完整Demo.svg]]
</grid>

***Learning directly from data allows for more flexible adaptation to rapid changes in motion and provides more accurate control[14], which is our core philosophy for this algorithm.***
<!-- element style="; font-size: 25px;"-->

[https://youtu.be/HmNPBUC3Tf4](https://youtu.be/HmNPBUC3Tf4)
<!-- element style="; font-size: 25px;"-->
==%% 從零開發四個月 %%==

---
演算法<!-- element style="; font-size: 60px;"-->
<br><i class="fas fa-sync fa-spin fa-1x"></i>
<br>解讀EMG資料(獲取特徵)<br>伺服馬達控制

---
EMG預處理
**信號處理步驟**：
- `bandpass_filter`**帶通濾波**：去除信號中的低頻和高頻噪聲，只保留特定頻率範圍內的信號，這樣可以去除肌肉信號中的基線漂移和高頻噪聲。
+ `notch_filter`**陷波濾波**：用來消除工頻干擾（例如來自電源的50或60 Hz干擾）。
+ `full_wave_rectification`**全波整流**：將信號的所有部分轉換為正值，確保信號只有正值部分，這樣可以更容易地提取信號包絡。
+ `lowpass_filter`**低通濾波**：用來提取信號的包絡，平滑信號，去除高頻成分，使信號更易於分析。

---
肌肉強度水平計算（Muscle Strength Level Calculation）
- `map_to_levels` <br>
將值映射到超出5到-5級的線性值上，基於放鬆閾值和初始最大RMS值，
分為十個等級區間。
- `calculate_emg_level`<br>
權重 `ta`、`rf`、`bf` 和 `Ga` 用於不同的通道，以加權它們對總強度的貢獻，因為我們的目標是做特定動作(例如走路就有其特定權重)的力量增強

---
Brief review of traditional RL methods: <br> Policy Gradient-Actor and Environment 的互動
- the probability of a trajectory:==state==, ==action==, ==policy==
$$P\left(\tau\right)=p\left(s_0\right)\prod_{t=0}^{T}{\pi\left(a_t\middle|\ s_t\right)p\left(s_{t+1}\middle|\ s_t,a_t\right)}$$

- Proximal Policy Optimization (PPO): 最佳化==Env== ==Reward==
$$\nabla_\theta J\left(\theta\right)=E_{s\sim\rho^\pi,a\sim\pi}\left[Q^\pi\left(s,a\right)\nabla_\theta\log{\pi}\left(a\middle|\ s;\theta\right)\right]$$

value function $Q^\pi\left(s,a\right)$, 用來從s, a評估預期的R

---
迭代優化

$$J\left(\theta\right)=E_{\tau\sim\pi_\theta}[Rτ]$$

$$\theta\gets\theta+\alpha\nabla_{\theta} J(θ)$$<br>
$$\mathrm{\nabla}_{\theta}J(θ)=Eτ∼πθ[Rτ∇θlogπθτ]$$
<br>直接取得期望值是困難的，所以用sampling的方式
$$\nabla_\theta J(\theta) \approx \frac{1}{N} \sum_{n=1}^N R(\tau^n) \nabla_\theta \log \pi_\theta (\tau^n)$$<br>
$$\nabla_\theta J\left(\theta\right)\approx\frac{1}{N}\sum_{n=1}^{N}\left(\sum_{t=1}^{T^n}{R\left(t\right)\nabla_\theta}\log{\pi_\theta}\left(a_t^n\middle|\ s_t^n\right)\right)$$

---
假設滿足Markov property，<br>
「未來的狀態只取決於當前的狀態」<br>
對於越後面發生的後果，影響越小。

$$G_t=\sum_{k=0}^{\infty}{\gamma^kR_{t+k+1}},\ then$$
$$\mathrm{\nabla}_\theta\ J\left(\theta\right)=E\left[\sum_{t=0}^{T}\nabla_\theta\log{\pi_\theta}\left(a_t\middle|\ s_t\right)G_t\right]$$
---
Q-learning:若同時評估狀態-策略的好壞?而不單看策略。

$$V^\pi\left(s\right)=Q^\pi\left(s,\pi\left(s\right)\right)$$

(這可以被用到PPO中，但前面沒有介紹到)<br>
Q-learning的核心想法：
$$\pi^\prime(s) = \arg\max_{a} Q^\pi(s, a)$$
$$V^{\pi^\prime}\left(s\right)\geq\ V^\pi\left(s\right)$$<br> for all status, $$V^\pi(s) \leq \arg\max_{a} Q^\pi(s, a) = Q^\pi(s, \pi^\prime(s)))$$
---
Prove:
![[Pasted image 20240524133018.png|1000]]

---
迭代優化

為了得到一個越來越厲害的Q<br>計算實際Reward 與 初始預估Reward
$$TDError=\left(R\left(s,a\right)+\gamma\max_{a^\prime}{Q}\left(s^\prime,a^\prime\right)\right)-Q\left(s,a\right)$$
<!--element style="; font-size: 35px;"-->
$$Q^{new}\left(s,a\right)\gets Q\left(s,a\right)+\alpha\left[R\left(s,a\right)+\gamma\max_{a^\prime}{Q}\left(s^\prime,a^\prime\right)-Q\left(s,a\right)\right]$$
<!--element style="; font-size: 35px;"-->

---
<grid drag="35 30" drop="0 60">
![[Pasted image 20240525150434.png]]
</grid>


Deep Q learning<br>
傳統Q-function是表格形式，用於對付離散問題，例如：鍵盤的左右上下。
如果用NN實現呢?<br>
$$J\left(\theta\right)=\left(TDError\right)^2$$ $$J\left(\theta\right)=\left(r_t+\gamma\hat{Q}\left(s_{t+1},a_{t+1};\theta^-\right)-\hat{Q}\left(s_t,a_t;\theta\right)\right)^2$$
衍生的instability and data sample correlation issues:
- experience replay
- fixed target Q-networks

以程式碼實現

---

From Q-learning to Deep Deterministic Policy Gradient (DDPG) 
<br>把DQN加上Actor NN，也因此可以處理連續空間。

對連續空間選擇，並進行迭代優化。
$$\nabla_{\theta^\mu}J\approx E_{s\sim\rho^\beta}\left[\nabla_aQ\left(s,a\middle|\theta^Q\right)|_{a=\mu\left(s\middle|\theta^\mu\right)}\nabla_{\theta^\mu}\mu\left(s\middle|\theta^\mu\right)\right]$$
<!-- element class="with-border fragment fade-up"-->
deterministic policy NN 代表直接輸出動作，而非機率(相比於PPO的作法)

$$L\left(\theta^c\right)=E_{\left(s,a,r,s^\prime\right)\sim D}\left[\left(r+\gamma Q_{\theta^{c-}}\left(s^\prime,\mu_{\theta^{\mu-}}\left(s^\prime\right)\right)-Q_{\theta^c}\left(s,a\right)\right)^2\right]$$
相比Q-learning，顯示的學習及輸出策略<br>
(以程式碼的流程實現)

---
**D4PG**
<!--element style="; font-size: 80px;"-->
用以改善確定性算法的==確定性==
- overly deterministic action selection
- oversimplified estimation of environmental rewards
- failing to capture the dynamics
- uncertainties of the environment adequately
使用離散支持點

---
$$z_i = V_{\text{min}} + i \cdot \Delta z \quad \text{for} \quad i = 0, 1, \ldots, N-1
$$
<!--element style="; font-size: 30px;"-->
$$\Delta z=\frac{V_{\mathrm{max}}-V_{\mathrm{min}}}{N-1}$$
<br>$$tz_j=\min{\left(V_{\mathrm{max}},\max{\left(V_{\mathrm{min}},r+\gamma z_j\right)}\right)}$$<br>
$$b_j = \frac{tz_j - V_{\text{min}}}{\Delta z} \biggm| = \left\lfloor b_j \right\rfloor, u = \left\lceil b_j \right\rceil$$
<br>$$L(\theta^c) = \text{Distance}(\text{ProjDistr}, \text{PredDistr})$$

$$L(\theta^c) = E(s, a, r, s') \sim D\left[ \text{Distance}\left( \text{Proj}[R(s, a) + \gamma Q \theta^c - (s', \mu \theta \mu - (s'))], Q \theta c(s, a) \right) \right]$$

<!--element style="; font-size: 25px;"-->



---
系統即時資料導入<!-- element style="; font-size: 60px;"-->

Real-time是最困難的<!-- element class="with-border"-->

考驗系統的穩定以及EMG是沒辦法用模擬的，沒有看到類似內容文獻，目前是初階力量少的版本，穩定後會與廠商討論硬體的修改。

---
![[Pasted image 20240522182005.png]]

<grid drag="80 30"bg="gray">
**Figure 16.** **Joints’ angle changes when walking** Display the variation in walking angles returned by the exoskeleton, excerpting the results of model training initiated on March 30, 2024, at 23:30:36, for the command steps 400 to 600 interval.
<!-- element style="font-size: 25px;align: left; text-align: left;"-->
</grid>

---

![[Pasted image 20240522182142.png]]
<grid drag="80 30"bg="gray">
**Figure 17.** **Joints’ velocity changes when walking** The data depicted in this figure is extracted from the same interval as the preceding one. The units are in deg/s.
<!-- element style="font-size: 25px;align: left; text-align: left;"-->
</grid>

---

![[Pasted image 20240522182438.png]]
<grid drag="80 30"bg="gray">
**Figure 18.** **Joints’ current changes when walking** When a command is issued and resistance current occurs, the resulting values will approximately double in proportion, thereby allowing inference regarding the resistance experienced by the exoskeleton. The unit of y-axis: 0.01A.
<!-- element style="font-size: 25px;align: left; text-align: left;"-->
</grid>

---
<grid drag="80 30"bg="white">
![[Pasted image 20240522182525.png]]
</grid>
<br>
<grid drag="80 30"bg="gray">
**Figure 19.** **Joints’ IMU changes when walking** This is the training process starting at the same time, demonstrating changes in gait IMU, which can therefore be utilized for motion protection judgment. The units are in 0.1 degrees.
<!-- element style="font-size: 25px;align: left; text-align: left;"-->
</grid>
---
%% 
<grid drag="80 30"bg="gray">
<!-- element style="font-size: 25px;align: left; text-align: left;"-->
</grid>

--- %%

性能表現:從模型的角度
<!-- element style="; font-size: 60px;"-->
![[Pasted image 20240522182705.png]]
**Figure 20. Differences of Rewards when walking after model optimization**<!-- element style="; font-size: 25px;"-->

---
性能表現:從EMG的角度
<grid drag="80 30"bg="white">
![[Pasted image 20240522182850.png]]
</grid>

**Figure 20. Differences of Rewards when walking after model optimization**<!-- element style="; font-size: 25px;"-->
==%% 不可能從關節資訊獲得回饋，因為那是外骨骼的 %%==


---
後續優化<br>
解決ESP32傳輸斷線問題導致系統不穩定：<br>
推測與ESP32 Wifi性能有關

- Dockerization
- 更強的模型做個特徵擷取
- Xilinx KR260 SoM：FPGA潛力
- ESP32 WiFi斷聯實驗：雲端管理
- ChatwithRTX：強化虛擬教練
- 自主開發無線EMG貼片、外骨骼馬達
==%% 最近再把整套系統包含廠商的資料搬上去Linux %%==

---
[[旺宏作品計劃書exoskeleton組v1.1.pdf]]
<br>[[documents/計劃書/附件1_外骨骼系統源代碼v2.pdf]]
<br>[[附件2_示範影片.pdf]]
<br>(論文引用、以及產品規格)

謝謝大家
<!-- element class="fragment fade-up"-->

---