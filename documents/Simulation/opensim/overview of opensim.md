ref.
- [opensim-org/opensim-core: SimTK OpenSim C++ libraries and command-line applications, and Java/Python wrapping.](https://github.com/opensim-org/opensim-core?tab=readme-ov-file)
- [OpenSim Documentation - OpenSim](https://opensimconfluence.atlassian.net/wiki/spaces/OpenSim/overview)
- file example: [opensim-models/Pipelines/Gait2354_Simbody/subject01_Setup_Scale.xml at master · opensim-org/opensim-models](https://github.com/opensim-org/opensim-models/blob/master/Pipelines/Gait2354_Simbody/subject01_Setup_Scale.xml)

# Content
- [[opensim Download]]
- [[opensim data collection and data structure]]
- [[opensim models]]
- [[Overview of opensim's workflow]]
	1. Importing Experimental Data
	2. [[opensim Scaling]]: 現在mocap已經整合了scaling:mass properties (mass and inertia tensor)
	3. [[opensim Inverse problem]]
	4. [[opensim forward problem]]
- [[opensim analysis simulation]]

其實可以用GUI去產生xml，再開始setting
Coordinate controller

---
# Application
- 使用[[gait analysis code from Maurice edd_Note]]

---
# API
![[Overview of the OpenSim Modeling Framework.png|400]]
![[simple opensim simulation.png|400]]
<div style="background-color: white; padding: 10px;">
<img src="D:\Notes\Exoskeleton-Control-Note\documents\Simulation\opensim\model's System and a State object.png" alt="ID Tool" width="500"/></div>

Object class
- 序列化 (Serialization)：轉成檔案格式進行儲存，反之，反序列化
Components: 執行計算的元素
- `SimTK::MultibodySystem`進行運算
- 


- opensim sample rate
- 創造物件的功能
- 取XML的內容

 [[opensim python API]]