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
    + 測試資訊可參考: https://wiki.teltonika-networks.com/view/RUT200_Power_Consumption
    + 使用9V最省電，電壓越高越不省電。可見內建支援9-30V是降壓到9V，轉換有耗損，但差異應該算小。
    + 待機大約1.31W(12V109mA)，高負載可達3.82W(12V318mA)。
  + SIM	1 x SIM slot (Mini SIM – 2FF), 1.8 V/3 V, external SIM holder
  + Antennas	2 x SMA for LTE, 1 x RP-SMA for WiFi antenna connectors
  + Operating temperature	-40 °C to 75 °C
  ```
  重點:
    1. 工業級工作溫度
    2. 電源吃9至30V DC，功耗小於 6.5 W。但是要注意，電源連接頭比較特殊不是很好找，要另外找來DIY才能自己接線，附贈的是直接做在變壓器上。
    3. 兩個RJ45，有帶燈但在座的下面很小一個綠點很容易被擋住看不到。亮=連接中，滅=不通，閃爍=傳資料中。
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
    此外，這個功能也不會刪掉系統的System>Maintenance>Events Log
    這個功能官方預設是用來提供給工程師錯誤排除的，內容數量太大的時候會自動刪掉舊的以避免容量繼續暴增。
    要刪掉的話可以用非官方建議之作法:  
    1. SSH into your router  
    2. Go to log folder using command: cd /log/  
    3. Run command: rm log.db  
    4. Run command: /etc/init.d/eventslog restart  
    看不懂的人就不要用了...這個記錄檔不會占用太多容量也不影響路由器運作。  
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
+ 當確認韌體版本是RUT2M_R_00.07.06後，就可以按照快速安裝來進行操作。
```
就算韌體版本不同，操作概念幾乎一致，也大概可以安裝完成，只是舊版安全性可能有疑慮。
```

### 快速安裝
+ 這是以韌體版本RUT2M_R_00.07.06的狀況下進行的安裝。
+ 準備好迴紋針，在野外忘記帶就找鑰匙圈上的鐵環。
+ 準備好SIM卡(大卡，或稱Mini SIM)。
+ 把迴紋針頂進去SIM卡槽旁邊的卡槽按鈕，讓SIM卡托盤退出。
+ 按照SIM卡托盤防呆方向放置SIM卡到托盤中。
+ 把托盤插回去卡槽中，托盤插回去的時候注意托盤側面英文字「SIM」閱讀上是正的。
+ 安裝天線，共三隻。請依照天線名稱接到正確的位置。
+ 插上電源
  + 電源連接頭下方會有一個POWER燈，亮就表示通電，滅就表示沒電。但是不知道電壓是否正確(請自行準備好符合規格的電壓)。
  + 所有燈號:2G,3G,4G,#1,#2,#3,#4,#5
  + 開機的時候:
    + 全部恆亮
    + 2G,3G,4G均滅，#1,#2,#3,#4,#5一起慢閃(一秒一次亮暗) -> 開機約60秒。
    + 開機完成後，沒插SIM卡或PIN碼錯誤的狀況下(若發生此錯誤，才會產生此燈號並持續卡在這個狀況):       
        + #1,#2,#3,#4,#5均滅，2G亮,3G亮,4G亮 -> 2G滅,3G滅,4G滅，慢閃(一秒一次亮暗) -> 不斷重複，此時可以進入管理頁面看狀態、改PIN碼等。
    + 有插SIM卡或且PIN碼正確，將開始搜尋網路營運商:       
        + #1,#2,#3,#4,#5均滅，2G亮,3G滅,4G滅 -> 2G滅,3G亮,4G滅 -> 2G滅,3G滅,4G亮 -> 不斷重複，此時可以進入管理頁面看狀態。
    + 找到網路營運商後，#1,#2,#3,#4,#5用來顯示手機訊號強度，並開始嘗試用4G訊號>3G訊號>2G訊號 :       
        + #1,#2,#3,#4,#5為手機訊號強度，2G,3G,4G擇一閃爍嘗試建立4G訊號(若失敗會繼續往下試，與管理頁面內設定有關) ->  不斷重複，此時可以進入管理頁面看狀態。
    + 手機訊號強度夠且成功建立4G訊號/3G訊號/2G訊號 :       
        + #1,#2,#3,#4,#5為手機訊號強度，2G,3G,4G擇一恆亮表示網路已通 ->  此時可以進入管理頁面看狀態。
    + 網路資料開始傳輸 :       
        + #1,#2,#3,#4,#5為手機訊號強度，2G,3G,4G擇一快速閃爍表示資料正在傳輸 ->  此時可以進入管理頁面看狀態。
+ 至此，已經可以正常使用網路。但若有需要進行設定，請繼續照後面的步驟操作。
+ 如果有必要，先回復原廠設定。恢復原廠設定仍會保存最後一次的PIN碼。如果要清掉PIN碼請先手動清掉。
  + 用迴紋針長按天線旁的RESET按鈕超過五秒後放開(大概按著十秒)，系統將回復出廠設定。
  + 2G,3G,4G,#1,#2,#3,#4,#5
  + 如果成功，等重開機完後會看到熟悉的SSID，可以用機身上的密碼登入。
  + 看密碼太麻煩，所以改用LAN連線。LAN是右邊數來第二個孔，比較靠近中間SIM卡的孔。
  + 接上之後，預設的區域網路為192.168.1.x。路由器是192.168.1.1。
  + 路由器管理頁面登入帳號為:admin，機身上有寫。
  + 初次登入會強制要求改密碼，密碼規範:
    + A password of minimum 8 characters, at least one uppercase letter, one lowercase letter and one number is accepted.
    + 採用A方案:開發階段修改密碼為:「RUT200_」+「admin01」=「RUT200_admin01」
    ```
    新路由器管理密碼請參考前述A、B、C方案。
    ```
+ 一律使用ADVANCED模式，也就是右上角MODE要顯示「ADVANCED」，若顯示BASIC就點擊一下「BASIC」就會切換為「ADVANCED」。
+ 確認韌體版本，這份文件是一開始在｢RUT2M_R_00.07.06」版本下操作。
+ 有幾個可能會考慮要設定的項目:
  + 系統時間
  + WIFI加密方法，這個韌體預設的是混和型，除非要支援舊設備，否則應該不用改。
  + Port Forwards
  +  RMS settings -> 用不到，就關掉吧...
  +  近端管理登入
  +  遠端管理登入(網頁、SSH、CLI....)
  +  IP block 設定，感覺把重開機清除啟用是個好選擇
  +  排程工作
  +  學會uci命令 (https://wiki.teltonika-networks.com/view/UCI_command_usage)
  +  學會gsmctl命令 (https://wiki.teltonika-networks.com/view/AT_Commands)

```
echo "1,3,5,7,9,11,13,15,17,19,21,23,25,27,29,31,33,35,37,39,41,43,45,47,49,51,53,55,57,59 * * * * echo -n 'curl https://cgrg.synology.me/RUT200_7974/write_log.php?value01=%7B%22uptime_sec%22:%22' > /tmp/cmd.sh && echo -n \$(cat /proc/uptime | awk '{print \$1}') >> /tmp/cmd.sh && echo -n '%22,%22temperature%22:%22' >> /tmp/cmd.sh && gsmctl -c > /tmp/temperature && cat /tmp/temperature | tr -d '\n' >> /tmp/cmd.sh && echo -n '%22%7D' >> /tmp/cmd.sh && sh /tmp/cmd.sh" > /etc/crontabs/root

