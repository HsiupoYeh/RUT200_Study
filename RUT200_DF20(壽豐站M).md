# RUT200_DF20(壽豐站M)
+ M是指Metronix，使用在另一台主路由器下方的次級路由器上網(WIFI WAN模式上網)。
+ 更新韌體至RUT2M_R_00.07.06
  + 拿到機器預載的是RUT2M_R_00.07.04.5
  + 不要插SIM卡更新韌體比較順
  + 若要從7.6之後的版本(例如:RUT2M_R_00.07.07.3)降級回RUT2M_R_00.07.06，建議先降到RUT2M_R_00.07.04.5再升上RUT2M_R_00.07.06。
+ 從網頁進行恢復原廠設設定
  + 若WIFI訊號異常，把電源拔掉一陣子再裝上就好了。
+ 預設資訊:
  + WIFI SSID=RUT200_DF20
  + WIFI PASSWORD=b6W0TfLk
  + USERNAME=admin
  + PASSWORD=t3N9Azu2

### 恢復出廠設定後，用預設密碼登入
+ 管理員密碼設定: 方案A

### 略過Setup Wizard
+ 自行手動修改各項參數。而非依照Setup Wizard的順序

### SIM卡設定 (Network > Mobile > General)  
+ 這台不裝SIM卡，但SIM卡設定照樣要設。
+ 修改參數:  
  + SIM Card Settings:
    + Deny data roaming: off
    + VoLTE: off
    + Network type: 4G only
    + PIN: 0000
    + Band Selection: Auto

### RMS設定 (Services > Cloud Solutions > RMS)
+ 修改參數:
  + Connection type: Disable

### Date & Time設定 (System > Administration > Date & Time)
+ 時區為台北

### 遠端訪問路由器 (System > Administration > Access Control)
+ 開啟遠端HTTP
  
### WAN AS LAN (Network > LAN)
+ 啟用

### 改LAN設定 (Network > LAN)
+ BASIC模式下
+ http://192.168.1.1/network/lan
+ 在lan後面按下edit
  + IP改為192.168.40.1
  + WAN AS LAN設定為ON
  + SAVE & APPLY 
```
注意! 至此開始，請重新取得IP，後續操作改用40網段。
```

### WIFI WAN 的事前準備(確認主路由器資訊)
+ 確認主路由器可上網。例如: 4G上網。
+ 確認主路由器的LAN IP。例如:192.168.x.1。目前選擇x=1，即192.168.1.1。
+ 確認主路由器的SSID。
+ 確認主路由器的PASSWORD。
+ 確認主路由器的LAN IP配置規劃，要由DHCP Server配發:
  + 主路由器本身: 192.168.x.1。 目前選擇x=1，即192.168.1.1。
  + 主路由器下的次級路由器使用: 192.168.x.2。 目前選擇x=1，即192.168.1.2。
  + 主路由器下的ESP32裝置使用: 192.168.x.11。 目前選擇x=1，即192.168.1.1。
  + 主路由器下的普通用戶: 192.168.x.100~249。請依照需求調整。
```
注意!對次級路由器來說，主路由器的LAN IP就是次級路由器的WAN IP。
```

### 使用實體網路線並重新取得IP
+ 之前的設定要不要用實體網路線的有線網路都無所謂，但接下來的設定需要使用實體網路線。
+ 使用有線RJ45連線透過DHCP取得IP後繼續操作。
+ 電腦關閉WIFI。
  
### 設定Wifi用戶端(Network > Wireless > SSIDs)
+ 按下「Scan 2.4GHz」
+ 找到目標RUT200的SSID。
+ 使用其WIFI密碼登入。
+ 按下「Save & Apply」。
+ 接著可能要維持預設值按下一兩次「Save & Apply」。
```
至此，次級路由器下的用戶已經可以上網了。但建立WIFI WAN連線需要耗時較久，請等待約6分半鐘，若仍無連線請重新開機並等待6分半鐘。
```

### 檢視是否取得WAN IP (Network > WAN)
+ 觀察wifi1介面Status是否為UP，IP是否有值。一般而言，約在6分半鐘內會取得IP，若仍無連線請重新開機並再次等待6分半鐘。至此，次級路由器下的用戶已經可以上網了。

