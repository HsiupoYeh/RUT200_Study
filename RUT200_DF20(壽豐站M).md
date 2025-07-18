# RUT200_DF20(壽豐站M)
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
  + Mobile->General->SIM Card Settings:
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

### 中繼的事前準備(確認主路由器資訊)
+ 確認主路由器可上網。例如: 4G上網。
+ 確認主路由器的LAN IP。例如:192.168.x.1。目前選擇x=40
+ 確認主路由器的SSID。
+ 確認主路由器的PASSWORD。
+ 確認主路由器的LAN IP配置規劃:
  + 主路由器本身: 192.168.x.1
  + 第一台中繼路由器: 192.168.x.2
  + ESP32裝置使用範圍: 192.168.x.11~20
  
### 安裝中繼(Relay Configuration)套件
+ 安裝了才會有需要的設定頁面
+ 使用上傳檔案的方式安裝，檔案下載位置:
  + https://wiki.teltonika-networks.com/view/RUT200_Package_Downloads#RUT2M_R_00.07.06
  + 直接下載連結位置: https://firmware.teltonika-networks.com/7.6/RUT2M/RUT2M_R_00.07.06_Packages.tar.gz
  + 從裡面找到「relay_configuration.tar.gz」，只需要上傳此檔案進行安裝。
  + 安裝完畢請重開路由器。


### 設定Wifi用戶端(Network > Wireless > SSIDs)
+ 按下「Scan 2.4GHz」
+ 找到目標RUT200的SSID。
+ 使用其WIFI密碼登入。
