https://oshwhub.com/wwwwyt/yi-zhong-di-gong-hao-bian-yuan-j
https://github.com/leapmotion/ProjectNorthStar
`git clone https://github.com/leapmotion/ProjectNorthStar.git ~/Desktop/ProjectNorthStar`
https://gitcode.net/EricLee/handpose_x
[Project North Star: Exploring Augmented Reality (youtube.com)](https://www.youtube.com/watch?v=7m6J8W6Ib4w)
[[other AR products]]

---
# AR SDK
舉Android and IOS為例的手機端可以使用 $Vuforia$ 環境完成這個架設
Frame Marker：
 - Frame Marker 通常是簡單的黑白圖案，可被 Vuforia 引擎快速識別和追蹤
 - **追蹤和識別**：當相機檢測到Frame Marker時，Vuforia SDK利用預先定義的標記模式進行追蹤和識別。
- **定位增強現實內容**：一旦識別出Frame Marker，應用程序就可以準確地在用戶的視野中覆蓋增強現實內容。這意味著用戶看到的虛擬物體或信息會根據他們與這些標記的相對位置和方向進行調整。

ARCamera：
1. **影像捕捉**：捕捉來自用戶設備相機的實時影像。
2. **場景渲染**：在捕捉的影像上渲染虛擬物體，使之看起來像是存在於真實世界中。
3. **追蹤和定位**：辨識和追蹤影像中的標記或物體，並根據這些信息定位虛擬物體。

Image Target：
1. **識別特定圖像**：選定的圖像（如產品包裝、海報、書籍封面等）被用作觸發 AR 體驗的媒介。
2. **空間定位**：當 `Image Target` 被識別後，AR 應用可以確定虛擬物體在真實世界中的確切位置和方向。
3. **互動增強**：用戶可以通過與 `Image Target` 互動來觸發不同的 AR 體驗和功能。

![[AR種類.png]]
會用到SLAM
![[AR開發工具.png]]
### 軟體處理能力
- 圖像運算：The app can have more than one dataset active simultaneously. Each dataset can have up to 100 images. That is a lot of data the app can process in real-time, which shows how powerful Vuforia can be.
- 物件格式轉換：cloud-based recognition. The Cloud Recognition service provided by Qualcomm enables apps to have over one million Image Targets at the same time.


---
# 物件
開發AR其實跟第一人稱視角的遊戲概念很像，只是移動辨識改成從頭盔感知而已。
Unity using Vuforia can utilize a webcam to detect trackables and even show you how exactly the AR content will be on the trackable without having to deploy
on the device first.

### 專案建立與發佈
File | Build Settings.發布到不同平台
在Unity中，"New Keystore" 指的是一個新的密鑰庫（Keystore），它是用於Android應用程式簽名的一部分。當你開發一個Android懡用程式並準備將其發布到Google Play商店時，你需要對應用程式進行數字簽名。這個簽名過程就需要使用到密鑰庫。
Asset menu in the menu bar, then inside Import package ..., click on custom package.

### 物件設計
在Unity中，"Prefab"（預製體）是一種特殊的遊戲對象，它允許你設計並儲存一個具有特定組件和屬性設定的遊戲對象模板。這樣，你就可以在遊戲或應用程式中多次重複使用這個模板，而無需每次都從頭開始創建。

追踪物件（Trackable）
Vuforia追踪圖像的原理基於尋找圖像中對比鮮明的邊緣位置，並在圖像周圍形成一個邊緣集群。這些邊緣被追踪，並根據儲存在數據集中的位置映射，Vuforia可以判斷追踪物件在現實世界中的相對位置，進而在其上正確渲染3D內容。

2D images animated
Mask shader

vedio passthrough：
optical passthrough：
運動不容易做
AR安全區域，需要跟廠商開虛擬邊界的權限，因為我們都是passthrough

---
[[Unity設定OpenXR]]
配置unity
https://developer.oculus.com/documentation/unity/unity-conf-settings/