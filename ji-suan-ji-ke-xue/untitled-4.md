# 第二章 應用層

第二章 應用層

應用層協議原理

 研發網絡應用層核心是寫出能夠運行在不同的端系統和通過網絡彼此通信的程序。

網絡應用程序體系結構

 應用程序體系結構（application architecture\)

 客戶-服務器體系結構 （client-server architecture\)

 P2P體系結構（對等方到對等方的結構）特徵之一：自擴展性

進程通信

1.客和服務器進程

客戶\(client\) 服務器\(server\)

2.進程與計算機網絡之間的接口

套接字\(socket\) 應用程序與網絡之間的應用程序編程接口

3.進程尋址

爲了標識接受進程,需要定義兩種信息:

1.主機的地址

2.在目的主機中指定接收進程的標識符

應用分配特定端口號

舉例

web服務器端口 50

郵件服務器進程\(SMTP\)

可供應用程序使用的運輸服務

1.可靠的數據傳輸\(reliable data transfer\)

2.吞吐量

具有吞吐量要求的應用程序被稱爲帶寬敏感應用

3.定時

較低的時延更好

4.安全性

加密 解密

因特網提供的運輸服務

1.TCP服務

面向連接的服務

經過握手階段之後,開始傳輸

全雙工通信

可靠的數據傳輸服務

沒字節的丟失和冗餘

具有擁塞控制機制

可以使用SSL來加強以提供安全服務

2.UDP服務

不可靠的數據傳輸服務

可亂序,不保證接受到,無握手,有擁塞控制機制.

應用層協議

1.交換的報文類型

2.各種報文類型的語法

3.字段的語義

4.確定了一個進程何時以及如何發送報文,對報文進行響應的規則

Web與HTTP

HTTP概況

Web的應用層協議\(HTTTP,HyperText Transfer Protocol 超本傳輸協議\)

多數Web頁面含有一個HTML的基本文件\(base HTML file \)

Web瀏覽器\(Web browser\) 實現HTTP的客戶端,服務器端用於存儲Web對象,每個對象由URL尋址.

HTTP服務器並不保存關於客戶的任何信息,所以HTTP是一個無狀態協議\(stateless protocol\)

非持續連接與持續連接

一.非持續連接

往返時間\(Round-Trip Time,RTT\)

總響應時間 = 2 X RTT + 服務器傳輸HTML的時間

缺點

1.爲每一個請求對象建立與維護一個全新的連接

2.每一個對象經受兩倍RTT的交付時延 \(一個用於TCP的創建,一個用於請求和接受一個對象\)

二.持續連接

經過一定時間間隔 \(一個可配置的超時間隔\) 仍未被使用,HTTP服務關閉連接.

HTTP報文格式

分爲請求報文與響應報文

一.請求報文

1.請求行（request line） ①方法字段 GET ,POST,HEAD,PUT,DELETE

 ②URL字段

 ③HTTP版本字段

2.首部行（header line\)

3.空行

4.實體行

二.響應報文

1.狀態行 ①版本字段

 ②狀態碼

 ③相應狀態信息

2.首部行 conntection

 Date

 Server

 Last-Modified

 Content-length

 Content-Type

3.空行

4.實體行

常見狀態碼

200 OK

301 Moved Permanently

400 Bad Request

505 HTTP Version Not Supported

用戶與服務器交互：cookie

4個組件 ： 1.HTTP響應報文中的一個cookie首部行

 2.HTTP請求報文中一個cookie首部行

 3.用戶端系統中保存有一個cookie文件

 4.位於Web站點的一個後端數據庫

Web緩存

Web緩存器（Web cache\) --------- 代理服務器 （proxy Server\)

通過使用內容分發網絡CDN

 Web緩存器正在因特網上發揮着越來越重要的作用

條件GET方法

HTTP協議有一種機制，允許緩存器證實它的對象是最新的

因特網中的電子郵件

用戶代理

郵件服務器

簡單郵件傳輸協議

SMTP

用戶 ---- 服務器

對比HTTP

HTTP pull

SMTP push

SMTP 7比特ASCII碼進行編碼

HTTP 每個對象封裝進響應報文

SMTP 所有對象封裝進入響應報文

郵件報文格式

From：

To：

Subject：

郵件訪問協議

1.POP3

RFC1939 進行定義

特許

事務處理 （下載並刪除，下載並保留）

更新

2.IMAP

服務器把每個報文與一個文件夾聯繫起來

允許用戶代理獲取報文某些部分的命令

