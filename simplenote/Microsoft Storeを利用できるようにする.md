 Microsoft Storeを利用できるようにする
2020-05-31

Rem -----------------------------------------------------------
Rem Microsoft Storeを利用できるようにするバッチファイル
Rem DoNotConnectToWindowsUpdateInternetLocationsが"0"で利用可能
Rem 管理者での実行が必要
Rem -----------------------------------------------------------

reg add HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\WindowsUpdate /v DoNotConnectToWindowsUpdateInternetLocations /t REG_DWORD /d 0 /f
timeout 30
