# ICND TCP/IP
傳輸控制通訊協定(end-to-end)/網際網路通訊協定之堆疊(protocol stack)

# 網際網路通訊協定

可用於跨越任何網路連線，包含區域或是廣域網路。

# TCP/IP Protocol Stacks


       Level 5          應用層 （包含：FTP、SMTP、
                                telnet實現虛擬終端機和遠端登入為設備做管理、
                                SNMP、DNS、）


       Level 4          傳輸控制（傳輸）


       Level 3          網際網路（網路）

       Level 1-2        網路介面


# TCP

傳輸層服務讓使用者能切割（segment）與重組 (reassemble) 將上層應用程式化成為傳輸層資料流 flux。


* end to end

傳輸層的資料流即為端點（終端）對端點（終端）的傳輸服務（發送端 <-> 接收端）。

* slide window

滑窗機制功能為控制流量，協調兩端主機每次傳送的資料量。

# IP












