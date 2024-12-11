注意：使用bind是做為server，而使用connect則是做為client
in python, PC端
## Server
1. **`server_socket.bind((host, port))`**: 這一行將服務器綁定到特定的IP地址和端口。這樣，當客戶端嘗試連接到這個地址和端口時，它會連接到這個服務器。
2. **`server_socket.listen(1)`**: 這一行讓服務器開始監聽來自客戶端的連接請求。數字`1`表示最大的等待連接的客戶端數量。
3. **`client_socket, address = server_socket.accept()`**: 這一行會阻塞，直到一個客戶端連接到服務器。一旦有客戶端連接，它會返回一個新的socket對象和客戶端的地址。
## Client
1. **`client_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)`**: 這一行創建一個新的socket對象。
2. **`client_socket.connect((host, port))`**: 這一行嘗試連接到服務器的指定IP地址和端口。
3. **`print(f"Successfully connected to {host}:{port}")`**: 如果連接成功，這一行會輸出成功消息。

---