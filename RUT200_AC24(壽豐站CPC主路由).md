# RUT200_AC24(壽豐站CPC主路由)
+ 更新韌體至RUT2M_R_00.07.06
  + 拿到機器預載的是RUT2M_R_00.07.04.5
  + 不要插SIM卡更新韌體比較順
  + 若要從7.6之後的版本(例如:RUT2M_R_00.07.07.3)降級回RUT2M_R_00.07.06，建議先降到RUT2M_R_00.07.04.5再升上RUT2M_R_00.07.06。
+ 從網頁進行恢復原廠設設定
  + 若WIFI訊號異常，把電源拔掉一陣子再裝上就好了。
+ 預設資訊:
  + WIFI SSID=RUT200_AC24
  + WIFI PASSWORD=f8NKu65R
  + USERNAME=admin
  + PASSWORD=Ya4d0VDf

### 恢復出廠設定後，用預設密碼登入
+ 管理員密碼設定: 方案A

### 略過Setup Wizard
+ 自行手動修改各項參數。而非依照Setup Wizard的順序

### SIM卡設定 (Network > Mobile > General)  
+ 這台用固定IP網卡，111.70.45.124。
+ PIN碼=0000
+ 2026-03-09: 給MT壽豐站CPC主路由器使用 
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

### 改LAN設定 (Network > LAN)
+ BASIC模式下
+ http://192.168.1.1/network/lan
+ 在lan後面按下edit
  + IP改為192.168.24.1
  + WAN AS LAN設定為ON
  + SAVE & APPLY 
```
注意! 至此開始，請重新取得IP，後續操作改用24網段。
```


### DHCP綁定 (Network > DHCP > Static Leases)
+ 建議先從「Status > Network > LAN」查看區域網路發佈IP位置與裝置清單來設定設備。
+ 把子路由器設定DHCP
+ 將子路由器綁好IP=192.168.24.2後再設定port forwards

### Port Forwards (Network > Firewall >Port Forwards)
+ 主路由器:
  + 記得，是設定192.168.24.1這台路由器。他的WAN是111.70.45.124。
  + RUT200_DF20_HTTP (111.70.45.124:26300->192.168.24.2:80)
  + RUT200_DF20_VPN_500 (111.70.45.124:500->192.168.24.2:500)
  + RUT200_DF20_VPN_1701 (111.70.45.124:1701->192.168.24.2:1701)
  + RUT200_DF20_VPN_4500 (111.70.45.124:4500->192.168.24.2:4500)
  + RUT200_DF20_ESP32_HTTP (111.70.45.124:26201->192.168.24.2:26200)
+ 次級路由器:
  + 記得，是設定192.168.40.1這台路由器。他的WAN是192.168.24.2。
  + ESP32_HTTP (111.70.45.124:26201->192.168.24.2:26200->192.168.40.1:26200->192.168.40.11:80)

### 實際測試建立連線時間
+ 主路由器，從開機到連線完成約要1分30秒。


