---
tags: sublime
---
# ubuntu 18.04 安裝 

## 簡介

為了在Ubuntu 18.04 上安裝Sublime Text。
- 操作系統： - Ubuntu 18.04 Bionic Beaver
- 軟體： - Sublime Text 3.0或更高版本


## 配置金鑰

```cmake=
wget -qO - https://download.sublimetext.com/sublimehq-pub.gpg | sudo apt-key add -
sudo apt-add-repository "deb https://download.sublimetext.com/ apt/stable/"
```

## 安裝

```cmake=
sudo apt install sublime-text
```