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
![[RL iteration flow.png|400]]
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

---
## 討論與結論:
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
- [x] D4PG能夠更好的去控制複雜意圖的判斷(需要驗證)
$$T=K_t \cdot I$$
$$T_{required}=T_{original}-T{ext}$$
$$I_{new}=\frac {T_{required}}{K_t}$$

---
### Reward設計
可以判斷抬升方向
- 外力順時針
	- 馬達往前移動(從角速度)(順時針)，正電流減少 (對抗)
	- 馬達往後移動(從角速度)(逆時針)，負電流減少 (抬升)
- 外力逆時針
	- 馬達往前移動(順時針)，正電流增加 (抬升)
	- 馬達往後移動(逆時針)，負電流增加 (對抗)

對抗：馬達沒有跟上
抬升：馬達在提供輔助
越疲乏分數絕對值越高: [[level of fatigue from EMG]]

| 相同嗎 | 意圖  | 疲乏  | 跨距  |
| --- | --- | --- | --- |
|     | 1   | 1   |     |
|     | 0   | 1   |     |
|     | 1   | 0   |     |
