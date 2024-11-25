目標：讓Cygnus可以運行在KV260 arm64 ubuntu
- 使用[[Bottles套Cygnus]]
- 自己寫core.exe的功能：FDTI BT2UART driver到local host（或者直接串接到D4PG env也可以）

ApiCmd -> stream.py
需要靠軟體濾波，最大極值+/- 375mV, DC-131Hz
正常windows版本輸出畫面

[[Consistent Overhead Byte Stuffing(COBS) encoding]]

整段commnad排列組合
錄EMG
motion capture 轉成，自己走路的model

sto 格式
EMG做到muscle activation
osim
有gym, or scorne-py but 沒辦法調整步態，沒辦法mimic
所以要改用cma-es
opensim四種評估指數
先有模擬，再把EMG用於校正
offline