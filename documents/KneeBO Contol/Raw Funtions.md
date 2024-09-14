備註：
>sender按鈕, e事件

### button1_Click
KneeBO_CMD(0x21, 3, 0); Ask KneeBO for Hello
checkBox4: 複選框

### button2_Click
KneeBO_CMD(0x21, 0, 0); Stop KneeBO Selected mode

### button3_Click
清空richTextBox1

levelSp trackBar7 label20
levelF   trackBar8 label22
times   trackBar9 label24

### button25_Click
>>會進入tabControl1.SelectTab(2)，第三個顯示頁面
>KneeBO_CMD(0x2D, 1, upperB); 
>>upper bound value, unit:1 deg
>>`upperB = Convert.ToByte(textBox67.Text);`
>
>KneeBO_CMD(0x2D, 2, lowerB);  
>>lower bound value, unit:1 deg
>>`lowerB = Convert.ToByte(textBox68.Text);`
>
>KneeBO_CMD(0x2D, 3, upperR);   //Set upper range, unit: 1 deg
>KneeBO_CMD(0x2D, 4, lowerR);   //Set lower range, unit: 1 deg
>KneeBO_CMD(0x2D, 5, levelSp); //Set speed level, 1-10
>KneeBO_CMD(0x2D, 6, levelF);  //Set force Level, 1-10
>KneeBO_CMD(0x2D, 8, times);   //Set repeat times, unit: 1 times
>KneeBO_CMD(0x2D, 9, gravity); //Gravity compensate function, 0:disable, 1:enable
>>if (checkBox2.Checked) gravity = 1; else gravity = 0;
>
>KneeBO_CMD(0x40, 43, 0);     Select ROM mode
>KneeBO_CMD(0x21, 1, 0);       Start KneeBO Selected mode
>KneeBO_CMD(0x21, 0, 0);       Stop KneeBO Selected mode
>KneeBO_CMD(0x21, 0, 0);       Disable Device
>KneeBO_CMD(0x21, 1, 0);       Enable Device

trackBar12 label27
trackBar11 label26
trackBar10 label25

### button27_Click ==ISO page==
radioButton12.Checked
radioButton13.Checked

radioButton9.Checked
KneeBO_CMD(0x40, 40, 0);    //Select Isokinetic mode

radioButton10.Checked
KneeBO_CMD(0x40, 41, 0);    //Select Isotonic mode

radioButton11.Checked
KneeBO_CMD(0x40, 42, 0);    //Select Isometric mode

KneeBO_CMD(0x2D, 0, dir);
>`dir` 1, flex
>`dir` 2, ext
>`dir` 3, both

button29_Click_1 -> button2_Click(null, null);

trackBar4  label54 , if == 10, trackBar13.Enabled = false;

trackBar5 label63 Flex
trackBar6 label61 Ext
trackBar13 label60 IMU
trackBar15 label67 stepL

KneeBO_CMD(0x51, 0, gain);           //Set assistance gain, 0 - 10
KneeBO_CMD(0x51, 1, flex);           //Set flex velocity level, 1 - 6
KneeBO_CMD(0x51, 2, ext);            //Set extend velocity level, 1 - 6
KneeBO_CMD(0x51, 3, imu);            //Set IMU level, 0 - 8, unit: 10 deg / s
KneeBO_CMD(0x51, 4, locktime);       //Set lock time, unit: 1s
System.Threading.Thread.Sleep(200);
KneeBO_CMD(0x51, 5, angle);           //Set limit angle, unit: deg, min: 20
KneeBO_CMD(0x51, 6, init);            //Set initial angle 0:-4 deg, 1:-3 deg … 13:9 deg, 14:10 deg
KneeBO_CMD(0x51, 7, side);            //Set which side, 0:R, 1:L
KneeBO_CMD(0x51, 8, stepL);           //Set unlock angle level, 0-10
System.Threading.Thread.Sleep(200);
KneeBO_CMD(0x40, 60, 0);              //Select Walk mode
