# Nginx_IPC
通訊方式


# Chennel 管道 

採用父子處理程序時，父子處理程序憑藉 Chennel | Pipeline 溝通訊息。
IPC 中 非同步的 msg queue (訊息佇列) 、signal (訊號) 和 同步的 semephore (號誌) 沒有應用於此，因為 Nginx 代理伺服器沒有支援，因為 Nginx 採用有親緣關係的父子處理程 Multi Processes 序取代多執行緒 Multi Threads 的請求處理方式 !

因為採用管線的通訊方式，本身已經受限制的缺點如下：

* 無雙向傳輸，僅單向

* 不處理不同處理程序之間的關係


# Socket 通訊阜

當不同主機，包含不同虛擬主機之間的通訊，採用 socket 建立連線，
例如使用者端與伺服器端建立的連線。

系統內也能採用 Socket 通訊方式，當主機和目標都是同一 IP 時，
此時的通訊方式是雙向的。

啟動 Master Process 及其產生子處理程序的函數：

      // main
      
      ngx_daemon(){
      
        fork();
        
        ngx_pid = ngx_getpid();
        
        umask(0);
        
        fd = open("/dev/null/", O_RDWR); 
        
        return NGX_OK;
      
      }


# 在系統內實現通訊阜通訊

起始點與目的地點都需要同 IP！

建立通訊端口的函數：

       int socketpair(int d, int type, int protocol, int sv[2])

函數參數的解釋：

* d = domain , 為通訊端口的域，此可設定為 AF_UNIX。

* type ， 為通訊端口的類型，分為 STREAM 和 DGRAM 兩種，前者需要建立連線，後者無需建立連線，用於處理程序間通訊則採用前者。

* protocol，使用的協定，當應用於處理程序間通訊時，則設定為 0。

* sv[2]，指向儲存檔案描述符號的指標，建立兩通訊端口的檔案描述符號指標。
