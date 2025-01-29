計畫：
- 搞懂基礎連線
- 建立資料紀錄系統
- 使用classifier
- 客製化GUI流程

---
- [[Myo Armband command]]

---
設計real-time python 工具的時候要使用shared_memory加上`mp.Lock()`，來確保多線程的穩定度
```python
for item in shared_memory_items:
        item.append(Lock())
```


- SharedMemoryManager：
	- 對`from multiprocessing.shared_memory import SharedMemory`的進一步封裝
	- 原來python如果要寫多線程需要寫成這樣像C