```
```
echo "0,2,4,6,8,10,12,14,16,18,20,22,24,26,28,30,32,34,36,38,40,42,44,46,48,50,52,54,56,58 * * * * echo -n 'curl https://cgrg.synology.me/RUT200_7974/write_log.php?value01=' > /tmp/cmd.sh && curl -s 192.168.1.11/info > /tmp/mppt_info.txt && sed -i 's/\"/%22/g' /tmp/mppt_info.txt && sed -i 's/{/%7B/g' /tmp/mppt_info.txt && sed -i 's/}/%7D/g' /tmp/mppt_info.txt && cat /tmp/mppt_info.txt | tr -d '\n' >> /tmp/cmd.sh && sh /tmp/cmd.sh" >> /etc/crontabs/root
```



```
echo "1,3,5,7,9,11,13,15,17,19,21,23,25,27,29,31,33,35,37,39,41,43,45,47,49,51,53,55,57,59 * * * * echo -n 'curl https://cgrg.synology.me/RUT200_7974/write_rut200_log.php?rut200_log=%7B%22From%22:%22RUT200%22,%22To%22:%22RemoteServer%22,%22uptime_sec%22:%22' > /tmp/cmd.sh && echo -n \$(cat /proc/uptime | awk '{print \$1}') >> /tmp/cmd.sh && echo -n '%22,%22temperature%22:%22' >> /tmp/cmd.sh && gsmctl -c > /tmp/temperature && cat /tmp/temperature | tr -d '\n' >> /tmp/cmd.sh && echo -n '%22%7D' >> /tmp/cmd.sh && sh /tmp/cmd.sh" > /etc/crontabs/root

```
```
echo "0,2,4,6,8,10,12,14,16,18,20,22,24,26,28,30,32,34,36,38,40,42,44,46,48,50,52,54,56,58 * * * * echo -n 'curl https://cgrg.synology.me/RUT200_7974/write_esp32s_log.php?esp32s_log=' > /tmp/cmd.sh && curl -s 192.168.1.11/info > /tmp/mppt_info.txt && sed -i 's/\"/%22/g' /tmp/mppt_info.txt && sed -i 's/{/%7B/g' /tmp/mppt_info.txt && sed -i 's/}/%7D/g' /tmp/mppt_info.txt && cat /tmp/mppt_info.txt | tr -d '\n' >> /tmp/cmd.sh && sh /tmp/cmd.sh" >> /etc/crontabs/root
```

echo "" > /etc/crontabs/root

```
1,3,5,7,9,11,13,15,17,19,21,23,25,27,29,31,33,35,37,39,41,43,45,47,49,51,53,55,57,59 * * * * root  CMD1
0,2,4,6,8,10,12,14,16,18,20,22,24,26,28,30,32,34,36,38,40,42,44,46,48,50,52,54,56,58 * * * * root  CMD1
```

```
curl https://cgrg.synology.me/RUT200_7974/write_log.php?value01=%7B%22ABC%22:%22123%22%7D
```


```
curl http://cgrg.synology.m 1>log.txt 2> /dev/null
```

```
if [ $(curl http://cgrg.synology.me/CGRG 1>log.txt 2> /dev/null)==0 ]; then echo "Job OK!"; fi
if [ $(curl http://cgrg.synology.m 1>log.txt 2> /dev/null)==0 ]; then echo "Job OK!"; fi
```


+ 設定DHCP綁定裝置靜態IP:
  + 「STATUS」>「Network」>「LAN」，找到「DHCP Leases」，從清單中按下「Create static」。這裡也等於在看連線中的用戶清單。
  + 或在「Network」>「DHCP」>「Static Leases」進行設定。也可配合兩者快速操作。
+ 設定Port Forword:
  + 在「Network」>「Firewall」>「Port Forwards」進行設定。
  + 目標: http://211.21.102.70:26200/

