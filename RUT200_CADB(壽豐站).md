# RUT200_CADB
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


### 管理員密碼設定
+ 方案A

### 改LAN設定
  + BASIC模式下
  + http://192.168.1.1/network/lan
  + 在lan後面按下edit
    + IP改為192.168.40.1
    + WAN AS LAN設定為ON
    + SAVE & APPLY 
### 修改參數:
+ Mobile->General->SIM Card Settings:
  + Deny data roaming: off
  + VoLTE: off
  + Network type: 4G only
  + PIN: 0000
  + Band Selection: Auto
+ Service->Cloud Solutions->RMS->RMS Settings:
  + Connection type: Disable

### SIM卡設定 (Network > Mobile > General)
+ 用固定IP網卡，211.21.102.67。
+ PIN碼=0000
+ 2025-07-07: 給MT壽豐站使用 

### 電信業者
+ 查看「Status」>「Network」>「Mobile」: http://192.168.1.1/status/network/mobile/1-1
  ```
  Mobile country code  466  -> 466=台灣 
  Mobile network code  92  -> 92=中華電信
  ```

### RMS設定 (Services > Cloud Solutions > RMS)
+ 關閉

### Date & Time設定 (System > Administration > Date & Time)
+ 時區為台北

### 遠端訪問路由器 (System > Administration > Access Control)
+ 開啟遠端HTTP
  
### WAN AS LAN (Network > LAN)
+ 啟用


### DHCP綁定 (Network > DHCP > Static Leases)
+ 建議先從「Status > Network > LAN」查看區域網路發佈IP位置與裝置清單來設定設備。
+ 把ESP32設定靜態IP: 192.168.40.11
+ 將ESP32綁好IP後再設定port forwards

### Port Forwards (Network > Firewall >Port Forwards)
+ ESP32_HTTP (26200->80)



### VPN (Service > VPN)
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

### 橋接
https://wiki.teltonika-networks.com/view/RUTOS_relay_/_Wi-Fi_extender_/_repeater_/_bridge_configuration
