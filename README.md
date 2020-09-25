# Nginx_IPC
通訊方式


# Chennel 管道

採用父子處理程序時，父子處理程序憑藉 Chennel | Pipeline 溝通訊息。
非同步的 msg queue (訊息佇列) 、signal (訊號) 和 同步的 semephore (號誌) 沒有應用於此。


# Socket 通訊阜

當不同主機，包含不同虛擬主機之間的通訊，採用 socket 建立連線，
例如使用者端與伺服器端建立的連線。



