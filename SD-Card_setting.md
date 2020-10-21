# SD 卡配置
1. 查看 SD 卡
    ```
    $ sudo fdisk -l
    ```
    ```
    Disk /dev/mmcblk2: 59.7 GiB, 64088965120 bytes, 125173760 sectors
    Units: sectors of 1 * 512 = 512 bytes
    Sector size (logical/physical): 512 bytes / 512 bytes
    I/O size (minimum/optimal): 512 bytes / 512 bytes
    Disklabel type: dos
    Disk identifier: 0xf4a39f5e

    Device         Boot Start       End   Sectors  Size Id Type
    /dev/mmcblk2p1       2048 125171711 125169664 59.7G  7 HPFS/NTFS/exFAT
    ```
2. 卸載 SD 卡
    ```
    $ umount /dev/mmcblk2p1
    ```
3. 格式化 SD 卡為 ext4 格式
    ```
    $ sudo mkfs.ext4 /dev/mmcblk2p1
    ```
4. 掛載 SD 卡至指定分區
    ```
    $ sudo mkdir /media/nvidia/SD
    $ sudo mount /dev/mmcblk2p1 /media/nvidia/SD
    ```
5. 複製根目錄內容至 SD 卡
    ```
    $ sudo cp -ax / /media/nvidia/SD
    ```
6. 進入 SD 卡
    ```
    $ cd /media/nvidia/SD
    ```
7. 備份並修改 extlinux.conf
    ```
    $ cd boot/extlinux
    $ sudo cp extlinux.conf extlinux.conf.original
    $ sudo gedit extlinux.conf
    ```
    - DEFAULT 由 primary 改為 sdard
        - ```DEFAULT sdcard```
    - root 由 /dev/mmcblk0p1 改為 /dev/mmcblk2p1
        - ```root=/dev/mmcblk2p1```
    ```
    TIMEOUT 30
    DEFAULT sdcard

    MENU TITLE L4T boot options

    LABEL sdcard
    MENU LABEL SD Card
    LINUX /boot/Image
    INITRD /boot/initrd
    APPEND ${cbootargs} quiet root=/dev/mmcblk2p1 rw rootwait rootfstype=ext4 console=ttyS0,115200n8 console=tty0 fbcon=map:0 net.ifnames=0 sdhci_tegra.en_boot_part_access=1 
    ```
8. 重新啟動 TX1
9. 驗證
    ```
    $ df
    ```
    ```
    Filesystem     1K-blocks     Used Available Use% Mounted on
    /dev/mmcblk2p1  61339452 11912016  46281812  21% /
    none             1780572        0   1780572   0% /dev
    tmpfs            2025104        4   2025100   1% /dev/shm
    tmpfs            2025104    20100   2005004   1% /run
    tmpfs               5120        4      5116   1% /run/lock
    tmpfs            2025104        0   2025104   0% /sys/fs/cgroup
    tmpfs             405020       16    405004   1% /run/user/120
    tmpfs             405020      112    404908   1% /run/user/1000
    /dev/mmcblk0p1  14384136 11900020   1733732  88% /media/nvidia/09989c5f-eabd-4fff-b992-98e51362873e
    ```
    - ```/dev/mmcblk2p1``` 已成為主要分區啟動
