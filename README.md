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
+ 把迴紋針頂進去SIM卡槽旁邊的卡槽按鈕，讓SIM卡托盤退出。
+ 按照SIM卡托盤防呆方向放置SIM卡到托盤中。
+ 把托盤插回去卡槽中，托盤插回去的時候注意托盤側面英文字「SIM」閱讀上是正的。
+ 安裝天線，共三隻。請依照天線名稱接到正確的位置。
+ 插上電源
  + 所有燈號:2G,3G,4G,#1,#2,#3,#4,#5
  + 開機的時候:
    + 全部恆亮
    + 2G,3G,4G均滅，#1,#2,#3,#4,#5一起慢閃(一秒一次亮暗) -> 開機約60秒。
    + #1,#2,#3,#4,#5均滅，2G,3G,4G有燈號閃爍如下:
      + 沒插SIM卡的狀況下:
        + 2G亮,3G滅,4G滅 -> 2G滅,3G亮,4G亮，慢閃(一秒一次亮暗) -> 約11秒。
        + 2G亮,3G亮,4G亮 -> 2G滅,3G滅,4G滅，慢閃(一秒一次亮暗) -> ???秒，之後重開機???。
+ 如果有必要，先回復原廠設定。恢復原廠設定仍會保存最後一次的PIN碼。如果要清掉PIN碼請先手動清掉。
  + 用迴紋針長按天線旁的RESET按鈕超過五秒後放開(大概按著十秒)，系統將回復出廠設定。
  + 2G,3G,4G,#1,#2,#3,#4,#5
  + 如果成功，等重開機完後會看到熟悉的SSID，可以用機身上的密碼登入。喵的不知道為什麼一定要用WIFI登入。
  + 看密碼太麻煩，所以改用LAN連線。LAN是右邊數來第二個孔，比較靠近中間SIM卡的孔。
  + 接上之後，預設的區域網路為192.168.1.x。路由器是192.168.1.1。
  + 路由器管理頁面登入帳號為:admin，機身上有寫。
  + 初次登入會強制要求改密碼，密碼規範:
    + A password of minimum 8 characters, at least one uppercase letter, one lowercase letter and one number is accepted.
    + 所以開發階段密碼改為:機器背後的WIFI SSID加上預設PASSWORD。例如背後寫WIFI SSID=「RUT200_7974」，PASSWORD=「admin01」，新密碼就是「RUT200_7974admin01」。
+ 效能好像有點爛，操作realtime data 的頁面會當機重開。
+ 一律使用ADVANCED模式，也就是右上角MODE要顯示「ADVANCED」，若顯示BASIC就點擊一下「BASIC」就會切換為「ADVANCED」。
+ 確認韌體版本，這份文件是在｢RUT2M_R_00.07.02.3」版本下操作。
+ 插入SIM卡後，唯一要改變的就是把pin碼改為0000。在「NETWORK>MOBILE>GENERAL」裡的「SIM CARD SETTINGS」的「PIN」設為「0000」

+ echo "*/2 * * * * echo -n 'curl https://cgrg.synology.me/RUT200_7974/write_log.php?value01=uptime' > /tmp/cmd.sh && echo -n $(cat /proc/uptime | awk '{print $1}') >> /tmp/cmd.sh && echo -n 'sec' >> /tmp/cmd.sh && sh /tmp/cmd.sh" > /etc/crontabs/root
