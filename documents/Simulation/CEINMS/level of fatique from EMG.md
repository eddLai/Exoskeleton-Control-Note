# IDEA
- ref. 
	- Characterization of muscle fatigue in the lower limb by sEMG and angular position using the WFD protocol [1]
	- [[Effects of various walking intensities on leg muscle fatigue and plantar pressure distributions.pdf]] [2]
	- [[Muscle Fatigue Analysis Using OpenSim.pdf]]
- 電壓振幅降到20%，但沒有提到時間區段的問題 [1]
- 關節角度 [1]
- 中位頻率 [2] 可以用頻率成份去理解這些肌肉活動
	- [x] 視野一個是只有穩態，一個是整個行走階段，所得到的中位頻率振幅不一樣？不會

$EMG_{FT}$
# atique
## Factors of fatique
- insufficient blood perfusion of muscle fibers
- depletion of energy sources
- metabolites’ build-up $\rightarrow$ excess hydrogen ions ***"slows down the waveform of an action potential"***

ref. [[Effects of various walking intensities on leg muscle fatigue and plantar pressure distributions.pdf]]
>***Synchronization of the motor unit pool leads to an increase in amplitude and an increase in the duration of the activation of the EMG signal***

頻率降低，但是振幅提升（因為同步性）


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

