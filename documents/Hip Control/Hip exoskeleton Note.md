Initalization: the same as KneeBO, 以開機初始狀態為0度
>角度偵測是累加的

## 回傳
預設2個RS232 Port，但一個改成留有RX(白色), TX(綠色), VCC, GND，注意VCC如果使用電腦USB不要再接，HIP本身有電供
![[Pasted image 20231012160433.png|200x250]]

回傳頻率：120Hz
9軸IMU圖示：紅色是穿戴前方
![[Pasted image 20231012162726.png|300x200]]

---
## 輸出
>注意：
>- 基本單位是0.01deg
>- Speed表示持續的輸出速度
>- E, F, G模式指令Value設為0比較保險

![[Pasted image 20231012160521.png|200x200 ]]


---

待辦：
- ~~買Blueteeth module，以用matlab等PC端~~ 先用現有的TTL module即可
- Demo code為商業機密已經寫在Micro裡頭，先逆向研究，再做進一步的延伸
- 主要任務：偵測作動，要建立逆電流(福寶)，或者IMU(緯創)回推能判斷走、跑、即可的公式