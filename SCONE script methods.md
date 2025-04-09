以下是你整理的 SCONE 模擬器中 Lua 腳本支援的主要類別與方法概要，依用途分類如下：

---

### 🔹 **LuaModel**

**用途：** 全域模型控制與資訊存取（如 COM、時間、參數、自訂值）

|函數|說明|
|---|---|
|`time()`, `delta_time()`, `max_duration()`|時間資訊|
|`com_pos()`, `com_vel()`|模型 COM 位置與速度|
|`mass()`|模型質量|
|`gravity()` / `set_gravity()`|重力設定|
|`actuator(index)`, `find_actuator(name)`|取得 Actuator|
|`dof(index)`, `find_dof(name)`|取得 DOF|
|`muscle(index)`, `find_muscle(name)`|取得 Muscle|
|`body(index)`, `find_body(name)`|取得 Body|
|`joint(index)`, `find_joint(name)`|取得 Joint|
|`get_custom_value(name)`, `set_custom_value(name, value)`|自定義值|
|各種 `create_*_sensor()`|建立延遲感測器|
|各種 `find_*_delay()`|查詢神經延遲參數|

---

### 🔹 **LuaBody**

**用途：控制個別剛體的力學參數**

|函數|說明|
|---|---|
|`mass()`, `inertia_diagonal()`|質量與轉動慣量|
|`com_pos()`, `com_vel()`, `com_acc()`|質心資訊|
|`ang_pos()`, `ang_vel()`, `ang_acc()`|角度資訊|
|`contact_force()`, `contact_moment()`|接觸力與力矩|
|`add_external_force(x,y,z)`|加外力|
|`add_external_moment(x,y,z)`|加外力矩|
|`set_com_pos()`, `set_ori()` 等|設定狀態|

---

### 🔹 **LuaActuator**

**用途：操作致動器（通常是肌肉或關節的動力來源）**

|函數|說明|
|---|---|
|`input()` / `add_input(value)`|設定輸入值（歸一化）|
|`min_input()`, `max_input()`|輸入範圍查詢|

---

### 🔹 **LuaDof**

**用途：操作自由度（DOF）與其動作參數**

|函數|說明|
|---|---|
|`position()`, `velocity()`|當前位置與速度|
|`add_input()`|控制 DOF|
|`muscle_moment()`|肌肉造成的轉矩|
|`create_delayed_*_sensor()`|建立延遲感測器|

---

### 🔹 **LuaMuscle**

**用途：查詢與控制肌肉的物理與動作屬性**

|函數|說明|
|---|---|
|`excitation()`, `activation()`|激發與活化程度|
|`fiber_length()`, `fiber_velocity()`|肌纖維長度與速度|
|`force()`, `normalized_force()`|肌肉力量|
|`moment_arm(dof)`|對特定 DOF 的轉矩臂|
|`create_delayed_*_sensor()`|建立延遲感測器|

---

### 🔹 **LuaJoint**

**用途：操作關節與馬達控制**

|函數|說明|
|---|---|
|`reaction_force()`, `limit_torque()`|關節受力|
|`set_motor_target_ori()`, `add_motor_torque()`|控制馬達|

---

### 🔹 **LuaSensor / LuaDelayedSensor**

**用途：建立與存取延遲感測器值**

|函數|說明|
|---|---|
|`value(delay)`|取得延遲的數值（通常是肌肉、速度等）|

---

### 🔹 **LuaParams**

**用途：參數優化與存取**

|函數|說明|
|---|---|
|`create_from_mean_std()`|建立參數|
|`get(name)`|取得參數值|

---

## 🔍 建議深入探索方向

若你要進行更高階的控制器或優化器開發，可深入研究以下幾個面向：

### ✅ **1. 延遲感測與神經延遲模擬**

- 了解如何利用 `LuaDelayedSensor`, `find_two_way_neural_delay()` 模擬真實神經控制延遲

### ✅ **2. 馬達控制（Joint Motor）**

