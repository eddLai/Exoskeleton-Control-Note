# Overview
![[Overview of the OpenSim Modeling Framework.png|400]]
![[simple opensim simulation.png|400]]
## Model components
- PhysicalFrame
	- Ground參考座標
	- Body 是具有慣性 (inertia) 的 PhysicalFrame
	- PhysicalOffsetFrame: 指定關節 (Joint) 或約束 (Constraint) 在 Body 上的位置與方向
	- ...
- Joint
- Constraint
- Force
- Actuator
- Controller
- Probe

---
# structure: Objects
- Object class
	- 序列化 (Serialization)：轉成檔案格式進行儲存，反之，反序列化
- Components: 執行計算的元素(rooted directed tree topology)
	- 計算系統：`SimTK::MultibodySystem`進行運算
	- 動態行為計算：解ODE
	- 繼承序列化
>並非所有的components都需要Inputs

---
<div style="background-color: white; padding: 10px;">
<img src="D:\Notes\Exoskeleton-Control-Note\documents\Simulation\opensim\model's System and a State object.png" alt="ID Tool" width="500"/></div>

# State
- Continuous state variables(通常稱為state variable)：來自components的動態方程 e.g.
	- activation
	- fiber-length
- Discrete state variables:  external inputs and controls, an Actuator is overridden
	- 某種作用力的產生
	- 外部信號
- Cache Variables: 提高模擬性能
	- **(realization Stages)** 管理快取變數的有效性。
	- 不同的階段（`Position`、`Velocity`、`Dynamics`、`Acceleration`）定義了快取變數的依賴範圍。
	- stale variables「過期」數據

```C++
// Get as abstract Component.
Component& c = device.updComponent("motor");
// Get as concrete Component.template
auto& a = device.updComponent<CoordinateActuator>("motor");
```

---
# Storage
![[storage structure of opensim.png|400]]

DataTable：為了高效訪問
- 元數據（metadata）的處理
- "獨立列" (**independent column**) 和多列 "依賴列" (**dependent columns**)會是相同資料結構。
DataAdapter： 是一個抽象類別，用於定義讀取和寫入 **DataTable** 的介面。
- FileAdapter：其中一個具體類別

---
# Solver
- 根據模型的數學描述，計算系統的未知數。
- 處理例如逆運動學 (Inverse Kinematics)、動力學、力矩臂等問題。
	- InverseKinematicsSolver：以匹配實驗中測量的標記位置
	- MomentArmSolver
	- Manager (ForwardDynamics Solver)

API使用方法
```C++
StatesTrajectory simulate(const Model& model, const State& initState, double finalTime) {
    StatesTrajectory states;  // 用於存儲狀態軌跡的容器
    SimTK::RungeKuttaMersonIntegrator integrator(model.getSystem());  // 穩定的積分器
    SimTK::TimeStepper ts(model.getSystem(), integrator);  // 設置時間步進器
    ts.initialize(initState);  // 初始化狀態
    ts.setReportAllSignificantStates(true);  // 設定報告所有重要狀態
    integrator.setReturnEveryInternalStep(true);  // 返回所有內部步驟狀態

    // 前向模擬迴圈
    while (ts.getState().getTime() < finalTime) {
        ts.stepTo(finalTime);  // 模擬到最終時間
        states.append(ts.getState());  // 將狀態追加到軌跡中
    }
    return states;  // 返回狀態軌跡
}
```

---
- opensim sample rate
- 創造物件的功能
- 取XML的內容

 [[opensim python API]]