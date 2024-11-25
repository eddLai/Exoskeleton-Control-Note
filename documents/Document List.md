```bash
tree -P '*.pdf' --noreport | sed -E 's/(├──|└──) (.*\.pdf)/\1 [[\2]]/'
```
.
├── documents
│   ├── AR
│   ├── conference
│   │   ├── Exo conference endnote
│   │   │   └── My EndNote Library.Data
│   │   │       └── sdb
│   │   ├── [[GCBME 2024 Abstract_Exoskeleton_final.pdf]]
│   │   ├── [[ICMST 2024 Abstract_Exoskeleton_v4.pdf]]
│   │   ├── [[ICMST 2024 Abstract_Exoskeleton_賴宏達,沈恩佑,劉芸婷v2.pdf]]
│   │   ├── [[ICMST 2024 Abstract_Exoskeleton_賴宏達,沈恩佑,劉芸婷v3.pdf]]
│   │   └── [[論文蒐集同意書_中文版_賴宏達.pdf]]
│   ├── deploy
│   ├── #Dynamics_Model
│   │   ├── [[Adaptive Synergetic Motion Control for Rehabilitation.pdf]]
│   │   ├── [[effect on healthcare-10-01291-v2.pdf]]
│   │   ├── [[Hierarchical_Interactive_Learning_for_a_HUman-Powered_Augmentation_Lower_EXoskeleton.pdf]]
│   │   ├── [[Optimal Task-Invariant Energetic Control for a Knee-Ankle exoskeleton.pdf]]
│   │   ├── Papers
│   │   │   ├── [[Admittance_Control_Based_Human-in-the-Loop_Optimization_for_Hip_Exoskeleton_Reduces_Human_Exertion_during_Walking.pdf]]
│   │   │   └── [[Design and Control of a Powered Hip.pdf]]
│   │   ├── [[Precision Interaction Force Control of an Underactuated Hydraulic Stance Leg Exoskeleton Considering the Constraint from the Wearer.pdf]]
│   │   └── [[Robust walking control of a lower limb rehabilitation exoskeleton coupled with a musculoskeletal model via deep reinforcement learning.pdf]]
│   ├── #EMG
│   │   └── paper
│   │       ├── [[a-model-free-deep-reinforcement-learning-approach-for-control-of-exoskeleton-gait-patterns.pdf]]
│   │       ├── [[applsci-13-12609.pdf]]
│   │       ├── [[DDPG-based controlling algorithm for upper limb prosthetic shoulder joint.pdf]]
│   │       ├── [[Deep_Reinforcement_Learning_for_EMG-based_Control_of_Assistance_Level_in_Upper-limb_Exoskeletons.pdf]]
│   │       ├── [[Designing_Deep_Reinforcement_Learning_Systems_for_Musculoskeletal_Modeling_and_Locomotion_Analysis_Using_Wearable_Sensor_Feedback.pdf]]
│   │       ├── [[Development and Evaluation of a Hip Exoskeleton for Lateral Resistance Walk Exercise.pdf]]
│   │       ├── [[End-to-End_Deep_Reinforcement_Learning_for_Exoskeleton_Control.pdf]]
│   │       ├── [[fnbot-17-1186175 (1).pdf]]
│   │       ├── [[Geyer&Herr-ReflexModel2Column (1).pdf]]
│   │       ├── [[ML EMG muscle estimation.pdf]]
│   │       └── [[Review of electromyography onset detection methods for real-time control of robotic exoskeletons.pdf]]
│   ├── #Exoskeleton examples
│   │   ├── [[Deep Reinforcement Learning in Unity With Unity ML Toolkit (Abhilash Majumder) (Z-Library).pdf]]
│   │   ├── [[DMPs tutorial.pdf]]
│   │   └── Papers
│   │       ├── [[A_Data-Driven_Reinforcement_Learning_Solution_Framework_for_Optimal_and_Adaptive_Personalization_of_a_Hip_Exoskeleton.pdf]]
│   │       ├── [[AutoEncoder-based_Safe_Reinforcement_Learning_for_Power_Augmentation_in_a_Lower-limb_Exoskeleton.pdf]]
│   │       ├── [[DDPGbasedcontrollingalgorithmforupperlimbprostheticshoulderjoint.pdf]]
│   │       ├── [[DMP-Based_Motion_Generation_for_a_Walking_Exoskeleton_Robot_Using_Reinforcement_Learning.pdf]]
│   │       ├── [[Experiment-free exoskeleton assistance via learning in simulation.pdf]]
│   │       ├── [[Human–exoskeleton interaction portrait.pdf]]
│   │       ├── [[Lower Limb Exoskeleton LSTM.pdf]]
│   │       ├── [[Model-free based neural network control with time-delay estimation.pdf]]
│   │       ├── [[musculoskeletal model via deep.pdf]]
│   │       ├── [[Real-Time_NN_Gait_Phase_Estimation_Using_a_Robotic_Hip_Exoskeleton.pdf]]
│   │       ├── [[Reinforcement Learning Based Adaptive Walking.pdf]]
│   │       └── [[Supplimentary_Experiment-free exoskeleton assistance via learning in simulation - 41586_2024_7382_MOESM1_ESM.pdf]]
│   ├── #Hardware
│   │   ├── [[AMD Kria K24 SOM Product Overview Deck.pdf]]
│   │   └── [[Xilinx Kria Series.pdf]]
│   ├── Hip Control
│   ├── KneeBO Contol
│   ├── Plan Graphs
│   ├── #RL
│   │   ├── books
│   │   │   ├── [[Book all-in-one.pdf]]
│   │   │   ├── [[Deep Reinforcement Learning Hands-On Apply modern RL.pdf]]
│   │   │   ├── [[Deep Reinforcement Learning in Unity_ With Unity ML Toolkit -- Abhilash Majumder (auth.) -- 1st ed., 2021.pdf]]
│   │   │   ├── [[The Art of Reinforcement Learning (Michael Hu) (Z-Library).pdf]]
│   │   │   ├── [[Visual Reinforcement Learning with Imagined Goals.pdf]]
│   │   │   └── [[深度强化学习实践(原书第2版) (：(俄罗斯)马克西姆·拉潘(Maxim Lapan)) (Z-Library).pdf]]
│   │   └── Papers
│   │       ├── [[A Distributional Perspective on Reinforcement Learning.pdf]]
│   │       ├── [[Combining Improvements in Deep Reinforcement Learning.pdf]]
│   │       ├── [[Deterministic Policy Gradient Algorithms.pdf]]
│   │       ├── [[DISTRIBUTED DISTRIBUTIONAL DETERMINISTIC.pdf]]
│   │       ├── [[RL curiosity.pdf]]
│   │       └── [[Skew_Fit_State_Covering_Self_Supervised1903.03698.pdf]]
│   ├── #Simulation
│   │   └── papers
│   │       ├── [[A Muscle-Reflex Model that Encodes Principles of.pdf]]
│   │       ├── [[A neuromuscular model of human locomotion combines spinal reflex circuits with voluntary movements.pdf]]
│   │       ├── [[CEINMS a toolbox to investigate the influence of different neural control solutions on the prediction of muscle excitation and joint moments during dynamic motor tasks.pdf]]
│   │       ├── [[Motor Control Programs and walking.pdf]]
│   │       └── [[Muscle-controlled physics simulations of bird locomotion resolve the grounded running paradox.pdf]]
│   ├── [[大茂-運動型外骨骼-SBIR計畫書_20230630_final.pdf]]
│   └── 計劃書
│       ├── 圖片
│       ├── 引用
│       │   ├── Dynamic Model_e
│       │   ├── EMG_e
│       │   ├── ML_App_e
│       │   ├── [[nodemcu-32s_product_specification.pdf]]
│       │   └── RL_end
│       ├── 影片
│       ├── [[旺宏作品摘要 exoskeleton組v1.pdf]]
│       ├── [[旺宏作品計劃書exoskeletonv0.4組.pdf]]
│       ├── [[旺宏作品計劃書exoskeleton組.pdf]]
│       ├── [[旺宏作品計劃書exoskeleton組v0.1.pdf]]
│       ├── [[旺宏作品計劃書exoskeleton組v0.3.pdf]]
│       ├── [[旺宏作品計劃書exoskeleton組v0.pdf]]
│       ├── [[旺宏作品計劃書exoskeleton組v1.0.pdf]]
│       ├── [[旺宏作品計劃書exoskeleton組v1.1.pdf]]
│       ├── [[旺宏作品計劃書 外骨骼v1.1.pdf]]
│       ├── [[附件1_source code_旺宏作品計劃書exoskeleton組 (2).pdf]]
│       ├── [[附件1_source code_旺宏作品計劃書exoskeleton組.pdf]]
│       ├── [[附件1_外骨骼系統源代碼v2.pdf]]
│       └── [[附件2_示範影片.pdf]]
├── Plan
├── Slide pics
└── 賴宏達SS_final_report
    ├── [[SS_期末專題slide.pdf]]
    ├── [[計劃書exoskeleton組v1.1.pdf]]
    └── [[附件1_外骨骼系統源代碼v2.pdf]]

