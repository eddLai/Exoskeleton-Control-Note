## 目標與方法
- 疲乏時==修正回正常==: 
	- Proportional Electromyography Control比例肌電控制: 需要{外骨骼力量}
	- Output要對應到一個{步態週期}裡頭，用{阻力}
- ==動作意圖==
	- 搬很重的東西時提供輔助
	- 準備起步
	- 準備停下來
	- 轉向
		- 重心轉移計算

==Output:離散 or 連續==

--- 
步態週期：腳跟落地到下次落地
討論Actor輸出:
- DNN：連續速度輸出，大多論文使用的是力矩
	- Reward怎麼判斷好壞
		- 判斷疲乏
		- 判斷想走快走慢:
			- 步態是否受到影響，{阻力}?
			- 重心是否不連續
		
		得到力矩:
		- 速度對應電流(做實驗)(input: EMG?))
- TCN：離散輸出動作意圖，Reward要怎麼設計
- 啟動與否，用NN學一個步態
- 系統更新頻率之間用instant or duration
	- 更迭頻率可以降

AUC

---
- Duration -> DNN?TCN -> 步態pattern函數
- 阻力+EMG -> 啟動狀態
- 系統更迭+速度 \* t->Output -> 目標：單個步態週期內，定速、雙腳協調的穩定
- 判斷疲乏 -> 啟動與否 -> Reward: 評估跟常模的差異
- PID and RL 控制理論，輸出人的表現:肌肉、步頻步伐，角度是不可知道的

關馬達，收Data，把物理量與EMG交叉比對(correlation)
![[Pasted image 20240723160705.png|400]]
1. 找安妤要資料 -> reward函數設計，力量少不代表力竭，==EMG訊號可以判斷出力竭==
2. train data 要固定、跑步機，測試KV260正不正常 (週五前)

---
## 可用參數
5Hz
f(開始, 結束), f() = 1,-1; 
Input:()
(1),(2) 上個狀態去預估下個狀態
1. Vel +/-: 得知擺動前後
2. Vel 大小:走快走慢
3. Acc :
```python
(1) Joint1, Joint2
(2) Joint1_Velocity, Joint2_Velocity
(3) Joint1_current, Joint2_current
(4) Roll, Pitch, Yaw
(5)
'Tibialis_anterior_right',  # 通道1: 右腿脛前肌
'Rectus Femoris_right',     # 通道2: 右腿股直肌
'Biceps_femoris_right',     # 通道3: 右腿股二頭肌
'Gastrocnemius_right',      # 通道4: 右腿腓腸肌
'Tibialis_anterior_left',   # 通道5: 左腿脛前肌
'Rectus Femoris_left',      # 通道6: 左腿股直肌
'Biceps_femoris_left',      # 通道7: 左腿股二頭肌
'Gastrocnemius_left'        # 通道8: 左腿腓腸肌
```

- [x] 段落全不不勾，最小行距
- [ ] [1] 要找有外骨骼以及疲乏的論文，討論為什麼要用RL，introduction，background review，RL配合review有一個清楚的為什麼要用這個架構，優勢?的說明
- [ ] 改成新的methods
- [x] AR要拿掉
- [x] Figure2 腳的圖
待討論:
- [x] 不要Gait pattern(都已經用NN架構了?)，把Env減小
- [x] Reward負責確保人機互動，減少人機阻力
- [x] Agent負責動作意圖，Motor架構
反正要訓練出在不同的疲乏程度下，做出正確的意圖判斷
方案A：scale：fatigue下，設計reward，隨著fatigue加權變小，不夠好，所以要Ouput更多
方案B：量化疲乏程度，reward，actor升力+越接近最佳的步態，正值

- [ ] 與正常的差異，最佳狀態的步態物理量+EMG資料
- [ ] 正確的人機互動的Reward抬腳
- [ ] 把能夠意圖預測做Scale
- [x] 怎麼知道阻力，不是抬升輔助的力量

- [x] 分出前或後的推力
- [x] 流程圖要有minimize muscle effort
- [x] 確保圖中元素都有提到
- [ ] D4PG能夠更好的去控制複雜意圖的判斷(需要驗證)
$$T=K_t \cdot I$$
$$T_{required}=T_{original}-T{ext}$$
$$I_{new}=\frac {T_{required}}{K_t}$$
可以判斷抬升方向
- 外力順時針
	- 馬達往前移動(從角速度)(順時針)，正電流減少 (對抗)
	- 馬達往後移動(從角速度)(逆時針)，負電流減少 (抬升)
- 外力逆時針
	- 馬達往前移動(順時針)，正電流增加 (抬升)
	- 馬達往後移動(逆時針)，負電流增加 (對抗)

對抗：馬達沒有跟上
抬升：馬達在提供輔助
越疲乏分數絕對值越高

| 相同嗎 | 意圖  | 疲乏  | 跨距  |
| --- | --- | --- | --- |
|     | 1   | 1   |     |
|     | 0   | 1   |     |
|     | 1   | 0   |     |

[5]
[6] 哪幾項假設，哪幾項因素會導致不精準

This approach aims to overcome the traditional dynamics models encounter when handling rapid motion transitions.

Given the personalized characteristics of EMG signal, we have chosen a Deep Learning (DL) architecture, surpassing the performance of traditional dynamics models [5, 6]

欠驅動系統
傳統模型，需要一些精確的動作假設，為了滿足假設，有時需簡化被動關節，也需考慮馬達的機械系統方能使系統精確，RL的架構使得指導模型的過程自動化，deep learning 的引入讓RL不需要顯式的公式或者列表，而能保持架構的靈活性。

In exoskeleton technology development, achieving precise and adaptable interaction force control is critical, particularly as we plan to conduct experiments on actual underactuated exoskeleton platforms and extend our interaction force control algorithm to lower limb hydraulic exoskeletons with complex multi-phase dynamics during different gait phases. Traditional mathematical models often fall short in flexibility and adaptability, especially when facing these highly nonlinear and time-varying system dynamics. Reinforcement Learning (RL) emerges as a superior solution, offering the ability to dynamically learn and adjust strategies through continuous interaction with the environment. This capability is crucial as it allows for the adaptation to the unpredictability of real-world applications and enhances safety and operational efficiency in scenarios requiring load carrying and the prediction of short-term user intentions, such as with the HUALEX system. Thus, employing RL over traditional methods is essential for advancing exoskeleton technologies, ensuring more synchronized and responsive human-machine interactions.

We employ the Distributed Deep Deterministic Policy Gradient (D4PG) strategy to detect walking intentions and enhance Human-Machine Interaction (HMI) [4]. The Temporal Convolutional Network (TCN) acts as the actor, identifying time series and understanding user action intentions during muscle fatigue, subsequently commanding the motor controller. The Deep Q-Network (DQN) optimizes the actor's performance. This data-driven approach simplifies the training process by allowing the user to walk at multiple speeds while interacting with the environment. To test our hypothesis that the system provides precise control to reduce the burden on the Rectus Femoris and Biceps Femoris muscles during walking, we conducted experiments comparing integrated EMG (iEMG) with and without assistance (Figure 1).

對外骨骼的敘述
action intention detection
Real-time
D4PG
Hip Exoskeleton
motion assistance when fatigue and lifting

論文==#Muslce fatigue is one of the harmful outcome of prolong physical activities.If it gets less concentration on it, the safety and healthy risk not only be the potential problem. Consequently, it inspire me to develop the  project , which is a system aims to reduce the  intensity of specific muscle usage and extend the duration of strenous acticities.#==

[[s41586-024-07382-4 (1).pdf]]，了解肌肉那部份的建模，RL可以問博維


