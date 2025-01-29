https://blog.csdn.net/weixin_44300062/article/details/140690981
確保接收方可以重建數據
Overhead: 將`0x00`替換成非零值，例如：結束字符, 轉譯字符
消除偵標記？
Stuffing: 對數據包進行轉換
將 [0,255] 變為 [1,255] 
轉換後加上0字節
有效負載？data package中的有意義資料
![[COBS data package.png]]