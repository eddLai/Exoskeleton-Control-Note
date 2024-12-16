![[pipeline of building Digital Twins.png]]
![[correct the pipeline]]
tools: [[SCONE]]用來RL training, [[overview of opensim]]用來進行IK推測, [[CEINMS app.]], EMG-informed methods or EMG-driven methods?
target: [[mocap+emg standing and walking sim]], [[level of fatigue from EMG]]

---
ref. [[Robust_Real-Time_Musculoskeletal_Modeling_Driven_by_Electromyograms.pdf]]
>"predicting joint moments from motor tasks"
>"framework can operate online on low power embedded systems"
==表示目前沒有的技術成分==
## software components:
使用ANSI C++
- external recording devices
- OpenSim API
>"real-time inverse kinematics (IK) and inverse dynamics (ID) performed using the OpenSim API"
>"The IK problem in OpenSim is solved via static optimization"
>root mean squared error (RMSE) to check marker between virtual and MOCAP
>=="Kalman filter to process IK-generated joint angles"==
>>parameters: [doi:10.1016/j.jbiomech.2008.09.035](https://pdf.sciencedirectassets.com/271132/1-s2.0-S0021929008X00156/1-s2.0-S0021929008004685/main.pdf?X-Amz-Security-Token=IQoJb3JpZ2luX2VjEGEaCXVzLWVhc3QtMSJGMEQCIBYVLeEyyRlSO7HFOoo4BJIDuIoy77kuSQUnX9nx9Q5FAiB%2B3KAfF9l2Cx56VNcxpN2gpgWAJCru8DeSNFTontqTziqzBQgpEAUaDDA1OTAwMzU0Njg2NSIMsbmA88NRcCn%2F90esKpAFguxpsweMh%2ByvXyhLkoP56N%2FUz9n5ShdIB4avIx6wm74cUAxhn8o1wjTCTi8Ug6kmXOthqntk1LxXSIbc2wbrxxtGfUiWtWUvbdcfz4owh1wvX3%2BYChPV7yY1QaXpWBUFmN2PH2qSaX5YOoiA8qKHb7Ksyqm477VPTQ7XAnO5Ru9DOjGciiwLNU7fAzfV72cIpP8gTMvOeLYGFIJUf0MOA3MJb%2Bf4JCz5FteBnaFzvvaf9iDnZ9%2BlMtKEh4pqxwXV6R4WNJyZqMgNTdXVK4aYXGRC2UeXWdzWU42UvydXeoEB%2FUdNncFrArqqZFr40mD07t211ViKiJcSQpggjXKJWS%2BUlFSyOQLQQp1dHqZQskVxM8ZYRWSXqqlDucBlsx3gGRVwMLNttCeTWN54xA%2FICDclBoTHf%2FDLMtcB4qw43C9sBeSeHBH26HuxPzDJf8LrSb3R%2BMvS%2FgBDNnusRmjqgYU73%2BVkvef%2BgGRgtbSlcJyXqgIMVfJ%2BWUOWfhK4Wq%2F%2FB3NlTqZDPHuZ73YvzoD4U5re4NCDa7hb%2Fs4OCX5O1MgwA8LGS2KNORgPTaWOAmm9GpK59Lf9hQ68GXRvcHmJqa0T9HRsXa6IWuY8V4d%2BOLUi1oPXEQCRO7VAbI%2FIXzgcYfi1lCRmccrE0b3T4P%2BHy2s1hTnloTvyFDgDMNXOLm1%2FpF4g0%2BJ3%2FFsIixK%2BQvsn%2BXD6jAJXVjygaVp%2B%2FEZ2QzYBwBhlw6j%2BGVTkLHixjeP%2BibFU%2FNgsgkn%2Bkyt2q%2FS%2FaWz7dPIGvXAkINAOFVWrqamUffwusBfbErlH%2FrA%2Bm9ZnSsf8wbplji3FdicBeZnzbudkpG%2BYT78xPzx244BmADlfsqqzfGxOzYbMt9VpxcQw7b7%2FugY6sgFJjyRMar%2BBhmdlhOLhaA3RBr4AHw4AiRNctlI%2B14tNZo4mb6crOdfohKn17gXiZM%2FgQh1n7oH5mlI6y93TCGIVWSEj9LL7jbwQ2sOfqA%2BaXiHNBoD0kySBLSEpcdU6%2Fe4%2BOgdgKKBNPoJWaR8AItSd6wqV1kC2Q9cAmo8H7vN88f6TY4tmb4RJA4CHF46tfJ6E4gh1YWR7f4OZyWWDw3xKiosddVk%2B%2FsCawHXSy2dkE8Xv&X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20241216T085654Z&X-Amz-SignedHeaders=host&X-Amz-Expires=300&X-Amz-Credential=ASIAQ3PHCVTY42AX2BPR%2F20241216%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Signature=5bc629bbafda06c91ac5bb3fc3ee5711f9c34f1c36b29a912e8379b056841648&hash=778e7165a7ef4676b1ea4adaaf1042ee06c9ac9c178fa807825d198dd216deb8&host=68042c943591013ac2b2430a89b270f6af2c76d8dfd086a07176afe7c76c2c61&pii=S0021929008004685&tid=spdf-ac232085-7541-430a-8f5a-f8342815f4e2&sid=0e729d377343d644d95af391f3e5c8333213gxrqa&type=client&tsoh=d3d3LnNjaWVuY2VkaXJlY3QuY29t&ua=161259035002565152&rr=8f2d767eac5d8288&cc=tw)
- computation of musculotendon kinematics(Multidimensional Cubic BSpline (MCBS) method)
- CEINMS

## Hardwares
- TCP/IP direct connection to external EMG amplifiers -> ~~amplitude-normalized linear envelopes~~(一致) -> filter沒有用帶通，其它都一樣
	- ~~high-pass filtering, full-wave rectification, and low-pass filtering~~
	- amplitude normalization: ==peak-processed values== for ==musculotendon unit (MTU) force-production modeling==
		- isometric maximal voluntary contractions (MVCs)
		- dynamic trials
- TCP/IP direct connec tion to MOCAP
- different threads within a multi-stage pipeline

---
### Terms
- physiological electromechanical delay (EMDs).


需要muscle-tendon kinematics