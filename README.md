# RUT200_Study
+ 「RUT200」是「TELTONIKA NETWORKS」所生產的一款工業級路由器，提供SDK讓使用者二次開發。

### 原廠(來自立陶宛)
+ TELTONIKA NETWORKS
+ 官網: https://teltonika-networks.com/
+ 產品相關連結:
  + RUT200 - INDUSTRIAL CELLULAR ROUTER
    + https://teltonika-networks.com/product/rut200/
  + RUT200 - Teltonika Wiki Knowledge Base
    + https://wiki.teltonika-networks.com/view/RUT200

### 台灣代理商 - 宸泰有限公司(Jointech Inc.)
+ 宸泰有限公司(Jointech Inc.)
+ 官網: https://www.jointech.com.tw/
+ 產品相關連結:
  + https://www.jointech.com.tw/web/product/product_in.jsp?dm_no=DM1614842114731&subdm_no=DM1614842160730&pd_no=PD1653557732603&lang=tw

### RUT200
+ 特色:
  + 4G (LTE) – Cat 4 up to 150 Mbps
  + Wireless mode	IEEE 802.11b/g/n, Access Point (AP), Station (STA)
  + 1 x WAN port (can be configured to LAN), 10/100 Mbps
  + 1 x LAN port, 10/100 Mbps
  + Operating system	RutOS (OpenWrt based Linux OS)
  + Input voltage range	9 – 30 VDC, reverse polarity protection, surge protection >33 VDC 10us max
  + Power consumption	< 6.5 W Max
  + SIM	1 x SIM slot (Mini SIM – 2FF), 1.8 V/3 V, external SIM holder
  + Antennas	2 x SMA for LTE, 1 x RP-SMA for WiFi antenna connectors
  + Operating temperature	-40 °C to 75 °C
  ```
  重點:
    1. 工業級工作溫度
    2. 電源吃9至30V DC，功耗小於 6.5 W。但是要注意，連接頭比較特殊不是很好找，要另外找來DIY才能自己接線，附贈的是直接做在變壓器上。
    3. 兩個RJ45，都沒帶燈看不出有沒有接上去。
    4. SIM卡用的是大卡(Mini SIM)，需要用迴紋針頂出。
    5. 燈號很不清楚，戶外大概都看不到。
    6. 只買路由器不會附DIN軌之類的固定配件，要另外買。
    7. 買路由器附贈的天線是短的，延長天線要另外買。  
  ```

### 快速安裝
+ 準備好迴紋針，在野外忘記帶就找鑰匙圈上的鐵環。
+ 準備好SIM卡(大卡，或稱Mini SIM)。
+ 把迴紋針頂進去SIM卡槽旁邊的卡槽按鈕，讓SIM卡卡槽退出。
+ 按照卡槽防呆方向放置SIM卡到卡槽中。
+ 把卡槽插回去
+ 安裝天線，共三隻。請依照天線名稱接到正確的位置。
+ 插上電源
  + 所有燈號:2G,3G,4G,#1,#2,#3,#4,#5
  + 開機的時候:
    + 全部恆亮
    + 2G,3G,4G均滅，#1,#2,#3,#4,#5一起慢閃 -> 開機約60秒。
    + 2G,3G,4G輪播，#1,#2,#3,#4,#5均滅
+ 如果有必要，先回復原廠設定。
  + 用迴紋針長按天線旁的RESET按鈕超過五秒後放開(大概按著十秒)，系統將回復出廠設定。
  + 2G,3G,4G,#1,#2,#3,#4,#5
  + 如果成功，等重開機完後會看到熟悉的SSID，可以用機身上的密碼登入。喵的不知道為什麼一定要用WIFI登入。
  + 看密碼太麻煩，所以改用LAN連線。LAN是右邊數來第二個孔，比較靠近中間SIM卡的孔。
  + 接上之後，預設的區域網路為192.168.1.x。路由器是192.168.1.1。
