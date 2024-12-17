---
bg: "[[NTKLab_white bg.png]]"
autoSlide:
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
	}
	.with-border{
		border: 1px solid red;
	}
</style>
<grid drag="70 10" drop="-3 40">
Muscle Fatigue Analysis Using OpenSim
<!-- element style="font-size: 40px;align: left; text-align: left;color: white"-->
</grid>

<grid drag="80 10" drop="-3 70">
Jing Chang1, Damien Chablat[1], Fouad Bennis[1], and Liang Ma[2][1] 
- [1] Laboratoire des Sciences du Numerique de Nantes (LS2N), Ecole Centrale de Nantes, 44321 Cedex 3, Nantes, France 
- [2]  Department of Industrial Engineering, Tsinghua University, Beijing, 100084, P.R.China
</grid>
<!-- slide bg="[[NTKLab_white bg_cover_resize.png]]"element style="font-size: 25px"-->

---
## 摘要
ref. [[Muscle Fatigue Analysis Using OpenSim.pdf]]
- muscle capability的資料很重要: ***OpenSim*** and ***AnyBody*** 才有
- 加入accumulation effect的opensim plug-in
- recall: residual reduction algorithm用來使model接近真實實驗數據

---
## Muscle fatigue mathematics description
$$\frac{dF_{cem}(t)}{dt}=-k\frac{F_{cem}(t)}{F_{max}}F_{Load}(t)$$

ref. **A new simple dynamic muscle fatigue model and its validation.**
Validated by static MET models.一個關注代謝的模型

---
### definition of fatigability 
includes intrinsic human attribute
>***"Muscle fatigability describes a tendency of a muscle from a given subject to get tired or exhausted, and it should only be determined by the physical and psychological properties of the individual subject"***

ref. Measurement of subject-speci c local muscle fatigabiltity

---
### Some characteristic
- females are found to be more fatigue-resistant than males
- older, much less force loss than the younger group after a certain exercises

ref. Sex differences with aging in the fatigability of dynamic contractions

---
## Apply in Opensim
Force-load muscle fatigue model

---
### workload on each muscle along the motion
muscle force generation phase

1. activation dynamics:
>"calcium release, diffusion and uptake from the sarcoplasmic reticulum",
>
>u is excitation; $$assume:Ca^+ \propto activation$$;
>$$\frac{da}{dt}=\frac{u-a}{\tau(u,a)}$$

---
2. contraction dynamics
	- force-length($l_m$)-velocity relationship$f_v$
	- elastic properties+tendon($l_mt$)	
	
	>$$\frac{dl_m}{t}=f_v^{-1}(l_m, l_{mt},a)$$

Opensim之CMC是用來推算series of muscles activation，得到Forward Dynamic Simulation

recall
- IK得到角度
- ==ID得到的關節總力會distribute joint force among a series of muscles==

---
### the maximal muscle capability
muscle force increases with muscle activation.

Full activation會被用於作為Fatigue計算之$F_{max}$
