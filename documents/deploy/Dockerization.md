Old dockerfile:
```Docker
docker pull ntklab/spinal_controller

xhost +local:root

docker run -it \
    --name spinal_controller \
    --privileged \
    --env=DISPLAY \
    --env=QT_X11_NO_MITSHM=1 \
    -v /tmp/.X11-unix:/tmp/.X11-unix \
    ntklab/spinal_controller \
    /bin/bash
```

從20.04開始
```
docker run -it ubuntu:20.04 /bin/bash
```

開通GUI共享