---
### 相似的架構：Note from phase I
- [[Reinforcement Learning Based Adaptive Walking.pdf]]：dynamics
- [[Lower Limb Exoskeleton LSTM.pdf]]：DL for trajectory prediction
- [[AutoEncoder-based_Safe_Reinforcement_Learning_for_Power_Augmentation_in_a_Lower-limb_Exoskeleton.pdf]]: dim descending
- [[DMP-Based_Motion_Generation_for_a_Walking_Exoskeleton_Robot_Using_Reinforcement_Learning.pdf]]：LIPM用來生成指定動作，而**DMP則為軌跡到關節角度的過程優化**，透過跌代標準g是基於目標動作進行優化的
- [[A_Data-Driven_Reinforcement_Learning_Solution_Framework_for_Optimal_and_Adaptive_Personalization_of_a_Hip_Exoskeleton.pdf]]：幾乎相同的研究，但是僅僅使用RL在資料收集方面使用PI2-CMA進行梯度計算
- [[Admittance_Control_Based_Human-in-the-Loop_Optimization_for_Hip_Exoskeleton_Reduces_Human_Exertion_during_Walking.pdf]]：蠻特別內容，使用RL做力矩模式轉換，來解決需要用RL跑連續動作輸出的狀況，但我們應該暫時不用力矩，先跑角度預測就好。
- [[ML EMG muscle estimation.pdf]]：使用ML SVM, SVR-GA(最佳), RL進行肌力使用預測。從預處理到ML方法的詳盡說明以及比較。

---
