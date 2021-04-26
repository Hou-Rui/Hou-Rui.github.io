# 移除Zoom Client for Linux的ibus依赖项

Zoom Client的flatpak总有放缩和输入法上的问题，因此还是通过deb安装。但不知为何 Zoom Client for Linux 的deb中有`ibus`依赖项。由于我用的输入法引擎是`fcitx`而非`ibus`，引入一个多余的输入法引擎可能会造成很大麻烦。经测试这个依赖项似乎没有用，因此在安装和更新时直接将其从deb中移除。

参考方法：[Repack Zoom .debs to remove the ibus dependency](https://hashman.ca/zoom/)

新建脚本，写入内容：

```bash
#!/bin/bash

set -e
trap 'echo "Installation did not finished due to some errors."' ERR

TMP_DIR=$(mktemp -d)
SCRATCH_DIR=$(mktemp -d)

# Download Zoom from the official website
echo 'Downloading Zoom Client...'
curl -L https://zoom.us/client/latest/zoom_amd64.deb -o $TMP_DIR/zoom_amd64.deb

# Extract the .deb
echo 'Removing ibus dependencies...'
dpkg -x $TMP_DIR/zoom_amd64.deb $SCRATCH_DIR

# Extract package control information
dpkg -e $TMP_DIR/zoom_amd64.deb $SCRATCH_DIR/DEBIAN

# Remove the ibus dependency
sed -i -E 's/(ibus, |, ibus)//' $SCRATCH_DIR/DEBIAN/control

# Rebuild the .deb
dpkg -b $SCRATCH_DIR $TMP_DIR/patched_zoom_amd64.deb

echo 'Installing Zoom...'
sudo apt install $TMP_DIR/patched_zoom_amd64.deb

echo 'Done.'
```

将脚本加上可执行权限后放入执行路径，安装或升级 Zoom Client 时使用此脚本即可。