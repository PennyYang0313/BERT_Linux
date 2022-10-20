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
sudo apt install python3-pip
pip install everything BERT needs
cp /mnt/c/Users/User.DESKTOP-ESIMPBC/no_time.py /tmp/pycpu/

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
