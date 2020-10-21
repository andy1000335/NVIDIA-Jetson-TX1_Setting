## Anaconda 安裝
1. 下載 Archiconda
    - [載點](https://github.com/Archiconda/build-tools/releases)
    - 下載 ```Archiconda3-0.2.3-Linux-aarch64.sh```
2. 到終端機下指令
    ```sh
    $ bash Archiconda3-0.2.3-Linux-aarch64.sh
    ```
3. 檢查是否安裝成功
    ```sh
    $ conda –V
    ```

#### 建立虛擬環境
```sh
$ conda create --name [name] python=[version]
```
- [name] 為虛擬環境的名稱
- [version] 為 python 版本 ex: 3.7
#### 檢視系統所有虛擬環境
```sh
$ conda env list
```
#### 啟動虛擬環境
```sh
$ source activate [name]
```
#### 離開虛擬環境
```sh
$ source deactivate
```
