$EMG_{FT}$
# Frequency analysis
### Median Frequency
[[Effects of various walking intensities on leg muscle fatigue and plantar pressure distributions.pdf]]
$$Z_{xx}(f,t) = \mathcal{F} \left\{ x(t) w(t - \tau) \right\}$$
$$P(f,t) = |Z_{xx}(f,t)|^2
$$
$$\text{Median Frequency} = \text{median} \left( P(f,t) \right)
$$

---

- ref. 
	- Characterization of muscle fatigue in the lower limb by sEMG and angular position using the WFD protocol [1]
	- Effects of Walking Intensity on Leg Muscle Fatigue and Plantar Pressure [[s12891-021-04705-8.pdf]] [2]
	- [[Muscle Fatigue Analysis Using OpenSim.pdf]]
- 出力振幅降到20%，但沒有提到時間區段的問題 [1]
- 關節角度 [1]
- 中位頻率 [2] 可以用頻率成份去理解這些肌肉活動
	- [x] 視野一個是只有穩態，一個是整個行走階段，所得到的中位頻率振幅不一樣？不會
- 樣本謪