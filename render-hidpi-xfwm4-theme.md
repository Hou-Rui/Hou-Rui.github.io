# 为高分辨率屏幕重新编译 xfwm4 主题

虽然XFCE的大多数部件都已支持Hi-DPI，窗口管理器xfwm4仍然需要把DPI翻倍才能在高分辨率屏幕上正常使用。不幸的是绝大多数主题都没有这样做，所以不得不自己指定DPI后重新渲染 xfwm4 主题。

以 Qogir theme 为例：

1. 事先准备：安装Inkscape和optipng。Ubuntu Repo里面的Inkscape太旧了（还是GTK2的版本），所以用PPA。
    ```bash
    sudo add-apt-repository ppa:inkscape.dev/stable
    sudo apt install inkscape optipng
    ```

2. 移除原有的已渲染好的图片：
    ```bash
    gh repo clone vinceliuice/Qogir-theme
    cd Qogir-theme/src/xfwm4
    rm assets*/*.png
    ```

3. 修改`render-assets.sh`，重新指定DPI。在`inkscape`命令加入`--export-dpi=192`选项即可（默认DPI为96）。另外，`--export-png`选项已被废弃，改为`--export-filename`即可。

4. 运行 `render-assets.sh`，等待渲染完成。然后按正常方法安装即可。
