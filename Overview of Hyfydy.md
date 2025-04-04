---
bg: "[[NTKLab_white bg.png]]"
---
<style>
    .reveal {
        font-family: 'Times New Roman', '標楷體';
        font-size: 30px;
        text-align: left;
        color: black;
        background-size: cover;
        background-position: center;
    }
	.reveal h1,
	.reveal h2,
	.reveal h3,
	.reveal h4,
	.reveal h5,
	.reveal h6 {
	  font-family: 'Times New Roman', '標楷體';
	  color: black;
	  %%text-transform: lowercase%%;
	  text-transform: capitalize;
	}
	.with-border{
		border: 1px solid red;
	}
</style>
<grid drag="60 10" drop="-3 40">
HyFyDy simulation engine
<!-- element style="font-size: 35px;align: left; text-align: left;color: white"-->
</grid>

<grid drag="50 10" drop="40 70">
賴宏達
<!-- element style="font-size: 30px;align: right; text-align: right"-->
</grid>

<!-- slide bg="../NTKLab_white bg_cover_resize.png"-->

---
# Idea
一個檔案HyFyDy.scone檔案只能有一個model(來自.hfd)
- 可以動態調整contact嗎(有開端口嗎)
- Gym裡頭可以調用兩個物件嗎
- 在現有環境已入控制器權重

```
model {
    name = my_model 
    body {
        name = my_body
        mass = 3
        inertia = [ 1.5 1.5 1.5 ]
        pos = [ 0 1 0 ] # single-line comment
    }
    /* multi line
    comment */
}
```

---
# Data Types
`{ key-value a=1 }`, `{ group }`, `[ array ]`

- string: 特定字元需要用`{ }`包住
- vector3: 陣列
- quaternion
- range: `num1..num2` means num1~num2

---
## 什麼是quaternion?
$$q=w+xi+yj+zk$$
$$w = \cos\left(\frac{\theta}{2}\right)$$

$$x = u_x \cdot \sin\left(\frac{\theta}{2}\right)
$$
以此類推
旋轉軸單位向量
$$\vec{u} = \frac{1}{\sin\left(\frac{\theta}{2}\right)} \cdot [x, y, z]$$

---
- $\phi$：繞 X 軸（roll）
- $\theta$：繞 Y 軸（pitch）
- $\psi$：繞 Z 軸（yaw）

$$w = \cos\left(\frac{\phi}{2}\right)\cos\left(\frac{\theta}{2}\right)\cos\left(\frac{\psi}{2}\right) + \sin\left(\frac{\phi}{2}\right)\sin\left(\frac{\theta}{2}\right)\sin\left(\frac{\psi}{2}\right)$$
$$x = \sin\left(\frac{\phi}{2}\right)\cos\left(\frac{\theta}{2}\right)\cos\left(\frac{\psi}{2}\right) - \cos\left(\frac{\phi}{2}\right)\sin\left(\frac{\theta}{2}\right)\sin\left(\frac{\psi}{2}\right)$$
$$y = \cos\left(\frac{\phi}{2}\right)\sin\left(\frac{\theta}{2}\right)\cos\left(\frac{\psi}{2}\right) + \sin\left(\frac{\phi}{2}\right)\cos\left(\frac{\theta}{2}\right)\sin\left(\frac{\psi}{2}\right)$$
$$z = \cos\left(\frac{\phi}{2}\right)\cos\left(\frac{\theta}{2}\right)\sin\left(\frac{\psi}{2}\right) - \sin\left(\frac{\phi}{2}\right)\sin\left(\frac{\theta}{2}\right)\cos\left(\frac{\psi}{2}\right)
$$

```
ori { w = 0.379928 x = -0.596368 y = -0.379928 z = -0.596368 }
ori { w = 0 x = 0 y = 0 z = 0 }
```

---
## modeling
- model 可以直接設定gravity
	- body: basic components in physics, mass properties, position/orientation as well as linear and angular velocity, etc. ==CoM怎麼設定==
	- joint: in a tree relationship with body
	- joint_6dof 專門用於球形結構
	- geometry
	- material 
	- model_options
- Actuators
	- lua script interface來控制行為

---
### Material

| 使用場景     | damping值  | 說明            |
| -------- | --------- | ------------- |
| 硬地面（如鋼鐵） | 1.0 ~ 1.5 | 迅速吸收碰撞能量      |
| 橡膠鞋底     | 0.5 ~ 0.8 | 有彈性但不完全反彈     |
| 軟墊（泡棉）   | 0.6 ~ 1.0 | 避震吸收用，幾乎沒有反彈  |
| 無阻尼（彈簧）  | 0         | 完全彈性碰撞（一般不建議） |

---
### Forces
- joint forces: 
	- `Joint Constraint Forces `$\rightarrow$ `joint_force_pnld`
		- ligaments and cartilage become activate whenever the joint rotates
			- $F_j=-k_pp_j-k_vv_j$
			- $\tau_j = -k_\alpha \theta_j(\alpha_j, \alpha_{\min}, \alpha_{\max}) \left(1 + k_\omega \omega_j \right)$
			- $\theta_j(\alpha_j, \alpha_{\min}, \alpha_{\max}) = \begin{cases}\alpha_j - \alpha_{\min}, & \text{if } \alpha_j < \alpha_{\min} \\\alpha_j - \alpha_{\max}, & \text{if } \alpha_j > \alpha_{\max} \\0, & \text{otherwise}\end{cases}$
		- some displacements
	- `Joint Limit Forces`$\rightarrow$ `joint_force_pd`
		- 速度快 or 阻尼大則越大
		- $\tau_j = -k_\alpha \theta_j(\alpha_j, \alpha_{\min}, \alpha_{\max}) - k_\omega \omega_j$
	- low computation, prefix: `planar_`

