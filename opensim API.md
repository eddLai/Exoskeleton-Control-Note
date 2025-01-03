# Basic
![[Overview of the OpenSim Modeling Framework.png|400]]
![[simple opensim simulation.png|400]]

# Objects
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
![[storage structure of opensim.png|400]]


---
- opensim sample rate
- 創造物件的功能
- 取XML的內容

 [[opensim python API]]