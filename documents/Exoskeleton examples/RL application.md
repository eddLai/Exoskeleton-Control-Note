## 專有名詞
flexion and extension, row and yoll, DOF, Hip locomotion, data-driven,optimal adaptive control, HITL開發流程：用來撰寫正式文章
漂亮的圖：
![[Pasted image 20240107180700.png| 300]]
![[Pasted image 20240107180743.png|300]]

---
## Auto-encoder
[[AutoEncoder-based_Safe_Reinforcement_Learning_for_Power_Augmentation_in_a_Lower-limb_Exoskeleton.pdf]]
在這項研究中，自編碼器（AutoEncoder, AE）被用於軌跡預測，具體方法如下：

1. **資料輸入與降維**：首先，高維度的數據（例如不同關節的角度和慣性測量單元（IMU）的角度）被輸入到AE中。AE的編碼器（Encoder）部分負責將這些高維數據轉換到一個更小的潛在空間，從而實現數據的降維。

2. **潛在空間優化**：在獲得降維後的數據（潛在參數）之後，利用強化學習（RL）算法進行進一步的優化。在這個較小的潛在空間中進行RL可以加快學習速度並提高安全性。

3. **數據重建**：一旦找到最優化的潛在參數，AE的解碼器（Decoder）部分會將這些參數轉換回原始數據空間，從而產生預測的軌跡。這個重建的過程確保了輸出數據（例如預測的角度）與原始輸入數據相符合。

4. **實際應用**：在軌跡預測的具體應用中，例如在下肢外骨骼的動力增強中，這些預測的軌跡被用於指導外骨骼的運動，從而實現與人類用戶同步的運動控制。

通過這種方法，AE能夠有效地處理和分析大量複雜的高維度數據，並將其轉換為實用的輸出，這對於複雜系統的控制和預測來說是非常有價值的。這種結合了AE和RL的方法特別適合於動力學系統的建模和控制，尤其是在需要實時、安全和有效地預測和回應的應用場景中[page 2,3](https://myaidrive.com/?r=c#/home?folder=&file=AutoEncoder-based_Safe_Reinforcement_Learning_for_Power_Augmentation_in_a_Lower-limb_Exoskeleton.pdf&pdfPage=2)。

- 使用GPR統計方法進行資料增強
- $PI^2 -CMA$：高維度連續學習空間，解決稀疏、大量的問題
- SAC
- HIL

用一雙假腿來做測試
能夠軌跡預測，但我要怎麼進行力量增強?
機器學習訓練了一套此人最佳狀況下的行走步態，而能夠在沒力的時候提供力量的增強?
在平穩階段給予更多的力量?
強化學習對肌力偵測用於自適應算法
為什麼需要強化學習，是因為人體何時該增強力道難以定義

---
## DMP-Based Motion Generation
[[DMP-Based_Motion_Generation_for_a_Walking_Exoskeleton_Robot_Using_Reinforcement_Learning.pdf]]
- Linear Inverted Pendulum Model, LIPM：Zero-Moment Point, ZMP、Center of Pressure, CoP
DMPs：
1. 基本框架：
DMPs的核心思想是将任何复杂的运动分解为可调节的稳定动力学系统。这通常涉及以下两个主要组成部分：
- **吸引子动力学**：描述运动的目标状态或最终位置。
- **非线性函数**：调节从起始状态到目标状态的路径。
2. 数学表示：
假设运动轨迹由函数 **f(x)** 表示，DMPs可以表示为以下形式的动力学系统：
- **目标吸引子方程**：
 $$\ddot{y} = \alpha_z(\beta_z(g - y) - \dot{y}) + f(x)$$
  
  其中：，
  - $g$  是目标位置，
  - $\alpha_z 和 \beta_z$ 是预定义的正常数，用于确保系统的收敛性，
  - $f(x)$ 是非线性函数，用于调节运动轨迹。

- **非线性函数**：
  $f(x) = \frac{\sum_{i=1}^{N} \psi_i(x)w_i}{\sum_{i=1}^{N} \psi_i(x)}x(g - y_0)$

  其中：
  - $w_i$ 可學習權重
  - $\psi_i(x)$ 是基于径向基函数（Radial Basis Function, RBF）的加权因子，
  - $x$ 是规范化的时间变量，通常由一个附加的线性系统控制，例如 $\dot{x} = -\alpha_xx$，以保证 $x$ 从1衰减到0。
>[!NOTE] 可用於引用，符合我們的猜想
>"each of the two ankle joints is passive to generate the balance"

---
## RL with dynamic sys.
[[Reinforcement Learning Based Adaptive Walking.pdf]]
RL使用傳統ML方法實現