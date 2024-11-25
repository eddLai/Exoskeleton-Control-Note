```C
void KneeBO_CMD(byte table, byte pa1, byte pa2)
        {
            byte[] buf = new byte[7] { 0, 0, 0, 0, 0, 0, 0 };

            buf[0] = 0x4A;  //Start byte
            buf[1] = 0x01;  //Device no.
            buf[2] = table; //Funtion
            buf[3] = pa1;   //Patameter 1
            buf[4] = pa2;   //Patameter 2
            buf[5] = 0x44;  //End byte

            for (int i = 0; i < 6; i++)
            {
                buf[6] ^= buf[i];
            }

            if (comX != null && comX.IsOpen)
            {
                comX.Write(buf, 0, buf.Length);
            }
        }
```