### DHCP綁定 (Network > DHCP > Static Leases)
+ 主路由器:
  + 記得，是設定192.168.1.1這台路由器。
  + 斷開與次級路由器的連線(拔掉RJ45)，用有線或無線的方式連接到主路由器，透過DHCP取得IP。
  + 建議先從「Status > Network > LAN」查看區域網路發佈IP位置與裝置清單來設定設備。
  + 原本已經把一個ESP32設定靜態IP: 192.168.1.11
  + 且也已經把一個將ESP32綁好IP後再設定port forwards
  + 再把次級路由器(本案例就是RUT200_DF20)也綁定靜態IP: 192.168.1.2。
  + 把主路由器與次級路由器重新啟動，直到確認次級路由器的WAN正在使用綁定的IP。
    + 檢視方案1: 在主路由器的用戶清單中(Status > Network LAN)
    + 檢視方案2: 在次路由器的WAN清單中(Network > WAN)
  + 接著設定port forwards
+ 次級路由器:
  + 記得，是設定192.168.40.1這台路由器。
  + 斷開與主路由器的連線，用有線或無線的方式連接到次級路由器，透過DHCP取得IP。
  + 建議先從「Status > Network > LAN」查看區域網路發佈IP位置與裝置清單來設定設備。
  + 把ESP32設定靜態IP: 192.168.40.11
  + 將ESP32綁好IP後再設定port forwards

### Port Forwards (Network > Firewall >Port Forwards)
+ 主路由器:
  + 記得，是設定192.168.1.1這台路由器。他的WAN是211.21.102.67。
  + ESP32_HTTP (211.21.102.67:26200->192.168.1.11:80)  **這個是已經有的**
  + RUT200_DF20_HTTP (211.21.102.67:26300->192.168.1.2:80)
  + RUT200_DF20_VPN_500 (211.21.102.67:500->192.168.1.2:500)
  + RUT200_DF20_VPN_1701 (211.21.102.67:1701->192.168.1.2:1701)
  + RUT200_DF20_VPN_4500 (211.21.102.67:4500->192.168.1.2:4500)
  + RUT200_DF20_ESP32_HTTP (211.21.102.67:26201->192.168.1.2:26200)
+ 次級路由器:
  + 記得，是設定192.168.40.1這台路由器。他的WAN是192.168.1.2。
  + ESP32_HTTP (192.168.1.2:26200->192.168.40.11:80)

### VPN (Service > VPN) 
+ L2TP/IPsec
  + L2TP:
    + 從「Add new instance」進行設定 (只能有一個instance)
    + New configuration name: L2TPVPN
    + Role: Server
    + 按下「Add」
    + Enable切換成ON
    + Local IP: 192.168.40.1
    + Remote IP range begin: 192.168.40.20
    + Remote IP range end: 192.168.40.30
    + User 按下 Add
    + Username: cgrg
    + Password: 45002931
    + Save & Apply
  + IPsec:
    + 從「Add new instance」進行設定 (只能有一個instance)
    + New configuration name: IPsecVPN
    + 按下「Add」
    + Enable切換成ON
    + Pre shared key* : 45002931
    + Type : Transport
    + Bind to : L2TPVPN
    + Save & Apply

### 排程
+ 查看目前排程，兩種方法都可以試試看
```
cat /etc/crontabs/root
```
```
crontab -l
```

+ 清空所有排程
```
echo "" > /etc/crontabs/root
```

+ 每小時奇數分鐘執行: RUT200狀態 (命令太長，利用echo -n 寫入不代換行字元的文字拆分兩次寫入，最後一次不需要-n)
```
echo -n "1,3,5,7,9,11,13,15,17,19,21,23,25,27,29,31,33,35,37,39,41,43,45,47,49,51,53,55,57,59 * * * * echo -n 'curl https://cgrg.synology.me/RUT200_DF20/write_rut200_log.php?rut200_log=%7B%22From%22:%22RUT200%22,%22To%22:%22RemoteServer%22,%22uptime_sec%22:%22' > /tmp/cmd.sh " >> /etc/crontabs/root
```
```
echo "&& echo -n \$(cat /proc/uptime | awk '{print \$1}') >> /tmp/cmd.sh && echo -n '%22,%22temperature%22:%22' >> /tmp/cmd.sh && gsmctl -c > /tmp/temperature && cat /tmp/temperature | tr -d '\n' >> /tmp/cmd.sh && echo -n '%22%7D' >> /tmp/cmd.sh && sh /tmp/cmd.sh " >> /etc/crontabs/root
```

+ 每小時偶數分鐘執行: RUT200狀態
```
echo "0,2,4,6,8,10,12,14,16,18,20,22,24,26,28,30,32,34,36,38,40,42,44,46,48,50,52,54,56,58 * * * * echo -n 'curl https://cgrg.synology.me/RUT200_DF20/write_esp32s_log.php?esp32s_log=' > /tmp/cmd.sh && curl -s 192.168.1.11/info > /tmp/mppt_info.txt && sed -i 's/\"/%22/g' /tmp/mppt_info.txt && sed -i 's/{/%7B/g' /tmp/mppt_info.txt && sed -i 's/}/%7D/g' /tmp/mppt_info.txt && cat /tmp/mppt_info.txt | tr -d '\n' >> /tmp/cmd.sh && sh /tmp/cmd.sh" >> /etc/crontabs/root
```

