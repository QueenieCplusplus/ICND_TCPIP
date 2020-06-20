# ICND TCP/IP
傳輸控制通訊協定(end-to-end)/網際網路通訊協定之堆疊(protocol stack)

# 網際網路通訊協定

可用於跨越任何網路連線，包含區域或是廣域網路。

# TCP/IP Protocol Stacks


       Level 5          應用層 
                                         （包含：FTP、SMTP、
                                          telnet實現虛擬終端機和遠端登入為設備做管理、
                                          SNMP、DNS）


       Level 4          傳輸控制（傳輸）  
       
                                         （使用 UDP 通訊協定的服務包含：
                                           SNMP、DNS、FTP、NFS)


       Level 3          網際網路（網路）
       

       Level 1-2        網路介面
       
       


# TCP

傳輸層服務讓使用者能切割（segment）與重組 (reassemble) 將上層應用程式化成為傳輸層資料流 flux。

* segmentation 

碎片化的好處是讓出入的 payload 較為少，（雖然數量變多），但可節省頻寬。

* end to end

傳輸層的資料流即為端點（終端）對端點（終端）的傳輸服務（發送端 <-> 接收端）。

* slide window (Congestion Control)

滑窗機制功能為控制流量，協調兩端主機每次傳送的資料量。

* seq id & ack

封包確實收到的保證(配合序列編號)，而序列編號則是確保資料正確的排序。

* UDP

TCP 中以兩種協定，一為 TCP，一為 UDP。UDP 與 TCP 不同，沒有重送功能，倘若接收者沒有收到封包，沒有檢查封包傳送的狀況之能力。

* Packet (TCP header)

connection-oriented.

           +------------+--------------+
           |  SRC Port  ｜   DES Port  ｜
           +------------+--------------+
           |        Sequence ID        |
           +---------------------------+
           |          Ack ID           |
           +----+----+----+------------+
           | LEN| RES|Code|   Window   |
           +----+----+----+------------+
           |   Checksum   |    Urgent  |
           +--------------+------------+
           |          Option           |
           +---------------------------+
           |           Data            |
           +---------------------------+
           
           /* 窗：設備能接收的八位元值。 */
           
           /* 選項：最大的TCP segment 大小 */
           
           /* Data: 來自上層通訊協定的資料。 */
           
* Packet (UDP header)

connectionless

           +------------+--------------+
           |  SRC Port  ｜   DES Port  ｜
           +--------------+------------+
           |   Checksum   |     LEN    |
           +---------------------------+
           |           Data            |
           +---------------------------+
           
           /* checksum: 標頭與資料欄的計算值。 */
           
  * Port
  
  
  * 3-way handshake

# IP

* IP

connectionless

* Packet (IP)

       +---------+-----+----------+-----------+
       | version | LEN | Priority | Total Len |
       +---------+-----+----------+-----------+
       |    標識   |   Flags   |Fragment Offset|
       +----------+-----------+---------------+
       |    TTL   |  protocol |    Checksum   |
       +--------------------------------------+
       |                SRC IP                |
       +--------------------------------------+
       |                DES IP                |
       +--------------------------------------+
       |                Option                |
       +--------------------------------------+
       |                 Data                 |
       +--------------------------------------+
       
       /*標識：IP 資料元可能存放*/
       
       /* flags: 標明分段是否發生。*/
       
       /* protocols means UDP or TCP. */
       
       /* protocols 欄位可能也標示了第三層通訊協定使用的演算法協定
       如 OSPF、GRE、EIGRP ，請詳通訊協定編號*/
       
       /* checksum: 檢查標頭的完整性。 */
  
       /* Fragment Offst: 為資料分段，使得不同 MTU 可以在網路上傳送 */
       
       /* 選項：包含網路測試與安全。* /
       

* ICMP

用於傳遞錯誤與控制訊息，被應用在所有使用 TCP/IP 的主機上，其封包內包含已定義的資訊和尚未定義的資訊，其中已經定義的資訊如下：

（常見於 ping 指令下，傳送與接收的封包訊息：echo <-> echo reply）

- [x] destionation unreachable

- [x] time exceeded

- [x] param problem

- [x] subnetmask request

- [x] redirect

- [x] echo

- [x] echo reply

- [x] timestamp

- [x] timestamp reply

- [x] info req

- [x] info reply

- [x] addr req

- [x] addr reply

* ARP

由已知 IP 位置，尋找 DataLink 層級的位置。

(常見於發送端檢查 ARP cache table)

* RARP

由已知 DataLink 層級的位置，找出上層 IP 位置。

(常見於 DHCP 的應用)


# 通訊協定編號

https://tools.ietf.org/html/rfc1700

       通訊協定名稱                              通訊協定欄位中的編號

        ICMP, Internet Control Msg Protocol              1

        IPv6                                            41

        IPX                                            111

        L2 Tunneling Protocol                          115

        IGRP, Interior Gateway Routing Protocol          9

        GRE, Generic Routing Encapsulation              47


# Subnet Mask

(又稱為 prefix)

to be continued...

# IP set up

常見於網管工作如：

(1) 在交換器上設定 IP add 與 Default GW 

    
    switch(congfig)# ip address + <ip address> + <subnet-mask 必須使用 decimal>
    
    switch(config)# ip default-gateway + <路由的網路邏輯位址>
    

(2) 在路由器介面上設定 IP add

    router(config-if)# ip address + <ip address> + <subnet-mask 必須使用 decimal>

(3) 設定時，均伴隨子網路遮罩，其格式設定如下

    router#term ip netmask-format {包含 bit count| decimal| hex}

(4) 主機名稱設定

    router(config-line)# ip host + <name> + <tcp-port-no.> + <ip-add>
    // 倘若有多個 IP 介面，則一台設備最多可以擁有 8 個不同的位址。
    // host 代表主機或伺服器。

(5) 伺服器定義網域名稱

    此由 Name Server 名稱伺服器所管理。










