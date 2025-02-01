[LibEMG — libemg 1.0.0 documentation](https://libemg.github.io/libemg/index.html)
https://github.com/NiklasRosenstein/myo-python/releases/tag/v1.0.4
計畫：
- 搞懂基礎連線
- 建立資料紀錄系統
- 使用classifier
- 客製化GUI流程

---
- [[python low-level system development]]
- [[Myo Armband command]]

---
BT 類裡使用了 threading.Lock 來保護對 serial 物件的存取，但鎖只能確保同一時間只有一個線程進行讀寫操作，並會導致線程堵塞
使用`fig.canvas.mpl_connect('key_press_event', on_key_press)`來解決有圖表情況下的鍵盤操作

git submodule add "https://github.com/LibEMG/libemg.git" libemg