# RUT200_CADB(壽豐站)
+ 更新韌體至RUT2M_R_00.07.06
  + 拿到機器預載的是RUT2M_R_00.07.04.5
  + 不要插SIM卡更新韌體比較順
  + 若要從7.6之後的版本(例如:RUT2M_R_00.07.07.3)降級回RUT2M_R_00.07.06，建議先降到RUT2M_R_00.07.04.5再升上RUT2M_R_00.07.06。
+ 從網頁進行恢復原廠設設定
  + 若WIFI訊號異常，把電源拔掉一陣子再裝上就好了。
+ 預設資訊:
  + WIFI SSID=RUT200_CADB
  + WIFI PASSWORD=u6DJm8d3
  + USERNAME=admin
  + PASSWORD=Re31HqXm

### 恢復出廠設定後，用預設密碼登入
+ 管理員密碼設定: 方案A

### 略過Setup Wizard
+ 自行手動修改各項參數。而非依照Setup Wizard的順序

### SIM卡設定 (Network > Mobile > General)  
+ 這台用固定IP網卡，211.21.102.67。
+ PIN碼=0000
+ 2025-07-07: 給MT壽豐站使用 
+ 修改參數:  
  + SIM Card Settings:
    + Deny data roaming: off
    + VoLTE: off
    + Network type: 4G only
    + PIN: 0000
    + Band Selection: Auto

### 電信業者
+ 查看「Status」>「Network」>「Mobile」: http://192.168.1.1/status/network/mobile/1-1
  ```
  Mobile country code  466  -> 466=台灣 
  Mobile network code  92  -> 92=中華電信
  ```

### RMS設定 (Services > Cloud Solutions > RMS)
+ 修改參數:
  + Connection type: Disable

### Date & Time設定 (System > Administration > Date & Time)
+ 時區為台北

### 遠端訪問路由器 (System > Administration > Access Control)
+ 開啟遠端HTTP
  
### WAN AS LAN (Network > LAN)
+ 啟用

### DHCP綁定 (Network > DHCP > Static Leases)
+ 建議先從「Status > Network > LAN」查看區域網路發佈IP位置與裝置清單來設定設備。
+ 把ESP32設定靜態IP: 192.168.1.11
+ 將ESP32綁好IP後再設定port forwards

### Port Forwards (Network > Firewall >Port Forwards)
+ ESP32_HTTP (211.21.102.67:26200->192.168.1.11:80)

### 實際測試建立連線時間
+ 主路由器，從開機到連線完成約要1分30秒。

### 排程
+ 查看目前排程
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

+ 每小時奇數分鐘執行: RUT200狀態
```
echo "1,3,5,7,9,11,13,15,17,19,21,23,25,27,29,31,33,35,37,39,41,43,45,47,49,51,53,55,57,59 * * * * echo -n 'curl https://cgrg.synology.me/RUT200_CADB/write_log.php?value01=%7B%22uptime_sec%22:%22' > /tmp/cmd.sh && echo -n \$(cat /proc/uptime | awk '{print \$1}') >> /tmp/cmd.sh && echo -n '%22,%22temperature%22:%22' >> /tmp/cmd.sh && gsmctl -c > /tmp/temperature && cat /tmp/temperature | tr -d '\n' >> /tmp/cmd.sh && echo -n '%22%7D' >> /tmp/cmd.sh && sh /tmp/cmd.sh" > /etc/crontabs/root
```
```
echo -n ">> /tmp/cmd.sh && echo -n '%22%7D' >> /tmp/cmd.sh && sh /tmp/cmd.sh" >> /etc/crontabs/root && echo "" >> /etc/crontabs/root
```

```
echo -n "* * * * * echo -n 'curl https://cgrg.synology.me/RUT200_CADB/write_rut200_log.php?rut200_log=%7B%22From%22:%22RUT200%22,%22To%22:%22RemoteServer%22,%22uptime_sec%22:%22' > /tmp/cmd.sh && echo -n \$(cat /proc/uptime | awk '{print \$1}') >> /tmp/cmd.sh && echo -n '%22,%22temperature%22:%22' >> /tmp/cmd.sh && gsmctl -c > /tmp/temperature && cat /tmp/temperature | tr -d '\n' >> /tmp/cmd.sh && echo -n '%22%7D' >> /tmp/cmd.sh && sh /tmp/cmd.sh" >> /etc/crontabs/root
```

```
echo "0,2,4,6,8,10,12,14,16,18,20,22,24,26,28,30,32,34,36,38,40,42,44,46,48,50,52,54,56,58 * * * * echo -n 'curl https://cgrg.synology.me/RUT200_CADB/write_esp32s_log.php?esp32s_log=' > /tmp/cmd.sh && curl -s 192.168.1.11/info > /tmp/mppt_info.txt && sed -i 's/\"/%22/g' /tmp/mppt_info.txt && sed -i 's/{/%7B/g' /tmp/mppt_info.txt && sed -i 's/}/%7D/g' /tmp/mppt_info.txt && cat /tmp/mppt_info.txt | tr -d '\n' >> /tmp/cmd.sh && sh /tmp/cmd.sh" >> /etc/crontabs/root
```


# 以下是不採用的部分
### 改LAN設定 (Network > LAN)
+ **目前停止使用**
+ BASIC模式下
+ http://192.168.1.1/network/lan
+ 在lan後面按下edit
  + IP改為192.168.40.1
  + WAN AS LAN設定為ON
  + SAVE & APPLY 

### VPN (Service > VPN) 
+ **目前停止使用**
+ L2TP/IPsec
  + L2TP:
    + 從「Add new instance」進行設定 (只能有一個instance)
    + New configuration name: L2TPVPN
    + Role: Server
    + 按下「Add」
    + Enable切換成ON
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

### 中繼設定之參考資料
+ ** 目前停止使用**
+ https://wiki.teltonika-networks.com/view/RUTOS_relay_/_Wi-Fi_extender_/_repeater_/_bridge_configuration
+ 視需求設定中繼，例如:RUT200_DF20(壽豐站M)
+ 若有需要可進一步綁定DHCP與Port Forwards。
