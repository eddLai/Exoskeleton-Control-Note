# IDEA
- ref. 
	- [[Characterization of muscle fatigue in the lower limb by sEMG and angular position using the WFD protocol.pdf]] [1]  Table2 Fatigue的定義有待商榷
	- [[Effects of various walking intensities on leg muscle fatigue and plantar pressure distributions.pdf]] [2]
	- [[Muscle Fatigue Analysis Using OpenSim.pdf]]

$EMG_{FT}$
# Fatique
由於個體差異，需要用統計方法在嘗試得到人體常模。
或者使用一些數學分析（例如頻率）找到數據的一致性。
## Factors of fatique
- insufficient blood perfusion of muscle fibers
- depletion of energy sources
- metabolites’ build-up $\rightarrow$ excess hydrogen ions ***"slows down the waveform of an action potential"***

>ref. [[Effects of various walking intensities on leg muscle fatigue and plantar pressure distributions.pdf]]
>***Synchronization of the motor unit pool leads to an increase in amplitude and an increase in the duration of the activation of the EMG signal***
>頻率降低，但是振幅提升（因為同步性）
>ref. [[Characterization of muscle fatigue in the lower limb by sEMG and angular position using the WFD protocol.pdf]]
>![[RF muscle amplitude in different level of faitque.png|400]]
隨著phase的不同，股直肌過度用力（恢復機制），為了繼續產生運動並協助在疲勞階段進行代償的肌肉

ref. [[Characterization of muscle fatigue in the lower limb by sEMG and angular position using the WFD protocol.pdf]]
![[heart rate when fatigue.png|400]]
### Characteristics
- RF在結束後會出現恢復性過勞行為 $> sEMG_{init}$
>post-fatigue behavior increasing the electrical amplitude until even exceeding the initial level
- 補償機制：
	- **RF和GL肌肉**在15分鐘時顯示出疲勞，並在隨後的測試中表現出一定的電活動增強，顯示肌肉有恢復過度使用的跡象。
	- **TA和BF肌肉**則在測試期間顯示出穩定的疲勞指標，沒有顯著恢復。
- pathological changes of neuromuscular regulations in patients with neurological impairments and is able to detect a decreasing pattern of EMG complexity
- speeds
	- 脛前肌（TA）會主動縮短，踝關節背屈，會加速疲勞



---
# Amplitude
ref. [[Characterization of muscle fatigue in the lower limb by sEMG and angular position using the WFD protocol.pdf]]
![[different muscles when fatigue.png||600]]
1. RF（股直肌）疲乏中期會下降，後期代償會增加
2. BF（股二頭肌）肌肉都會增加
3. TA 疲乏初期也會下降
4. GL 中期較大

![[different mean of muscles when fatigue.png|600]]
誤差條的“鬍鬚”代表了每位參與者的sEMG信號振幅的變異範圍
系統需要能夠理解代償，或者要想辦法fit回去

---
# Frequency analysis
### Median Frequency
==步行速度的增加，脛前肌(TA)的肌電圖中值頻率會顯著下降==
ref. [[Effects of various walking intensities on leg muscle fatigue and plantar pressure distributions.pdf]]
$$Z_{xx}(f,t) = \mathcal{F} \left\{ x(t) w(t - \tau) \right\}$$
$$P(f,t) = |Z_{xx}(f,t)|^2
$$
$$\text{Median Frequency} = \text{median} \left( P(f,t) \right)
$$

---
# Statistics Method
ref. [[Characterization of muscle fatigue in the lower limb by sEMG and angular position using the WFD protocol.pdf]]
為了對抗個體差異，因此必須考慮統計方法。方可得到人類的常模（母體均值）。
### Recall
樣本均值鄉對於母體均值的波動變化
SD樣本標準差，$\bar{x}$ 樣本均值
$$SE=\frac{SD}{\sqrt{n}}$$
SE越小就越接近母體
$$CI=\bar{x}+Z_{0.95} \cdot SE$$
Tukey檢驗
單因素ANOVA後使用
$$\Delta \bar{Y}_{ij} = \bar{Y}_i - \bar{Y}_j$$
$$SE(\Delta \bar{Y}_{ij}) = \sqrt{\frac{S^2}{n_i} + \frac{S^2}{n_j}}$$
$$q_\alpha透過顯著水平\alpha定義臨界值$$
$$|\Delta \bar{Y}_{ij}| > q_\alpha \cdot SE(\Delta \bar{Y}_{ij})則認為有顯著差異$$
### Application
SD $\uparrow$ ，肌肉的運動模式變得不一致
- ==RF和BF 會趨於不穩定，SD上升==
- 透過SE and CI去分辨是否是具備統計學意義的肌肉疲勞與補償
$$\mu_x = \frac{1}{n} \sum_{i=1}^{n} x_i$$
$$SE_x = \frac{SD_x}{\sqrt{n}}$$, but n should be a constant
$$CI_x = \mu_x \pm t_{\alpha/2} \cdot SE_x$$
用來判斷處於CI的範圍內，才合理
- 用tukey判斷同一個體各時間段落是否出現顯著差異
- 使用ANOVA：速度與持續時間
	- 步行速度 (mph): 1.8, 3.6, 5.4
	- 持續時間 (分鐘): 10, 20

---
# Stablility analysis
### Multiscale Entropy, MSE
https://physionet.org/files/mse/1.0/tutorial/tutorial.pdf
不同步行強度下脛前肌和腓腸肌的肌電圖訊號複雜度變化
粗粒化，用平均
$$y_j(\tau) = \frac{1}{\tau} \sum_{i = (j-1)\tau + 1}^{j\tau} x_i \quad \text{for} \quad 1 \leq j \leq \frac{N}{\tau}$$

Sample Entropy (SE)
$$SE(m, \gamma, \tau) = -\log\left(\frac{A_{\tau}}{B_{\tau}}\right)$$
$$CI(Complexity\ Index) = \sum_{i=1}^{\tau_{\text{max}}} SE(i)$$

### Movement angles
![[Movement angles of 3 participants.png|500]]

---
# Connection with Exoskeleton