# shared_memory
設計real-time python 工具的時候要使用shared_memory加上`mp.Lock()`，來確保多線程的穩定度
```python
for item in shared_memory_items:
        item.append(Lock())
```


- SharedMemoryManager：
	- 對`from multiprocessing.shared_memory import SharedMemory`的進一步封裝
	- 原來python如果要寫多線程需要寫成這樣像C

# Process
```python
from multiprocessing import Process
class MyoStreamer(Process):
	...
myo = MyoStreamer(...)
myo.start()  # ✅ 呼叫 `Process.start()`
```


---
# binary package
`struct`, `pack()` 和 `unpack()`

|**符號**|**端序 (Endianness)**|**數據對齊方式**|**適用場景**|
|---|---|---|---|
|`<`|**小端序 (Little Endian)**|**無對齊要求**|**適用於 BLE 通訊，常見於 ARM 架構**|
|`>`|**大端序 (Big Endian)**|**無對齊要求**|**適用於網絡協議 (Big-Endian，常見於 TCP/IP)**|
|`!`|**大端序 (Big Endian)**|**標準 C 對齊**|**用於 C 語言互操作**|
|`=`|**當前系統預設端序**|**根據系統決定**|**適用於跨平台應用**|

| **格式 (`fmt`)** | **說明**                                      | **大小**    |
| -------------- | ------------------------------------------- | --------- |
| `'B'`          | 無符號 8-bit (1 byte)                          | `1 byte`  |
| `'H'`          | 無符號 16-bit (2 bytes)                        | `2 bytes` |
| `'I'`          | 無符號 32-bit (4 bytes)                        | `4 bytes` |
| `'6s'`         | 固定長度 6 bytes 字串                             | `6 bytes` |
| `'<BHB'`       | 小端序 (Little Endian)，包含 8-bit, 16-bit, 8-bit | `4 bytes` |
```python
def pack(fmt, *args):
	return struct.pack('<' + fmt, *args)

payload = b'\x01\x02\x03\x04'  # 假設有 4 個 bytes 資料
data = struct.pack('4B', 0, len(payload), cls, cmd) + payload
```
## BLE GATT(Generic Attribute Profile) Protocol

| **類別 (`cls`)** | **用途**                         | 命令 (`cmd`) | 用途                                |
| -------------- | ------------------------------ | ---------- | --------------------------------- |
| `0x00`         | **系統指令 (System Commands)**     |            |                                   |
|                |                                | `0x01`     | **Write Response確認寫入成功**          |
| `0x02`         | **連線指令 (Connection Commands)** |            |                                   |
| `0x03`         | **安全指令 (Security Commands)**   |            |                                   |
| `0x04`         | **屬性 (ATT, Attribute) 操作指令**   | `0x04`     | **Read Attribute Request請求讀取屬性**  |
|                |                                | `0x05`     | **Write Attribute Request請求寫入屬性** |


```python
self.write_attr(0x19, pack('3B', 3, 1, 1))  # 震動模式 1
self.send_command(4, 5, pack('BHB', con, 0x19, 3) + b'\x03\x01\x01')
```

- `multichr`, `multiord` 確保可以將字串轉換成數值 or byte方便後續作為二進制封裝
- `proc_byte`：按照順序讀取封包
- `handler`負責處理預先註冊的函式調用也就是event
- `wait_event(4, 5)` **阻塞，直到收到讀取結果 (cls=4, cmd=5)**。