---
- contact forces: geometries intersect
	-  _restitution_ and _friction_ 
	- 1.Collision detection 
		- component: only generates contacts, no forces
		- `simple_collision_detection { enable_collision_between_objects = 1 }` otherwise detect only with static body
	- 2.Collision response:
		- Kelvin-Voigt model: $\vec{F}_c = F_n \vec{n} + \vec{F}_t$
			- $F_n = kd - cv_n$
			- $\vec{F}_t = -\frac{\vec{v}_t}{\|\vec{v}_t\|} \cdot \min(\eta \|\vec{v}_t\|, \mu F_n)$
		- contact_force_hunt_crossley: $F_n = kd^{3/2} \left(1 - \frac{3}{2} cv_n \right)$
			- better energy sim
			- Contact Stiffness $k_{hfd} = \left( \frac{4}{3} \sqrt{r}k_{osim} \right)^{2/3}$ transformation
		- contact_force_hunt_crossley_sb
			- `transition_velocity` from static to dynamic friction

---
- actuator forces
	- muscle
		- muscle_force_m2012fast: hill-type, but better. **damping when muscle deactivate**
		- muscle_force_gh2010: activation muscle be kept above a threshold
		- muscle_force_tj2003: force-velocity relationship is poorly defined at low activation and relies heavily on its ad-hoc extrapolation of the force-velocity curve
- external forces.
>hill-type [Flexing Computational Muscle: Modeling and Simulation of Musculotendon Dynamics | J. Biomech Eng. | ASME Digital Collection](https://asmedigitalcollection.asme.org/biomechanical/article-abstract/135/2/021005/371394/Flexing-Computational-Muscle-Modeling-and?redirectedFrom=fulltext)

---
### Integrators
1. linear and angular acceleration
2. force
3. velocity and position/orientation
4. advance in simulation

$${q_{t+h}, \dot{q}_{t+h}} = I_h ({q_{t}, \dot{q}_{t}, \ddot{q}_t , h})$$
step_size h in hyfydy is variable based on accuracy
>How does the system know the accuracy?

---
- `forward_euler_integrator`
- `symplectic_euler_integrator`: 保持保守系統的能量（如震盪系統） 
- `midpoint_euler_integrator`: 提高能量守恆與穩定性, 不適合非常剛性的高頻模擬場景
- `planar_symplectic_euler_integrator`

---

| 項目                       | Hyfydy                                                                 | OpenSim                                                                  |
|----------------------------|------------------------------------------------------------------------|---------------------------------------------------------------------------|
| **關節約束** (Joint constraints) | 透過**力**實現關節約束，可設定剛度與阻尼，允許微小位移                         | 使用**代數約束**強制執行，關節為剛性連接                                     |
| **關節限制** (Joint limits)     | 使用**非線性阻尼力**，根據偏離程度調整限制力                                  | 使用 `CoordinateLimitForce`，超過閾值後採**固定阻尼**                         |
| **摩擦力** (Friction force)     | 使用 `contact_force_hunt_crossley_sb`，**可模擬 OpenSim 行為**                | 有摩擦模型，但與 Hyfydy 的實作略有不同                                      |
| **肌肉力** (Muscle force)       | 採用**優化版 Millard 模型**，力-長度與力-速度關係使用多項式擬合，阻尼實作不同 | 使用 OpenSim 的原始 Millard 模型                                            |
| **肌肉激活動力學**             | 激活動力學與 OpenSim **實作不同**，在去激活速率等方面可能有差異              | 使用標準激活動力學模型                                                      |
| **數值積分** (Integration)     | 基於**最大誤差**判斷精度，**誤差限制較嚴格**                                  | 使用**加權總和誤差**作為準則                                                 |
| **模擬轉換**                   | 與 OpenSim 模型之間無法**直接轉換**，需經過**優化迭代**                        | 同樣無法直接與 Hyfydy 互轉                                                  |


---
# License
```
================ LICENSE BEGIN ================
Hung-Ta Lai (eddlai.be10@nycu.edu.tw)
National Yang Ming Chiao Tung University
Personal Non-Commercial License (expires 2026-04-09)
2d4e3c3ef3806f7d9e8892ad72587d567f7b2e3c038b9769
e0d6c443c6a0b02635c705ccbf61390a357c980c572e1a4c
================= LICENSE END =================
```

```
================ LICENSE BEGIN ================
Hung-Ta Lai (eddlai.be10@nycu.edu.tw)
National Yang Ming Chiao Tung University
Personal Non-Commercial License (expires 2026-04-09)
3926a0be97c4ba3b3656764cf5d4395b9f5b764c1fb70b19
a350bdd3c53f8077d1df31743f16fa546ccc04acabf51f94
================= LICENSE END =================
```