3.基於Web

用戶代理 -------- sevser ------ servser

 HTTP SMTP

DNS:因特網服務目錄

域名系統

DNS

1. 分層式的DNS服務器

2.應用層協議

通常的IP地址就緩存在一個附近的DNS服務器中

有助於減少DNS的網絡流量與DNS的平均時延

重要服務

主機別名

規範主機名

郵件服務器別名

DNS工作機理概述

單點故障

通信容量

遠距離的集中式數據庫

維護

1.分佈式層次數據庫

根DNS服務器-----頂級域DNS服務器-----權威DNS服務器

2.DNS緩存

DNS記錄與報文

資源記錄 RR

（提供主機名到IP地址的映射 \)

\(Name,Value,Type,TTL\)

\(主機名，IP，A\)

\(個域，權威DNS，NS）

\(個域，規範主機名，CNAME）

\(個域，郵件服務器的規範全名，MX）

1.DNS報文

2.在DNS數據庫中插入記錄

P2P文件分發

1.P2P體系結構

客戶-----服務器體系結構

Dcs=max\(NFus,Fdmin\)D\_{cs} = max\({ \frac{NF}{u\_s},\frac{F}{d\_{min}}}\)Dcs​=max\(us​NF​,dmin​F​\)

 P2P最小分发时间

Dp2p&gt;=max\(Fus,Fdmin,NFus+u1+u2+....ui\)D\_{p2p}&gt;= max\({ \frac{F}{u\_s},\frac{F}{d\_{min}},\frac{NF}{u\_s+u\_1+u\_2+....u\_i}}\)Dp2p​&gt;=max\(us​F​,dmin​F​,us​+u1​+u2​+....ui​NF​\)

 2.BitTorrent

一個特定的文件分發的所有對等方的集合被稱爲一個洪流\(torrent\)

每個洪流具有一個基礎設施節點,成爲追蹤器.\(tracker\)

最稀缺優先\(rarest first\) : 首先請求在鄰居副本中數量最少的塊疏通: 確定以最高的速率流入的四個鄰居

一些有趣的機制 片\(小塊\),流水線,隨機優先選擇,殘局模型與反怠慢機制

林一種P2P應用 ------------分佈式散列表\(DHT\) {BTC 就是 靠得這個\)

內容分發網頁

\(Content Distribution Network,CDN\)

CDN 管理分佈在多個地理位置上的服務器,在它的服務器種存儲視頻,並且所有試圖江每個用戶請求定向到一個將提供最好的用戶體驗的CDN位置.

1.CDN操作

截獲請求:

確定適合的CDN服務器集羣

重新定向

2.集羣選擇策略

CDN部署核心:

週期性實時測量

地理上最爲臨近

套接字編程:生成網絡應用

UDP套接字編程

UDPclient.py

```text
From socket import *servserName = 'hostname'servserPort = 12000clientSocket = socket (AF_INET,SOCK_DGRAM)meassage = raw_input('Input lowercase sentence:')clientSoket.sendto(message.encode(),(servserName,serverPort))modifiedMessage,serverAddress = clientSocket.recvfrom(2048)print(modifiedMessage.decode())clientSocket.close()
```

UDPServer.py

```text
from  socket import   *servserPort = 12000serverSocket = socket(AF_INET,SOK_DGRAM)serverSocket = bind (   (   '  '   ,  serverPort  )   )print(“The Server is ready to receive")while True :    measssge,clientAddress = serverSocket.recvfrom(2048)    modfiedMessage = message.decode(  )  . upper(  )    serverSocket.sendto(modifiedMessage.encode(  ),clientAddress)
```

**TCP套接字编程**

TCPClient.py

```text
from socket import * serverName = 'servername'serverPort = 12000clientSocket = socket(AF_INET,SOCK_STREAM)sentence = raw_input ('Input lowercase sentence:')clientSoket.send(sentence.encode())modfiedSentence = clientSocket.recv(1024)print ('From Server:',modfiedSentce.decode())clientSocket.close()
```

TCPServer.py

```text
from socket import * serverPort = 12000clientSocket = socket(AF_INET,SOCK_STREAM)serverSocket.bind((' ',serverPort))serverSocket.listen(1)print('The server is ready to recive ')while True    connectionSocket, addr = serverSocket.accept( )    sentence = connectionSocket.recv(1024).decode( )    capitalizedSentence = sentence.upper( )    connectionSocket.send(capitalizedSentence.encode())    connectionSocket.close( )
```

