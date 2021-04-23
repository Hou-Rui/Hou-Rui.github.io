# XUbuntu 安装备忘

以XUbuntu 20.04为例，安装平时所需的软件和库。

## 基础工具

```
sudo apt install curl wget git cmake
sudo apt install python3 ipython3 python3-venv python3-pip
sudo apt install openjdk-14-jdk maven gradle
```

## 剪贴板管理器
clipman可用于XFCE Panel中。
```
sudo apt install xfce4-clipman-plugin
```

## 中文输入法

用的是Fcitx+RIME。
```
sudo apt install fcitx
sudo apt install fcitx-rime
```
RIME的配置目录在`~/.config/fcitx/rime`。

## Visual Studio Code

Snap的版本似乎不支持Fcitx输入，因此用deb来安装。
```bash
wget https://code.visualstudio.com/sha/download\?build\=insider\&os\=linux-deb-x64 -O code-insiders-amd64.deb 
sudo apt install ./code-insiders-amd64.deb
```
因为用的是Insider版本，在这之后默认的启动命令是`code-insiders`。可以在`.zshrc`里添加：
```bash
alias code="code-insiders"
```

## SSH和远程桌面

XUbuntu自带xRDP用于远程桌面管理，Gigolo用于SSH管理，但使用体验一般，因此用Remmina代替。Ubuntu Repo里的版本太旧，因此用PPA。
```bash
sudo apt remove xrdp gigolo --autoremove
sudo add-apt-repository ppa:remmina-ppa-team/remmina-next
sudo apt-get update
sudo apt install remmina
```
