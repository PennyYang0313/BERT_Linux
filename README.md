# BERT_Linux version
## 環境
### 系統
Ubuntu 18.04（WSL）
### Anaconda
 * [64-Bit (x86) Installer (659 MB)](https://repo.anaconda.com/archive/Anaconda3-2022.05-Linux-x86_64.sh)
 * Update APT Package & Install cURL
```
sudo apt update 
sudo apt upgrade
sudo apt install curl
```
  * Download
```
cd /tmp
curl https://repo.anaconda.com/archive/Anaconda3-2022.05-Linux-x86_64.sh --output anaconda.sh
```
  * Install
```
bash anaconda.sh
```
Enter > Ctrl+C > yes(Continue) > ENTER to confirm the location > Finish installation > yes(Initialize)

```
source ~/.bashrc
conda info
conda env list
```
#### Environment for BERT (only cpu)
  * 建構 & 進入虛擬環境
```
conda create --name pycpu python==version
conda activate pycpu
```
  * Install pytorch  

[Version](https://pytorch.org/get-started/locally/)
```
conda install pytorch torchvision torchaudio cpuonly -c pytorch
```
#### Transformer
```
conda install -c huggingface transformers
conda install -c fastai accelerate
conda install datasets
conda install memory_profiler
conda install -c conda-forge prettytable
conda install scikit-learn
```

```
cd /mnt/c/Users/User.DESKTOP-ESIMPBC
```

#### Error
1. libssl.so.10: cannot open shared object file
  1. can't install
  
  Edit the source list to add the following line
  ```
   sudo nano /etc/apt/sources.list
  ```
  "deb http://security.ubuntu.com/ubuntu xenial-security main"
  
  Then 
  ```
  sudo apt update 
  sudo apt install libssl1.0.0
  cd /usr/lib/x86_64-linux-gnu
  sudo ln -s libssl.so.1.0.0 ~/anaconda3/envs/pycpu/lib/libssl.so.10
  sudo ln -s libcrypto.so.1.0.0 ~/anaconda3/envs/pycpu/lib/libcrypto.so.10
  sudo ln -s libssl.so.1.0.0 /tmp/libssl.so.10
  sudo ln -s libcrypto.so.1.0.0 /tmp/libcrypto.so.10
  ```
### No Anaconda
``` 
sudo apt-get update
sudo apt-get upgrade
sudo apt install python3-pip
cp /mnt/c/Users/User.DESKTOP-ESIMPBC/no_time.py /tmp/pycpu/
```

### pip install everything BERT needs
```
pip install torch 
pip install memory_profiler
pip install datetime
pip install tqdm
pip install prettytable
pip install datasets
pip install accelerate
pip install transformers
pip install scipy sklearn
pip install sklearn
python3 -m pip install scikit-learn
```
change transformers
```
cd ~/.local/lib/python3.8/site-packages
cp /mnt/c/Users/User.DESKTOP-ESIMPBC/anaconda3/envs/pycpu/Lib/site-packages/transformers/models/bert/modeling_bert.py ~/.local/lib/python3.8/site-packages/transformers/
```
   
   
### Linux make ramdisk
```
sudo -i
mkdir /tmp/ramdisk
chmod 777 /tmp/ramdisk
mount -t tmpfs -o size=8G tmpfs /tmp/ramdisk/
df -h
```
### re-mount degubfs (如果找不到 /sys/kernel/debug)
```
sudo  mount -t debugfs none /sys/kernel/debug
```

### stat
```
nohup vmstat 5 60| (while read; do echo "$(date +%d-%m-%Y" "%H:%M:%S) $REPLY"; done) >> /tmp/pycpu/vmstat_output.log
```

### Bert Libotrch version

 * [Cmake](https://pytorch.org/tutorials/advanced/cpp_export.html) 
```
sudo apt install cmake
mkdir /tmp/example-app
cp /mnt/c/Users/User.DESKTOP-ESIMPBC/example-app/example-app.cpp /tmp/example-app/
cp /mnt/c/Users/User.DESKTOP-ESIMPBC/example-app/CMakeLists.txt /tmp/example-app/

cd /tmp/example-app
mkdir build
cd build
cmake -DCMAKE_PREFIX_PATH=/tmp/libtorch .. (if error >>> sudo apt-get update && sudo apt-get install -y build-essential)
cmake --build . --config Release
```
* Bert model for torch script
```
cp /mnt/c/Users/User.DESKTOP-ESIMPBC/bert.py /tmp/pycpu/
cd /tmp/pycpu/

sudo apt install python3-pip
pip3 install torch torchvision torchaudio --extra-index-url https://download.pytorch.org/whl/cpu
pip install pytorch_pretrained_bert
python3 bert.py (跑出pt檔)
```

* Exec
```
cd /tmp/example-app/build
(改bert code) cp /mnt/c/Users/User.DESKTOP-ESIMPBC/bert.py /tmp/pycpu/
(改c++) cp /mnt/c/Users/User.DESKTOP-ESIMPBC/example-app/example-app.cpp /tmp/example-app/
make
./example-app /tmp/pycpu/traced_bert.pt
```

* test
```
cp /mnt/c/Users/User.DESKTOP-ESIMPBC/bert_libtorch.py /tmp/pycpu/
cp /mnt/c/Users/User.DESKTOP-ESIMPBC/example-app/example-app.cpp /tmp/example-app/
cd /tmp/pycpu/
python3 bert_libtorch.py
cd /tmp/example-app/build/
make
./example-app /tmp/pycpu/script_model.pt
```

* backward
```
bertmodel backward ?
有loss才有backward?
```
