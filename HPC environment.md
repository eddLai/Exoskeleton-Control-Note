`eddlai.be10@140.113.9.253`
`hMdZTTLRkLao` -> `yylab123`

---
- GNOME or XFCE GUI
	- sudo 權限
	- Docker容器
	- OpenML
	- [x] conda環境(成功使用X11轉發SCONE GUI)，就是下載模組以及設定一些環境變數

需要透過module命令load進已經建設的需要sudo權限安裝程式
運算節點，仰賴SLURM (Simple Linux Utility for Resource Management)管理

`export PATH=$PATH:/home/aa0463/eddlai.be10/.local/bin`
`export PATH=/cm/shared/apps/hpc_sdk/2024_241/Linux_x86_64/24.1/cuda/bin:$PATH`

`rsync -avz --delete D:/depRL/ eddlai.be10@140.113.9.253:~/Downloads/depRL`
`rsync -avz --delete eddlai.be10@140.113.9.253:~/Downloads/depRL/ D:/depRL`

運行SCONE的準備
`sys.path.append("/home/aa0463/eddlai.be10/opt/scone/lib")`
`mamba install -c conda-forge lapack=3.6.1`
`mamba install -c conda-forge libgfortran=3`

Docker是靠Enroot實現的

`srun --partition=trialq --gres=gpu:1 --time=00:30:00 --ntasks=1 --cpus-per-task=20 --pty bash`
`squeue -u eddlai.be10`
`scontrol show job <JOBID>`

---
## HPC torch設定
cuda版本是12.3
```
(test_depRL_gymversion) eddlai.be10@login:~/Downloads$ conda list torch
# packages in environment at /home/aa0463/eddlai.be10/.conda/envs/test_depRL_gymversion:
#
# Name                    Version                   Build  Channel
torch                     2.6.0                    pypi_0    pypi
(test_depRL_gymversion) eddlai.be10@login:~/Downloads$ conda info torch
(test_depRL_gymversion) eddlai.be10@login:~/Downloads$ pip show torch
Name: torch
Version: 2.6.0
Summary: Tensors and Dynamic neural networks in Python with strong GPU acceleration
Home-page: https://pytorch.org/
Author: PyTorch Team
Author-email: packages@pytorch.org
License: BSD-3-Clause
Location: /home/aa0463/eddlai.be10/.conda/envs/test_depRL_gymversion/lib/python3.9/site-packages
Requires: filelock, fsspec, jinja2, networkx, nvidia-cublas-cu12, nvidia-cuda-cupti-cu12, nvidia-cuda-nvrtc-cu12, nvidia-cuda-runtime-cu12, nvidia-cudnn-cu12, nvidia-cufft-cu12, nvidia-curand-cu12, nvidia-cusolver-cu12, nvidia-cusparse-cu12, nvidia-cusparselt-cu12, nvidia-nccl-cu12, nvidia-nvjitlink-cu12, nvidia-nvtx-cu12, sympy, triton, typing-extensions
Required-by: deprl, sconegym
```

`srun --partition=defq --gres=gpu:1 --time=20:00:00 --ntasks=1 --cpus-per-task=20 --pty bash`

---
運算節點吃不到license

H100測試one
```
(base) eddlai.be10@DGX-CN01:~$ sconecmd --hyfydy id
22:38:51 SCONE version 2.4.0.2990
22:38:51 Successfully initialized OpenSim3 version 3.3-2021-01-28
22:38:52 Could not initialize Hyfydy: License key is not supported on this computer (96a0d4bf385e74c2)

Hardware ID: 96a0d4bf385e74c2
```

```
(base) eddlai.be10@DGX-CN01:~$ sconecmd --hyfydy id
22:42:28 SCONE version 2.4.0.2990
22:42:28 Successfully initialized OpenSim3 version 3.3-2021-01-28
22:42:28 Could not initialize Hyfydy: License key is not supported on this computer (96a0d4bf385e74c2)

Hardware ID: 96a0d4bf385e74c2
```

```
(base) eddlai.be10@DGX-CN02:~$ sconecmd --hyfydy id
22:43:39 SCONE version 2.4.0.2990
22:43:39 Successfully initialized OpenSim3 version 3.3-2021-01-28
22:43:39 Could not initialize Hyfydy: License key is not supported on this computer (96a0d4bf385e74c2)

Hardware ID: 96a0d4bf385e74c2
(base) eddlai.be10@DGX-CN02:~$ 
```

```
(base) eddlai.be10@login:~$ sconecmd --hyfydy id
22:48:10 SCONE version 2.4.0.2990
22:48:10 Successfully initialized OpenSim3 version 3.3-2021-01-28
22:48:10 Could not initialize Hyfydy: License key has expired (2025-03-06)

Hardware ID: 8e6056df55deaa82
```

---
## setup
```
export PATH=$PATH:/home/aa0463/eddlai.be10/.local/bin
export LD_LIBRARY_PATH=/home/aa0463/eddlai.be10/.conda/envs/simulation/lib:$LD_>
export PATH=$PATH:/home/aa0463/eddlai.be10/opt/scone/bin
export LD_LIBRARY_PATH=$CONDA_PREFIX/lib:$LD_LIBRARY_PATH
export QT_QPA_PLATFORM_PLUGIN_PATH=$CONDA_PREFIX/plugins/platforms
export QT_PLUGIN_PATH=$CONDA_PREFIX/lib/qt/plugins/platforms
export QT_QPA_PLATFORM_PLUGIN_PATH=$CONDA_PREFIX/lib/qt/plugins/platforms
export DISPLAY=localhost:10.0
# 修復 OpenGL 錯誤的環境變數
export LD_LIBRARY_PATH=/usr/lib/x86_64-linux-gnu:$LD_LIBRARY_PATH
export PATH=$CONDA_PREFIX/bin:$PATH
export LD_LIBRARY_PATH=$CONDA_PREFIX/lib:$LD_LIBRARY_PATH:wq

```