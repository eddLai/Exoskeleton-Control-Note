```bash
tree -P '*.pdf' --noreport | sed -E 's/(├──|└──) (.*\.pdf)/\1 [[\2]]/'
```
### 相似的架構：Note from phase I
- [[Reinforcement Learning Based Adaptive Walking.pdf]]：dynamics
- [[Lower Limb Exoskeleton LSTM.pdf]]：DL for trajectory prediction
- [[AutoEncoder-based_Safe_Reinforcement_Learning_for_Power_Augmentation_in_a_Lower-limb_Exoskeleton.pdf]]: dim descending
- [[DMP-Based_Motion_Generation_for_a_Walking_Exoskeleton_Robot_Using_Reinforcement_Learning.pdf]]：LIPM用來生成指定動作，而**DMP則為軌跡到關節角度的過程優化**，透過跌代標準g是基於目標動作進行優化的
- [[A_Data-Driven_Reinforcement_Learning_Solution_Framework_for_Optimal_and_Adaptive_Personalization_of_a_Hip_Exoskeleton.pdf]]：幾乎相同的研究，但是僅僅使用RL在資料收集方面使用PI2-CMA進行梯度計算
- [[Admittance_Control_Based_Human-in-the-Loop_Optimization_for_Hip_Exoskeleton_Reduces_Human_Exertion_during_Walking.pdf]]：蠻特別內容，使用RL做力矩模式轉換，來解決需要用RL跑連續動作輸出的狀況，但我們應該暫時不用力矩，先跑角度預測就好。
- [[ML EMG muscle estimation.pdf]]：使用ML SVM, SVR-GA(最佳), RL進行肌力使用預測。從預處理到ML方法的詳盡說明以及比較。

---
