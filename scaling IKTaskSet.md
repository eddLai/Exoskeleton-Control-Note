對於優化算法，這樣定義權重:
## Marker Tasks
虛擬與實驗標記之位置差異
```
<IKMarkerTask name="Sternum"> <weight>1</weight> </IKMarkerTask>
<IKMarkerTask name="R.Acromium"> <weight>1</weight> </IKMarkerTask>
```

## Coordinate Tasks
用來約束關節
```
<IKCoordinateTask name="mtp_angle_r"> <value>0</value> </IKCoordinateTask>
<IKCoordinateTask name="lumbar_extension"> 
    <value>0</value> 
    <weight>1000.0</weight> 
```