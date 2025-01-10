training file
settings file
desired algorithm, environment, number of training iterations

## Terms
- Differential Extrinsic Plasticity, DEP：自組織並產生連貫的行為
- evolutionary priors：內建在生物體內的機制或目標

使用RL methods，需要注意：
- 過度驅動系統 (Overactuated Systems): 生物肌肉骨骼系統通常是過度驅動的，即肌肉數量多於自由度。在這種情況下，高效的探索策略是至關重要的。
- 動作空間 (Action Space): 肌肉控制任務的動作空間通常很大，因為需要控制許多單獨的肌肉
- ε-greedy 策略或零均值不相關高斯雜訊不夠用

行走速度、關節疼痛和肌肉努力的獎勵函數