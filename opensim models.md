
Tasks: 需要建置有手部肌肉的模型，以及外骨骼模型，怎麼從`STL`轉換。
## Components
- reference frames
- bodies
- joints
- constraints
- forces
- contact geometry
- markers
- controllers

rigid bodies interconnected by joints

![[model sys..png]]

XML -> **ModelBuilder.py** -> new model

##### 外部檔案
 `socket_`: indicate the path
例如: 
```XML
<socket_parent_frame>/ground</socket_parent_frame>
```

##### 表示一個Body
```XML
<Body name="r_humerus">
    <attached_geometry>...</attached_geometry>
    <WrapObjectSet>...</WrapObjectSet>
    <mass>1.8645719999999999</mass>
    <mass_center>0 -0.18049599999999999 0</mass_center>
    <inertia>0.01481 0.0045510000000000004 0.013193 0 0 0</inertia>
</Body>
```

#### 使用mesh體
```
<Body>
<attached_geometry>
<Mesh name="base_geom_1">
```

```
<socket_frame>
<input_transform>
<scale_factors> 特殊的x,y,z的scaling
```

```
<Appearance>
<visible>
<opacity>
<color>
<SurfaceProperties> (1:Points, 2:Wire, 3:Shaded)
```

`<mesh_file>bone.vtp</mesh_file>`: `.vtp`、`.stl`、`.obj`

####  XML for a Joint
Frames：
1. **Ground**：每個模型都從一個Ground Frame開始。這是一個固定不動的參考框架。
2. **Body**：剛體的框架，與移動的剛體相關聯。
3. **PhysicalOffsetFrame**：相對於其他物理框架（如 Body）的偏移框架，定義了一個 **固定的變換（constant transform）**，用來描述兩個框架之間的相對位置和方向。

製作joints，需要連接父框架和子框架

