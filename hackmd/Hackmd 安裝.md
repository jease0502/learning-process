# Hackmd 安裝
---
## 環境
- linux bash

## 安裝
在安裝前先進入```su```模式吧~
```cmake
su
```
然後她會教你輸入密碼，當然密碼忘記了可以用下面指令重設
```cmake
sudo passwd root
```

### 安裝相依套件
```cmake
[root@hackmd ~] yum install curl git
```
### 安裝 nodejs & npm
```cmake
[root@hackmd ~] yum install epel-release
[root@hackmd ~] yum install nodejs npm node-gyp  gcc gcc-c++
```
當然你有可能失敗，如果失敗式式下面的
```cmake
sudo apt-get install nodejs
sudo apt-get install npm
```
### clone hackmd git
```cmake
[root@hackmd ~] cd /opt
[root@hackmd ~] git clone https://github.com/hackmdio/hackmd.git
```

### 安裝 hackmd
如果你家網路不夠快的話，他需要跑一陣子
```cmake
[root@hackmd ~] cp config.json.example config.json
[root@hackmd ~]# bin/setup
```
如果出現```yarn: error: no such option: --pure-lockfile```這句error的話，可以用下面方法排除，排除後再安裝一遍即可
```cmake
apt install cmdtest
npm install --global yarn
```

### 安裝 mysql 5.6.38-2.el7
```cmake
[root@hackmd ~] rpm -Uvh http://dev.mysql.com/get/mysql-community-release-el7-5.noarch.rpm
[root@hackmd ~] yum install mysql-community-server
[root@hackmd ~] systemctl start mysqld
[root@hackmd ~] /usr/bin/mysql_secure_installation   #設定帳密
```