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

### 預先準備
+ 觀察機身正面，找到預設資訊:
  + 本範例:路由器預設IP=192.168.1.1
  + 本範例:路由器預設管理帳號密碼=admin/admin01
    ```
    所有產品幾乎都是這個內容，這些資訊被其他人知道也沒關係。
    ```
+ 觀察機身背面，找到預設資訊:
  + 本範例:WIFI SSID=RUT200_7974
  + 本範例:WIFI PASSWORD=d0X1Wtz3
    ```
    這設定被其他人知道也不會造成路由器的安全問題，只是讓附近的人能登入WIFI網路，可以耗用流量以及訪問區網內設備。  
    真的要防範惡意訪問WIFI，請自行修改密碼並貼在機身上，以利維修檢測者登入。
    ```
+ 路由器管理帳號:
  + 一般狀況下不能修改，必為:admin
+ 路由器管理密碼:
  + A:開發階段修改密碼為:「RUT200_」+「admin01」=「RUT200_admin01」
  + B:以產品序號區分修改密碼為=「RUT200_7974」+「admin01」=「RUT200_7974admin01」
  ```
  SSID加上預設管理密碼=「RUT200_7974」+「admin01」=「RUT200_7974admin01」。
  ```
  + C:以管理人區分修改密碼為:「RUT200_」+「hsiupoyeh」=「RUT200_hsiupoyeh」
  ```
  名字也可以是大小寫混雜、注音符號、統一編號等等...
  ```
+ 插上電源，等待3-5分鐘，應該LAN或WIFI要有反應，嘗試使用LAN或WIFI取得利用DHCP取得IP。依照分配IP找到管理頁面網址，並使用路由器管理帳號密碼嘗試登入。若登入成功即可從網頁確認韌體版本。
```
對這步驟有理解困難的人請參閱原廠說明書，了解常見路由器網頁管理操作方式。
```  
+ 如果拿到的設備不是出廠狀態或忘記帳號密碼無法登入管理頁面，請使用RESET按鈕恢復原廠設定。常見的恢復方法如下:  
  + 準備一個手機計時器，能看秒數的，等下需要看秒數在指定時間放開按鈕。
  + 出廠預設的RESET按鈕的規定如下:
    + 長按未達5秒=重開機
    + 長按6-11秒=清除使用者設定
    + 長按12-20秒=恢復原廠設定
    + 超過20秒=沒有事情發生
    ```    
    基本上利用清除使用者設定就會將路由器管理密碼恢復為機身上的預設值，初次登入會強制要求修改。  
    新路由器管理密碼請參考前述A、B、C方案。
    這個操作不會刪掉SIM卡的PIN碼。  
    此外，為了避免日後忘記，不建議修改RESET按鈕的規定，若有修改請務必留存設定值。  
    ```
  + 具體操作方式(長按6-11秒):
    + 用迴紋針長按天線旁的RESET按鈕，按住之後LED燈會逐個增加燈號，一秒加一個，最多加到滿5個，參考手邊準備的時鐘，秒數到第7秒時放開，系統將清除使用者設定。
    + 接著使用機身上預設帳號密碼登入路由器管理頁面。
    + 會被要求改密碼。請從前面所述的密碼挑一個方案設定，我是建議優先用A，全都事情做完再改B或C。
    + 使用改好的密碼重新登入。
    + 從網頁system/maintenance/backup找到Restore to factory default 的按鈕「Restore」。
    ```
    注意，這個操作不會刪掉SIM卡的PIN碼。但路由器管理密碼恢復為機身上的預設值，初次登入會強制要求修改。  
    新路由器管理密碼請參考前述A、B、C方案。  
    這也造成了會用預設的方式上網。也就是WAN有接上DHCP他也會上網，SIM卡有插入剛好PIN碼符合也會上網。  
    因此不想要PIN碼有效請在恢復原廠設定前把PIN碼改為空白。再按下恢復原廠設定的網頁按鈕。  
    ```
+ 因為拿到手的路由器當時出廠可能是舊版韌體，這部分造成網頁排板與功能設定上稍有不同，後續操作指引是以目前最新韌體(RUT2M_R_00.07.06)說明。
  + 最新韌體: RUT2M_R_00.07.06_WEBUI.bin
    + 韌體說明: https://wiki.teltonika-networks.com/view/RUT200_Firmware_Downloads#RUT2M_R_00.07.06_.7C_2023.12.20
    + 韌體下載連結: https://firmware.teltonika-networks.com/7.6/RUT2M/RUT2M_R_00.07.06_WEBUI.bin
+ 韌體更新方式包含:
  + 由路由器管理網頁連到伺服器線上更新(需要網路)
  + 自行準備韌體檔案並由路由器管理網頁上傳更新(不需要網路)
  + 自行準備韌體檔案並由bootloader網頁上傳更新(不需要網路)
+ 注意事項:
  + 不會更新的人請參考原廠說明書。但正常從網頁找一下韌體的頁面照著操作就能成功。
  + 一般狀況下，韌體更新可選擇保留原設定。即使選擇不保留，SIM卡的PIN碼也仍會保留。
  + 更新韌體完成後，建議再次恢復原廠設定後再重新設定各項內容。建議從網頁進行恢復原廠設定。
    + 從網頁system/maintenance/backup找到Restore to factory default 的按鈕「Restore」。
      
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
+ 確認韌體版本，這份文件是一開始在｢RUT2M_R_00.07.02.3」版本下操作。
+ 插入SIM卡後，唯一要改變的就是把pin碼改為0000。在「NETWORK>MOBILE>GENERAL」裡的「SIM CARD SETTINGS」的「PIN」設為「0000」

```
echo "*/2 * * * * echo -n 'curl https://cgrg.synology.me/RUT200_7974/write_log.php?value01=uptime' > /tmp/cmd.sh && echo -n \$(cat /proc/uptime | awk '{print \$1}') >> /tmp/cmd.sh && echo -n 'sec' >> /tmp/cmd.sh && sh /tmp/cmd.sh" > /etc/crontabs/root

```
