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
