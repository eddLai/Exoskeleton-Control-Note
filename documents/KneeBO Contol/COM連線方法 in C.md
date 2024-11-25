comX.Dispose(); 釋放COM資源

待處理
```C
					if (checkBox4.Checked)
                    {
                        string str = "AT\r\n";
                        byte[] cmd = new byte[100];                       
                        str = "AT\r\n";
                        cmd = Encoding.UTF8.GetBytes(str);
                        comX.Write(cmd, 0, str.Length);
                        System.Threading.Thread.Sleep(200);
                        str = "AT+PWMODE=0\r\n";
                        cmd = Encoding.UTF8.GetBytes(str);
                        comX.Write(cmd, 0, str.Length);
                        System.Threading.Thread.Sleep(200);                    
                        str = "AT+CON=A434F1A5BE3D\r\n";                   
                        cmd = Encoding.UTF8.GetBytes(str);
                        comX.Write(cmd, 0, str.Length);
                        System.Threading.Thread.Sleep(200);
                        str = "AT+CONNECT?\r\n";
                        cmd = Encoding.UTF8.GetBytes(str);
                        comX.Write(cmd, 0, str.Length);
                        System.Threading.Thread.Sleep(200);
                    }
```