# IDEA
- ref. 
	- [[Characterization of muscle fatigue in the lower limb.pdf]] [1]
	- [[Effects of various walking intensities on leg muscle fatigue and plantar pressure distributions.pdf]] [2]
	- [[Muscle Fatigue Analysis Using OpenSim.pdf]]
- 電壓振幅降到20%，但沒有提到時間區段的問題 [1]
- 關節角度 [1]
- 中位頻率 [2] 可以用頻率成份去理解這些肌肉活動
	- [x] 視野一個是只有穩態，一個是整個行走階段，所得到的中位頻率振幅不一樣？不會

$EMG_{FT}$
# Fatique
## Factors of fatique
- insufficient blood perfusion of muscle fibers
- depletion of energy sources
- metabolites’ build-up $\rightarrow$ excess hydrogen ions ***"slows down the waveform of an action potential"***

ref. [[Effects of various walking intensities on leg muscle fatigue and plantar pressure distributions.pdf]]
>***Synchronization of the motor unit pool leads to an increase in amplitude and an increase in the duration of the activation of the EMG signal***

統一的結論：頻率降低，但是振幅提升（因為同步性）
![[RF muscle amplitude in different level of faitque.png|400]]
隨著phase的不同，股直肌過度用力（恢復機制），為了繼續產生運動並協助在疲勞階段進行代償的肌肉

ref. [[Characterization of muscle fatigue in the lower limb.pdf]]
用了很棒的統計方法在嘗試解決這種不直觀的數據。
步行速度的增加，脛前肌的肌電圖中值頻率會顯著下降
![[different muscles when fatigue.png||600]]
1. RF（股直肌）疲乏中期會下降，後期代償會增加
2. BF（股二頭肌）肌肉都會增加
3. TA 疲乏初期也會下降
4. GL 中期較大

系統需要能夠理解代償，或者要想辦法fit回去

---
# Frequency analysis
### Median Frequency
[[Effects of various walking intensities on leg muscle fatigue and plantar pressure distributions.pdf]]
$$Z_{xx}(f,t) = \mathcal{F} \left\{ x(t) w(t - \tau) \right\}$$
$$P(f,t) = |Z_{xx}(f,t)|^2
$$
$$\text{Median Frequency} = \text{median} \left( P(f,t) \right)
$$

---
# Stablility analysis
### Multiscale Entropy, MSE

