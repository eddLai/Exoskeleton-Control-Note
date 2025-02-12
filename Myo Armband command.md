基於`serial`, `serial.tools.list_ports`用於透過serial操控dongle

| 指令名稱                                              | BLE 類別 (`cls`) | BLE 指令 (`cmd`) | 參數                                                                  | 功能                | 來源           |
| ------------------------------------------------- | -------------- | -------------- | ------------------------------------------------------------------- | ----------------- | ------------ |
| `connect(addr)`                                   | `0x06`         | `0x03`         | `addr` (6 bytes, 目標裝置 MAC 地址)                                       | 嘗試與指定的裝置建立 BLE 連線 | **電腦**       |
| `get_connections()`                               | `0x00`         | `0x06`         | 無                                                                   | 取得當前的連線資訊         | **電腦**       |
| `discover()`                                      | `0x06`         | `0x02`         | `b'\x01'` (啟動掃描)                                                    | 啟動 BLE 裝置掃描       | **電腦**       |
| `end_scan()`                                      | `0x06`         | `0x04`         | 無                                                                   | 結束 BLE 掃描         | **電腦**       |
| `disconnect(h)`                                   | `0x03`         | `0x00`         | `h` (1 byte, 連線 ID)                                                 | 中斷指定連線            | **電腦**       |
| `read_attr(con, attr)`                            | `0x04`         | `0x04`         | `con` (1 byte, 連線 ID), `attr` (2 bytes, 屬性 ID)                      | 讀取裝置某個特定屬性的值      | **電腦 → Myo** |
| `write_attr(con, attr, val)`                      | `0x04`         | `0x05`         | `con` (1 byte, 連線 ID), `attr` (2 bytes, 屬性 ID), `val` (變數長度, 欲寫入的值) | 寫入裝置的某個特定屬性       | **電腦 → Myo** |
| `send_command(cls, cmd, payload, wait_resp=True)` | 動態決定           | 動態決定           | `payload` (可變長度, 具體數據)                                              | 發送自訂 BLE 指令       | **電腦**       |
