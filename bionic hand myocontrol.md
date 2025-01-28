設計real-time python 工具的時候要使用shared_memory加上`mp.Lock()`，來確保多線程的穩定度
```python
for item in shared_memory_items:
        item.append(Lock())
```