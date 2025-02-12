---
bg: "[[NTKLab_white bg.png]]"
---

<style>
    .reveal {
        font-family: 'Times New Roman', '標楷體';
        font-size: 30px;
        text-align: left;
        color: black;
        background-size: cover;
        background-position: center;
    }
	.reveal h1,
	.reveal h2,
	.reveal h3,
	.reveal h4,
	.reveal h5,
	.reveal h6 {
	  font-family: 'Times New Roman', '標楷體';
	  color: black;
	  %%text-transform: lowercase%%;
	  text-transform: capitalize;
	}
	.with-border{
		border: 1px solid red;
	}
</style>
<grid drag="60 10" drop="-3 40">
level of fatigue from EMG
<!-- element style="font-size: 40px;align: left; text-align: left;color: white"-->
</grid>

<grid drag="50 10" drop="40 70">
賴宏達、劉智翔
<!-- element style="font-size: 40px;align: right; text-align: right"-->
</grid>

<!-- slide bg="../../NTKLab_white bg_cover_resize.png"-->

---
IDEA
- ref. 
	- [[Characterization of muscle fatigue in the lower limb by sEMG and angular position using the WFD protocol.pdf]] [1]  Table2 Fatigue的定義有待商榷
	- [[Effects of various walking intensities on leg muscle fatigue and plantar pressure distributions.pdf]] [2]
	- [[Muscle Fatigue Analysis Using OpenSim.pdf]]

$EMG_{FT}$
- [[Statistical Methods for Defining and Analyzing Declining Trends]]

Fatique
由於個體差異，需要用統計方法在嘗試得到人體常模。
或者使用一些數學分析（例如頻率）找到數據的一致性。

---
Factors of fatique
- insufficient blood perfusion of muscle fibers
- depletion of energy sources
- metabolites’ build-up $\rightarrow$ excess hydrogen ions ***"slows down the waveform of an action potential"***

---

>ref. [[Effects of various walking intensities on leg muscle fatigue and plantar pressure distributions.pdf]]
>***Synchronization of the motor unit pool leads to an increase in amplitude and an increase in the duration of the activation of the EMG signal***
>頻率降低，但是振幅提升（因為同步性）
>ref. [[Characterization of muscle fatigue in the lower limb by sEMG and angular position using the WFD protocol.pdf]]

---
>
>![[RF muscle amplitude in different level of faitque.png|400]]
隨著phase的不同，股直肌過度用力（恢復機制），為了繼續產生運動並協助在疲勞階段進行代償的肌肉

---
ref. [[Characterization of muscle fatigue in the lower limb by sEMG and angular position using the WFD protocol.pdf]]

![[heart rate when fatigue.png|400]]

---
Characteristics
- RF在結束後會出現恢復性過勞行為 $> sEMG_{init}$
>post-fatigue behavior increasing the electrical amplitude until even exceeding the initial level
- 補償機制：
	- **RF和GL肌肉**在15分鐘時顯示出疲勞，並在隨後的測試中表現出一定的電活動增強，顯示肌肉有恢復過度使用的跡象。
	- **TA和BF肌肉**則在測試期間顯示出穩定的疲勞指標，沒有顯著恢復。

---
- pathological changes of neuromuscular regulations in patients with neurological impairments and is able to detect a decreasing pattern of EMG complexity
- speeds
	- 脛前肌（TA）會主動縮短，踝關節背屈，會加速疲勞
	- 足底壓力上升
	- 外翻（pronation）和內翻（supination）。然而，在疲勞狀態下，走路時會出現**外翻力矩（dorsiflexion moment）**

---
Amplitude

ref. [[Characterization of muscle fatigue in the lower limb by sEMG and angular position using the WFD protocol.pdf]]

![[different muscles when fatigue.png|600]]

---
1. RF（股直肌）疲乏中期會下降，後期代償會增加
2. BF（股二頭肌）肌肉都會增加
3. TA 疲乏初期也會下降
4. GL 中期較大

---

![[different mean of muscles when fatigue.png|600]]
誤差條的“鬍鬚”代表了每位參與者的sEMG信號振幅的變異範圍
系統需要能夠理解代償，或者要想辦法fit回去

---
Median Frequency

==步行速度的增加，脛前肌(TA)的肌電圖中值頻率會顯著下降==

>"multiplied by the **Hamming window**. The **window size** was **512 ms**. The sampling interval in the time domain was **75% of the window length**. The **average value of median** frequency in each short-time segment was used as a fatigue index of muscles in each walking condition."

ref. [[Effects of various walking intensities on leg muscle fatigue and plantar pressure distributions.pdf]]

---
Statistics Application
SD $\uparrow$ ，肌肉的運動模式變得不一致
- ==RF和BF 會趨於不穩定，SD上升==
- 透過SE and CI去分辨是否是具備統計學意義的肌肉疲勞與補償

$$\mu_x = \frac{1}{n} \sum_{i=1}^{n} x_i$$,
$$SE_x = \frac{SD_x}{\sqrt{n}}$$, but n should be a constant


$$CI_x = \mu_x \pm t_{\alpha/2} \cdot SE_x$$

用來判斷處於CI的範圍內，才合理
- 用tukey判斷同一個體各時間段落是否出現顯著差異
- 使用ANOVA：速度與持續時間
	- 步行速度 (mph): 1.8, 3.6, 5.4
	- 持續時間 (分鐘): 10, 20

---
Stablility analysis

---
Multiscale Entropy, MSE

- https://physionet.org/files/mse/1.0/tutorial/tutorial.pdf
- [[MSEtutorial.pdf]]
- https://github.com/inuritdino/MultiScaleEntropy
- [[Multi-Scale Entropy Analysis of Different Spontaneous Motor.pdf]]

應用：不同步行強度下脛前肌和腓腸肌的肌電圖訊號複雜度變化

---
- https://journal.gerontechnology.org/archives/2109-2424-1-SM.pdf
- https://pmc.ncbi.nlm.nih.gov/articles/PMC3831372/pdf/nihms439498.pdf
- [[Denoising_electromyogram_and_electroencephalogram_.pdf]]

---
Movement angles

![[Movement angles of 3 participants.png|700]]

---
Connection with Exoskeleton
生理數據資料庫
- WFDB application
- MIT-BIH database
- EMG Pattern Recognition: [LibEMG/TMR_ShirleyRyanAbilityLab](https://github.com/LibEMG/TMR_ShirleyRyanAbilityLab)

6 subjects provided data before and after targeted muscle reinervation (TMR). An array of 32 surface bipolar pre-gelled silver/silver chloride EMG electrodes were placed on each subjects’ residual forearm. Individuals were asked to perform various hand muscle contractions including hand open, 9 different grasp patterns (lateral, power, pinch with the remaining fingers opened and closed, 3 jaw chuck with the remaining fingers opened and closed, index point, hook, and tool), 8 different individual finger and thumb movements (thumb flexion/extension, thumb abduction/adduction, index flexion, middle flexion, ring flexion, and pinky flexion), and rest. Muscle contractions were held for 2 seconds and repeated 8 times for a total of 16 seconds per movement.
Datasets: https://lnkd.in/gKDerZxR
Paper: https://lnkd.in/gQStt-eC