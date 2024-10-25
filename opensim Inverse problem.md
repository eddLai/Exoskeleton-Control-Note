1. [[Inverse Kinematics]]: "best match" is expressed as a **weighted least-squares** problem
2. Inverse Dynamics: ID -> forces, 解方程by Simbody™
<div style="background-color: white; padding: 10px;">
<img src="D:\Notes\Exoskeleton-Control-Note\documents\Simulation\opensim\Inverse Dynamics (ID) Tool.png" alt="ID Tool" width="300"/></div>

3. [[Static Optimization(SO)]]
	1. 根據特定目標計算每個時間點的最佳肌肉力分佈，但不一定符合生理真實的肌肉激活模式
4. [[Computed Muscle Control]], 無法使用Scripting?
	1. 用途:用來讓muscle逼近輸入的物件座標 `==` 基於追蹤已知運動的「控制」，
	3. 特性:適合較高能量的運動(肌腱動態和彈性儲能，例如跑步)，
	4. 指標:residuals from the CMC
5. EMG-Informed Methods: [[CEINMS app.]]