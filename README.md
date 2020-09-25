# Nginx_IPC
通訊方式


# Chennel 管道

採用父子處理程序時，父子處理程序憑藉 Chennel | Pipeline 溝通訊息。
IPC 中 非同步的 msg queue (訊息佇列) 、signal (訊號) 和 同步的 semephore (號誌) 沒有應用於此，因為 Nginx 代理伺服器沒有支援，因為 Nginx 採用有親緣關係的父子處理程 Multi Processes 序取代多執行緒 Multi Threads 的請求處理方式 !

因為採用管線的通訊方式，本身已經受限制的缺點如下：

* 無雙向傳輸

* 不處理不同處理程序之間的關係


# Socket 通訊阜

當不同主機，包含不同虛擬主機之間的通訊，採用 socket 建立連線，
例如使用者端與伺服器端建立的連線。



