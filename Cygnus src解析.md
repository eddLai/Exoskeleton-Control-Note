目標：讓Cygnus可以運行在KV260 arm64 ubuntu
- 使用[[Bottles套Cygnus]]
- 自己寫core.exe的功能：FDTI BT2UART driver到local host（或者直接串接到D4PG env也可以）

ApiCmd -> stream.py
需要靠軟體濾波，最大極值+/- 375mV, DC-131Hz
正常windows版本輸出畫面

[[Consistent Overhead Byte Stuffing(COBS) encoding]]