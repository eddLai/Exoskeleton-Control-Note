有一些依賴項目需要ubuntu 20.04，才有的封包
e.g. [freeglut3_2.8.1-3_amd64.deb](https://ubuntu.pkgs.org/20.04/ubuntu-universe-amd64/freeglut3_2.8.1-3_amd64.deb.html)
### 方法
1. 解決依賴項目的問題
	1. equivs工具
	2. 修改SCONE的 .deb 包
	3. 從源文件編譯舊的工具，但可能會出現相依問題

2. 源文件編譯：depends on OpenSim v3.3 and OpenSceneGraph v3.2.需要gun-8
https://github.com/tgeijten/scone-studio/blob/main/BUILD.md
4. 建立Docker環境