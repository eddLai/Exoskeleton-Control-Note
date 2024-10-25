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
例如: `<socket_parent_frame>/ground</socket_parent_frame>`

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