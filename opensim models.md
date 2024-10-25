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

語法: `socket_`: indicate the path
例如: `<socket_parent_frame>/ground</socket_parent_frame>`