- 使用 `set_motor_target_ori()` 搭配 `set_motor_stiffness()`、`set_motor_damping()` 建構穩定控制器

### ✅ **3. 自定義參數調整與優化**

- `LuaParams` 可用於建立可調參數（for optimization），支援 mean/stdev/min/max 設定
    
### ✅ **4. 自訂資料共享**

- 利用 `set_custom_value()` 與 `get_custom_value()` 進行跨 Lua 腳本資料傳遞
    

---

如果你之後希望我幫你製作「SCONE Lua 快速語法對照表」或「實作範例腳本」，也可以跟我說，我可以做成一份簡潔文件供你參考。需要嗎？


---
控制範例
```
 
function init( model, par )
	-- get the 'target_body' parameter from ScriptController, or set to "pelvis"
	-- target_body = model:find_body( scone.target_body or "pelvis" )
	calcn_r = model:find_body( "calcn_r" )
	calcn_l = model:find_body( "calcn_l" )

	-- target_actuator = model:find_actuator("motor_act")
	-- target_actuator = model:find_dof("knee_angle_r")
	
	-- hamstrings_r

	
	-- target_actuator = model:find_actuator(scone.target_act)
	target_actuator = model:find_dof(scone.target_act)
	-- target_actuator = model:find_dof("knee_angle_r")
	scone.debug("scone.target_act : " .. scone.target_act)
	scone.debug("target_actuator : " .. tostring(target_actuator))

	scone.debug("\nActuators:")
	for i = 1, model:actuator_count(), 1 do
		scone.debug(model:actuator(i):name())
	end
		
	peak_time = par:create_from_string( "peak_time", scone.peak_time )
	rise_time = par:create_from_string( "rise_time", scone.rise_time )
	duration_time = par:create_from_string( "duration_time", scone.duration_time )
	fall_time = par:create_from_string( "fall_time", scone.fall_time )
	peak_torque = par:create_from_string( "peak_torque", scone.peak_torque )
 
	-- initialize global variables that keep track of the device state
	device_startxxx = 0
	device_end = peak_time + duration_time + fall_time
	device_moment = 0
end
 
function update( model )
	

	local t = model:time() - device_startxxx

	if (t < 0) then
		device_startxxx = 0
		t = model:time() - device_startxxx
	end
	
	if t < peak_time - rise_time then
		device_moment = 0
	elseif (peak_time - rise_time <= t and t < peak_time) then
		device_moment = (peak_torque / 2) * (1 - math.cos(math.pi * ((t - (peak_time - rise_time))/rise_time)))
	elseif (peak_time <= t and t < peak_time + duration_time) then
		device_moment = peak_torque
	elseif ((peak_time + duration_time) <= t and t < (peak_time + duration_time + fall_time)) then
		device_moment = (peak_torque / 2) * (1 + math.cos(math.pi * ((t - (peak_time + duration_time))/fall_time)))
	elseif (peak_time + duration_time + fall_time) <= t then
		device_moment = 0
	end

	-- scone.debug( 
	-- 	model:time() - device_startxxx .. " , " .. model:time() .. " , " .. device_startxxx .. " , " .. tostring(calcn_l:contact_force().y) .. " , " .. tostring(calcn_r:contact_force().y))

	-- scone.debug( 
	-- 	t .. " , " .. device_end .. " , " .. model:time() .. " , " .. device_startxxx .. " , " .. tostring(calcn_l:contact_force().y) .. " , " .. tostring(calcn_r:contact_force().y))

	target_actuator:add_input( 1.0 * device_moment )
	scone.debug("scone.target_act : " .. scone.target_act .. " , actuator_input: " .. target_actuator:input() .. " , " .. device_moment)
	if (calcn_r:contact_force().y - calcn_l:contact_force().y > 0) and (t > device_end) then
		device_startxxx = model:time()
		-- scone.debug("device_start: " .. device_startxxx)
		-- scone.debug(" .................................................. ")
		device_end = peak_time + duration_time + fall_time
	end
	-- return false to keep going
	return false;
end

```