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
Develop log: 
<!-- element style="font-size: 35px;align: left; text-align: left;color: white"-->
</grid>

<grid drag="50 10" drop="40 70">
賴宏達、劉智翔
<!-- element style="font-size: 40px;align: right; text-align: right"-->
</grid>

<!-- slide bg="../NTKLab_white bg_cover_resize.png"-->

---
## Idea
HyFyDy, DepRL, SCONE gym都有**引入額外的模型**，展現其環境適應性
How?
1. (單獨訓練出一SCONE這個可解釋架構)
2. 用RL policy(同DepRL架構)串接低階控制器
>猜測可能需要DL的資料衍生能力
3. 要從Offline走到Online跟外骨骼做互動

1. Control the EXO in simulation
	1. 怎麼導入物件 e.g.[(82) Tripping and Slipping Simulations (short) - YouTube](https://www.youtube.com/watch?v=MudlYgzAxro)
	2. 怎麼導入虛擬模型
	3. 怎麼控制
2. if assisting or obstacle from current and $\omega$ 