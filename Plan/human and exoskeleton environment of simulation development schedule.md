EMG side project: [[bionic hand myocontrol]]
![[division of work with new members 20250217.png]]

| Date             | Duration length | task                                                                  | check      | Note            | developer         |
| ---------------- | --------------- | --------------------------------------------------------------------- | ---------- | --------------- | ----------------- |
| 24/10/10~25/1/16 | ~~1 week~~      | [[mocap+emg standing and walking sim log]]                            | v          | 用的是矢狀面的人體模型     | eddie, sean       |
| 25/1/16~25/3/15~ |                 | [[Customized Environment, Exoskeleton model and Sciprt control log]]  | 還需要mimic方法 | SCONE simulator | eddie, sean       |
|                  |                 | [[Review the Exoskeleton control algorithm and level of fatigue log]] |            |                 | mark, eric, Aaron |
|                  |                 | [[deployment of Exoskeleton controller from sim to real]]             |            |                 |                   |

Phase1遺留問題：
- Full body model or , 11初過後再說
- H0918 -> RLU2023
- 為什麼有時候錄下來的資料整個左標系統是反的
- 對全部的KA的分析
- 用EMD分析EMG的spectrum, STFT邊緣振幅，以及特性channel的雜訊
- CUSUM, AGLR需要分析每個肌肉的資料，並比較與文獻的差異MSE
- CEINMS 0.9 vs 0.10，現在使用wine的問題，之後走向RT
- points lost issue
- 進一步檢查SCONE生成的資料與實際差異
	- on/off時間對上
	- activation vs CEINMS adjusted activation
	- q, u
		- 
-  DepRL, SCONE gym搞懂怎麼做offline learning，更具有環境適應性的DL虛擬小腦
- 檢查環境適應性
- ==osim可以放CEINMScalibrate產出結果的地方==
	- [ ] mtuDefault
		- [ ] percentageChange
		- [ ] damping
		- [ ] Force Curve
	- [ ] dof
		- [ ] c1, c2
		- [ ] strengthCoefficient
		- [ ] pennationAngle
		- [ ] shapeFactor
		- [ ] maxIsometricForce
		- [ ] maxContractionVelocity
		- [ ] tendonSlackLength
		- [ ] optimalFibreLength
	- [ ] mtuSet
		- [ ] name
		- [ ] mtuNameSet
- OsimRL
	- 需要自己開發[[imitation learning]]或者其它RL架構
	- OsimRL有支援的架構?(無)[Deep Reinforcement Learning Workshop](https://neurips.cc/virtual/2022/workshop/49989)，一樣需要大量開發
		- [NeurIPS 2022 Tutorials](https://neurips.cc/virtual/2022/events/tutorial)
		- [AIcrowd | NeurIPS 2019: Learn to Move - Walk Around | Submissions](https://www.aicrowd.com/challenges/neurips-2019-learn-to-move-walk-around/submissions?page=1&q%5Bs%5D=score_display+asc)
		- [Reinforcement learning with musculoskeletal models](https://osim-rl.kidzinski.com/docs/models/interface/)
		- [How Forward Dynamics Works - OpenSim Documentation - OpenSim](https://opensimconfluence.atlassian.net/wiki/spaces/OpenSim/pages/53089643/How+Forward+Dynamics+Works)
- 用Scaled過的會controller對不上，先暫停可能可以用depRL解決

| Date  | Duration length | task                                                            | check |
| ----- | --------------- | --------------------------------------------------------------- | ----- |
| 10/13 | 1 month         | [[mocap+emg standing and walking sim log]]                      |       |
| 10/20 | 1 week          | running and climbing                                            |       |
| 11/2  | 2 weeks         | trasistion                                                      |       |
| 11/9  | 1 week          | 導入Exoskeleton 的model                                            |       |
| 11/16 | 1 week          | D4PG + CMA-ES 整合進 Scone                                         |       |
| 12/6  | 3 weeks         | HMI, 4 indexs to evalution, [[Dockerization]] 為了整合到Arm64 Linux上 |       |
| 12/13 | 1 week          | KV260, model par進python, NPU acc., EMG轉muscle activation        |       |
| 12/24 | 2 weeks         | week fine-tuning 繼續跑跑步機                                         |       |
| 12/25 | -               | application and EMG filter                                      |       |

把成果提前到11月前
病理的目標：平衡的很好
- [Torso muscle EMG profile differences between patients of back pain and control - ScienceDirect](https://www.sciencedirect.com/science/article/pii/S0268003309002526?ref=pdf_download&fr=RR-2&rr=8f3e2c5f2e418454)

![[EXO_schedule_20241101.png]]
https://miro.com/welcomeonboard/MW5VQ0Z6RzdydVZXRnB3SEI0ZThETTdyaTlqdE1OVmo0elFwRndUWGE4akx0d1lLNURQNFp3dmltUU1nclN5YXwzNDU4NzY0NTc0OTA5NzMzNTQ4fDI=?share_link_id=448721730790

---
## Environment setup
script: https://drive.google.com/file/d/1hkAW0v1uI5a-RmqmFO94sdbuqrGNXU6K/view?usp=sharing
- Ubuntu+mamba+conda+git
- Data of motion capture and EMG(sean1009): https://drive.google.com/file/d/16MtPkEdB8mLzgeYqDPMfbAr_ctd6Iz3X/view?usp=drivesdk

- github code: https://github.com/eddLai/ExoskeletonPowerAsistance.git
- pls find out these download link on [SimTK: Welcome](https://simtk.org/)
 - Download: python3.11+opensim_python+opensim4.4+CEINMS
 - Download: python3.9+peotry+SCONEpy+SCONE+HyFyDy