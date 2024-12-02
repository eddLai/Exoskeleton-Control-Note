# IDEA
- ref. 
	- [[Characterization of muscle fatigue in the lower limb by sEMG and angular position using the WFD protocol.pdf]] [1]
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
==步行速度的增加，脛前肌的肌電圖中值頻率會顯著下降==
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
用來判斷是否合理

---
# Stablility analysis
### Multiscale Entropy, MSE