---

# 以下是不採用的設定

### 中繼的事前準備(確認主路由器資訊)
+ 確認主路由器可上網。例如: 4G上網。
+ 確認主路由器的LAN IP。例如:192.168.x.1。目前選擇x=40，即192.168.40.1。
+ 確認主路由器的SSID。
+ 確認主路由器的PASSWORD。
+ 確認主路由器的LAN IP配置規劃，要由DHCP Server配發:
  + 主路由器本身: 192.168.x.1
  + 中繼路由器使用範圍: 192.168.x.2~5。 目前選擇x=40，即192.168.40.1。
  + ESP32裝置使用範圍: 192.168.x.11~20
  + 普通用戶: 192.168.x.100~249。請依照需求調整。
```
注意!對中繼路由器來說，主路由器的LAN IP就是中繼路由器的WAN IP。
```

### 使用實體網路線並自行設定IP
+ 之前的設定要不要用實體網路線的有線網路都無所謂，但接下來的設定需要使用實體網路線。
+ 使用有線RJ45連線並且不依賴DHCP伺服器，以利後續操作順利。
+ 電腦關閉WIFI。
+ 中繼路由器維持原本LAN IP: 192.168.1.1。用戶電腦自行設定電腦IP為192.168.1.100。
  
### 安裝中繼(Relay Configuration)套件
+ 安裝了才會有需要的設定頁面
+ 使用上傳檔案的方式安裝，檔案下載位置:
  + https://wiki.teltonika-networks.com/view/RUT200_Package_Downloads#RUT2M_R_00.07.06
  + 直接下載連結位置: https://firmware.teltonika-networks.com/7.6/RUT2M/RUT2M_R_00.07.06_Packages.tar.gz
  + 從裡面找到「relay_configuration.tar.gz」，只需要上傳此檔案進行安裝。

### 設定Wifi用戶端(Network > Wireless > SSIDs)
+ 按下「Scan 2.4GHz」
+ 找到目標RUT200的SSID。
+ 使用其WIFI密碼登入。
+ 按下「Save & Apply」。
+ 接著可能要維持預設值按下一兩次「Save & Apply」。
```
至此，已經可以上網了。但還是在NAT後面而非中繼。
```

### 設定中繼模式參數(Network > Wireless >Relayd)
+ Enabled設為ON
+ Interface設為lan
+ Wireless interface設為wifi1
+ 按下「Save & Apply」。

### 關閉DHCP伺服器(Network > LAN)
+ 關閉
```
注意: 這台路由器沒有DHCP，所以要牢記其LAN IP，並且連接他的裝置要自行設定IP。
```

### 電腦IP改回DHCP
+ 將192.168.1.100改回自動取得IP。
+ 也可以開啟WIFI。
```
注意! 此時應該配到的IP是192.168.40.x。不再是192.168.1.x。若是，表示中繼設定成功。
此時，雖然配到的IP是192.168.40.x，但直接連到中繼路由器的用戶，包含WIFI與有線網路，仍然可以由192.168.1.1訪問中繼路由器的LAN。
但是直接連到主路由器的用戶，雖然也是配到192.168.40.x，但卻無法訪問192.168.1.1。
```

### 設定主路由器的DHCP綁定 (Network > DHCP > Static Leases)
+ 記得，是設定192.168.40.1這台路由器。
+ 建議先從「Status > Network > LAN」查看區域網路發佈IP位置與裝置清單來設定設備。
+ 原本已經把一個ESP32設定靜態IP: 192.168.40.11
+ 且也已經把一個將ESP32綁好IP後再設定port forwards
+ 第二台ESP32也用相同邏輯設定IP，IP將是192.168.40.12。
+ 中繼路由器(本案例就是RUT200_DF20)也綁定靜態IP: 192.168.40.2。
+ 接著設定port forwards

### Port Forwards (Network > Firewall >Port Forwards)
+ 主路由器:
  + ESP32_11_HTTP (211.21.102.67:26200->192.168.40.11:80)  **這個是已經有的**
  + ESP32_12_HTTP (211.21.102.67:26201->192.168.40.2:26201)
  + RUT200_DF20_HTTP (211.21.102.67:26300->192.168.40.2:80)
+ 中繼路由器:
  + ESP32_12_HTTP (192.168.40.2:26201->192.168.40.12:80)

### 實際測試建立連線時間
+ 當主路由器存在時，從開機到連線完成約要6分30秒。
