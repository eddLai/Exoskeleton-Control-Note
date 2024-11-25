2023/09/22 賴宏達
# Goal
解析命令，透過GUI的Button對應的功能，了解收發指令去控制exskeleton's servo motor
1. 先統整出現的CMD(困難在於後面兩個參數)
2. 找到button and label，知道GUI對應的function
3. 解析工作過程，了解如何對程式進行底層操控
4. 自製模式, [[動作設計範例]]Based on 現有高階功能

### Other notes
- [[Raw Funtions]]
- [[COM連線方法 in C]]

---
# Result
輸入命令，以及KneeBO回傳都是靠Com，
但因為KneeBO命令有一定的格式(參見旗下[[Command Table]])，Based on [[KneeBO_CMD]]
[[Record]]則是??
補力??

---
### Parameter
- Level

|Class|Bar|Label|
|---|---|---|
|Flex|5|63|
|Ext|6|61|
|Speed|7|20|
|Force|8|22|
|Times|9|24|
||10|25|
||11|26|
||12|27|
|IMU|13|60|
|step Left|15|67|

- TextBox

---
### GUI
Bottons
- button
	- 1: 
	- 2, 29: Stop
	- 3: Clear TextBox
	- 25
- radioButton
	- 9 isokinetic
	- 10 isotonic
	- 11 isometric

| Condition  | textBox70 | textBox71 | textBox72 | textBox69 | trackBar12 | trackBar11 | trackBar10 | radioButton Pressed |
|------------|---------------------|-----------|-----------|-----------|-----------|------------|------------|------------|
| Isokinetic | 1         | 1         | 1         | 1         | 1          | 0          | 0          |9        |
| Isotonic   | 1         | 1         | 1         | 1         | 0          | 1          | 0          |10       |
| Isometric  | 0         | 0         | 1         | 0         | 0          | 1          | 1          |11       |
- checkBox2: gravity compensation

Displayer
- SelectTab(2): Bars