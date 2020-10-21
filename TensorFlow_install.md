# TensorFlow 安裝

1. 安裝 TensorFlow 所需系統軟體
    ```
    $ sudo apt-get update
    $ sudo apt-get install libhdf5-serial-dev hdf5-tools libhdf5-dev zlib1g-dev zip libjpeg8-dev liblapack-dev libblas-dev gfortran
    ```
2. 進入虛擬環境
    ```
    $ source activate tensorflowVE
    ```
3. 安裝 Python 包依賴
    ```
    $ pip install -U numpy==1.16.1 future==0.18.2 mock==3.0.5 h5py==2.10.0 keras_preprocessing==1.1.1 keras_applications==1.0.8 gast==0.2.2 futures protobuf pybind11
    ```
4. 安裝 TensorFlow
    ```
    $ pip install --pre --extra-index-url https://developer.download.nvidia.com/compute/redist/jp/$JP_VERSION tensorflow
    ```
    - ```$JP_VERSION```：JetPack 版本
        - JetPack 4.2.2：42
        - JetPack 3.3.1：33
    - 安裝 TensorFlow 1.x  
      ```$ pip install --pre --extra-index-url https://developer.download.nvidia.com/compute/redist/jp/v44 ‘tensorflow<2’```
    - 安裝 TensorFlow 特定版本  
      ```$ pip install --extra-index-url https://developer.download.nvidia.com/compute/redist/jp/v$JP_VERSION tensorflow==$TF_VERSION+nv$NV_VERSION```
        - ```$JP_VERSION```：JetPack 版本
        - ```$TF_VERSION```：TensorFlow 版本
        - ```NV_VERSION```：TensorFlow 的 NVIDIA container 版本

    ex：  
    ```$ pip install --extra-index-url https://developer.download.nvidia.com/compute/redist/jp/v42 tensorflow-gpu==1.13.1+nv19.3```

## 測試
```python
import tensorflow as tf

print(tf.__version__)                # 查看 TensorFlow 版本
print(tf.test.is_gpu_available())    # 是否有使用到 GPU
```
