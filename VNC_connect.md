# Jetson TX1 遠端連線
- ubuntu 系統可利用 Vino 執行 VNC 遠端連線
- Jetson TX1 已內建 Vino

## Jetson TX1 設定
1. 檢查 Vino
    ```
    $ sudo apt list | grep vino
    ```
    或下載 Vino
    ```
    $ sudo apt update
    $ sudo apt install vino
    ```
2. 設定 Vino
    - 關閉啟用提示及加密
    ```
    $ gsettings set org.gnome.Vino prompt-enabled false
    $ gsettings set org.gnome.Vino require-encryption false
    ```
3. 顯示 UUID
    ```
    $ nmcli connection show
    ```
    ```
    NAME                UUID                                  TYPE      DEVICE 
    MyNet               b278433f-8ac1-4d93-b63b-f5dbe71d77ac  wifi      wlan0  
    Wired connection 1  1e608131-ae62-327e-9fba-f5866655c50d  ethernet  --
    ```
4. 填入 UUID
    - Vino 需要加入網路設備的 UUID 後才能使用
    ```
    $ dconf write /org/gnome/settings-daemon/plugins/sharing/vino-server/enabled-connections "['UUID']"
    $ export DISPLAY=:0
    ```
    - 單引號內的 ```UUID``` 為上一步所查詢到的 UUID
    - ex:
        ```
        $ dconf write /org/gnome/settings-daemon/plugins/sharing/vino-server/enabled-connections "['b278433f-8ac1-4d93-b63b-f5dbe71d77ac']"
        ```
5. 執行 server 程式
    ```
    $ /usr/lib/vino/vino-server
    ```
6. 取得 IP 位址
    - 可在 Setting 裡的 Network 查看
    - 或使用指令 ```$ ifconfig```

## 其他裝置連線設定
1. 下載 [VNC Viewer](https://www.realvnc.com/en/connect/download/viewer/)
2. 啟動並輸入 TX1 IP 位址

## Jetson TX1 開機自動執行 server
1. 在 TX1 開啟 Startup Applications
2. 新增指令 ```/usr/lib/vino/vino-server```
    - 名稱與註解可任意填寫

## 解析度設定
使用指令
```
$ sudo xrandr --fb 1920x1080
```
或修改 /etc/X11/xorg.conf 永久設定
```
Section "Screen"
    Identifier "Default Screen"
    Monitor "Configured Monitor"
    Device "Default Device"
    Subsection "Display"
        Depth 24
        Virtual 1920 1080
    EndSubsection
EndSection
```
