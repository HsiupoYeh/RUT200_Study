# RUT200_C85E
+ 更新韌體至RUT2M_R_00.07.06
  + 拿到機器預載的是RUT2M_R_00.07.04.5
  + 不要插SIM卡更新韌體比較順
  + 若要從7.6之後的版本(例如:RUT2M_R_00.07.07.3)降級回RUT2M_R_00.07.06，建議先降到RUT2M_R_00.07.04.5再升上RUT2M_R_00.07.06。
+ 從網頁進行恢復原廠設設定
  + 若WIFI訊號異常，把電源拔掉一陣子再裝上就好了。
+ 修改參數:
  + Mobile->General->SIM Card Settings:
    + Deny data roaming: off
    + VoLTE: off
    + Network type: 4G only
    + PIN: 0000
    + Band Selection: Auto
  + Service->Cloud Solutions->RMS->RMS Settings:
    + Connection type: Disable
+ 預設資訊:
  + WIFI SSID=RUT200_CADB
  + WIFI PASSWORD=6DJm8d3
  + USERNAME=admin
  + PASSWORD=Re31HqXm

+ 電信業者
  + 查看: http://192.168.1.1/status/network/mobile/1-1
    ```
    Mobile country code  466  -> 466=台灣 
    Mobile network code  89  -> 89=台灣之星
    ```

+ 修改LAN設定
  + BASIC模式下
  + http://192.168.1.1/network/lan
  + 在lan後面按下edit
    + IP改為192.168.40.1
    + WAN AS LAN設定為ON
    + SAVE & APPLY 
