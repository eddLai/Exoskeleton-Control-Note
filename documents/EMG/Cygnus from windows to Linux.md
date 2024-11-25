方法：
為了解決穩定性問題
為了在FPGA上運行Cygnus
- 不管內容，把exe檔案在Linux上面跑起來，使用wine
	- 同時了解windows and Linux
- 自己寫一個exe
	- 從GUI code的調用方式研究
	- 把元件拆看研究
- 得到廠商原本的code，編譯成exe版本
	- 反編譯

---
## 怎麼調用.exe以及dll這些不能使用的
- [x] 使用run exe on linux(考量大小問題)：[Can Linux Run .exe Files? How to Use Wine and Run Windows Software on Linux (wikihow.com)](https://www.wikihow.com/Can-Linux-Run-Exe)
	- [x] wine(失敗，需要最高權限的cmd)
	- [x] VM
- [x] 改用純python code，沈恩佑
	- [x] 依賴庫
	- [x] 路徑名稱改用
	- [x] 藍牙driver?解封包而已，直接使用串口通訊以及command輸入