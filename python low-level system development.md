# shared_memory
設計real-time python 工具的時候要使用shared_memory加上`mp.Lock()`，來確保多線程的穩定度
```python
for item in shared_memory_items:
        item.append(Lock())
```


- SharedMemoryManager：
	- 對`from multiprocessing.shared_memory import SharedMemory`的進一步封裝
	- 原來python如果要寫多線程需要寫成這樣像C

---
# binary package
`struct`, `pack()` 和 `unpack()`

| **格式 (`fmt`)** | **說明**                                      | **大小**    |
| -------------- | ------------------------------------------- | --------- |
| `'B'`          | 無符號 8-bit (1 byte)                          | `1 byte`  |
| `'H'`          | 無符號 16-bit (2 bytes)                        | `2 bytes` |
| `'I'`          | 無符號 32-bit (4 bytes)                        | `4 bytes` |
| `'6s'`         | 固定長度 6 bytes 字串                             | `6 bytes` |
| `'<BHB'`       | 小端序 (Little Endian)，包含 8-bit, 16-bit, 8-bit | `4 bytes` |
```python
payload = b'\x01\x02\x03\x04'  # 假設有 4 個 bytes 資料
data = struct.pack('4B', 0, len(payload), cls, cmd) + payload
```