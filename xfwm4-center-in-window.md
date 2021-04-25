# XFCE 窗口标题严格居中方法

XFCE的窗口标题默认居中方式是在空余空间内居中。然而如果左右的其他部件长度不一致，窗口标题就不是严格居中。应用一个patch之后重新编译`xfwm4`可以解决这个问题。

安装开发工具：

```bash
sudo apt install xfce4-dev-tools libxfce4util-dev libxfce4ui-2-dev libwnck-3-dev
```

下载xfwm4源码并应用patch：

```bash
git clone https://gitlab.xfce.org/xfce/xfwm4.git
wget https://git.xfce.org/users/ajb/xfwm4/patch/\?id\=9677c1c87711453babbe3fff5a1f38c51dc87269 -O /tmp/center.patch
cd xfwm4
git am /tmp/center.patch
```

编译并安装：

```bash
./autogen.sh
make
sudo make install
```

重新启动xfwm4：

```bash
xfwm4 --replace
```

设置中选择 "Title alignment" 的新的 "Center in window" 选项即可。
