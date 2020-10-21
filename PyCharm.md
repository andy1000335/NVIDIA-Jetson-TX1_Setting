# PyCharm 安裝與使用

## 安裝
1. [下載](https://www.jetbrains.com/pycharm/download/#section=linux)
2. 解壓縮
3. 進入 ```pycharm-2018.1.4/bin```
    ```
    $ cd Download/pycharm-professional-2020.2.3/pycharm-2020.2.3/bin
    ```
4. 安裝
    ```
    $ sh ./pycharm.sh
    ```
5. 選擇 Evaluate for free -> Evaluate 
### 安裝時若出現 JDK error
```
No JDK found. Please validate either PYCHARM_JDK, JDK_HOME or 
JAVA_HOME environment variable points to valid JDK installation.
```
按以下步驟安裝 JDK  
1. 下載 JDK8
    ```
    $ sudo apt-get install openjdk-8-jdk
    ```
2. 查看路徑位置
    ```
    $ sudo update-alternatives --config java
    ```
    ```
    There is only one alternative in link group java (providing /usr/bin/java):
    /usr/lib/jvm/java-8-openjdk-arm64/jre/bin/java
    ```
3. 開啟 ```/etc/profile``` 設定環境變數 ```JAVA_HOME```
    ```
    $ sudo gedit /etc/profile
    ```
    在最後加上 ```export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-arm64```  
4. 啟用環境變數
    ```
    $ source /etc/profile
    ```

## 進入虛擬環境
1. 建立 Python Project
2. 選擇 Existing interpreter 進入已建立的虛擬環境
3. 選擇 Conda Environment
4. 選擇 Conda 虛擬環境位置 (```Anaconda安裝目錄/envs/Conda環境名字/bin/python3```)
5. Create
