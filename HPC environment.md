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