<div style="background-color: white; padding: 10px;">
<img src="D:\Notes\Exoskeleton-Control-Note\documents\Simulation\opensim\Inverse Dynamics (ID) Tool.png" alt="ID Tool" width="300"/></div>
<div style="background-color: white; padding: 10px;">
<img src="D:\Notes\Exoskeleton-Control-Note\documents\Simulation\opensim\Inputs and Outputs of the IK Tool.png" alt="ID Tool" width="300"/></div>
==輸出的是.mot==
Units: m, radians
所以如果要用
## Settings:
tips: 
- 優先增加「運動」段標記（例如放置於大腿段的三角架標記）的權重，因為這些標記通常較為穩定，不易受到軟組織位移的影響
- 相對權重 vs 絕對權重

## Process
weighted least squares problem
IK solver可以只依賴marker運算，但也可以提供實驗值
會得到: 
非預設座標的值會變動
$$\min_{\mathbf{q}} \left[
\sum_{i=\text{markers}} w_i \left\| \mathbf{x}_i^{\text{exp}} - \mathbf{x}_i (\mathbf{q}) \right\|^2
+ \sum_{j=\text{unprescribed coords}} \omega_j \left( q_j^{\text{exp}} - q_j \right)^2
\right]$$

## Evaluation
官方建議: 
- Maximum marker error should generally be less than 2-4 cm
- RMS under 2 cm
- similar experiment should within one standard deviation

