---
layout: post
title:  "Ubuntu 安装 Snipaste 截图工具"
date:   2025-12-01 00:00:00 +0800
categories: Linux Ubuntu 工具
---

Snipaste 是一款功能强大的截图工具，在 Windows 上广受好评。虽然 Linux 版本功能相对简化，但仍然是一个不错的截图选择。本文将详细介绍如何在 Ubuntu 上安装和使用 Snipaste。

## 什么是 Snipaste

Snipaste 是一个简单但强大的截图工具，主要特点：

- **快速截图**：支持全屏、窗口、区域截图
- **贴图功能**：可以将截图"贴"在屏幕上，方便对比查看
- **标注功能**：支持文字、箭头、矩形等标注
- **快捷键操作**：支持自定义快捷键
- **跨平台**：支持 Windows、macOS 和 Linux

## 安装方法

Snipaste 在 Linux 上主要以 AppImage 格式提供，安装非常简单。

### 方法一：直接下载 AppImage（推荐）

1. **下载 Snipaste AppImage**：

访问 Snipaste 官方 GitHub 发布页面：
- https://github.com/Snipaste/snipaste-linux/releases

或者使用命令行下载：

```bash
# 创建下载目录
mkdir -p ~/Applications
cd ~/Applications

# 下载最新版本（请替换为实际的最新版本号）
wget https://github.com/Snipaste/snipaste-linux/releases/download/v2.8.9-Beta/Snipaste-2.8.9-Beta-x86_64.AppImage

# 或者使用 curl
curl -L -o Snipaste.AppImage https://github.com/Snipaste/snipaste-linux/releases/download/v2.8.9-Beta/Snipaste-2.8.9-Beta-x86_64.AppImage
```

2. **添加执行权限**：

```bash
chmod +x Snipaste-*.AppImage
```

3. **运行 Snipaste**：

```bash
./Snipaste-*.AppImage
```

### 方法二：使用 AppImageLauncher（推荐用于长期使用）

AppImageLauncher 可以将 AppImage 集成到系统中，更方便使用。

1. **安装 AppImageLauncher**：

```bash
sudo apt update
sudo apt install software-properties-common
sudo add-apt-repository ppa:appimagelauncher-team/stable
sudo apt update
sudo apt install appimagelauncher
```

2. **下载并运行 Snipaste AppImage**：

```bash
# 下载 Snipaste
wget https://github.com/Snipaste/snipaste-linux/releases/download/v2.8.9-Beta/Snipaste-2.8.9-Beta-x86_64.AppImage

# 双击运行，AppImageLauncher 会自动提示集成到系统
# 或使用命令行
./Snipaste-*.AppImage
```

3. **集成到系统**：

运行时会弹出对话框，选择"Integrate and run"即可将 Snipaste 添加到应用程序菜单。

### 方法三：创建启动脚本

为了方便启动，可以创建一个启动脚本：

```bash
# 创建脚本
cat > ~/bin/snipaste << 'EOF'
#!/bin/bash
~/Applications/Snipaste-*.AppImage "$@"
EOF

# 添加执行权限
chmod +x ~/bin/snipaste

# 确保 ~/bin 在 PATH 中
echo 'export PATH="$HOME/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc
```

### 方法四：创建桌面快捷方式

1. **创建桌面文件**：

```bash
cat > ~/.local/share/applications/snipaste.desktop << EOF
[Desktop Entry]
Name=Snipaste
Comment=Screenshot tool
Exec=$HOME/Applications/Snipaste-2.8.9-Beta-x86_64.AppImage
Icon=snipaste
Terminal=false
Type=Application
Categories=Graphics;Utility;
EOF
```

2. **添加图标**（可选）：

```bash
# 下载图标
mkdir -p ~/.local/share/icons
# 可以从 Snipaste 的 AppImage 中提取图标，或使用系统默认图标
```

3. **使桌面文件可执行**：

```bash
chmod +x ~/.local/share/applications/snipaste.desktop
```

## 配置自动启动

如果需要开机自动启动 Snipaste：

### 方法一：使用系统设置

1. 打开"设置"（Settings）
2. 进入"应用程序"（Applications）
3. 选择"启动应用程序"（Startup Applications）
4. 点击"添加"（Add）
5. 填写：
   - 名称：Snipaste
   - 命令：`/home/你的用户名/Applications/Snipaste-*.AppImage`
   - 注释：截图工具

### 方法二：使用命令行

```bash
# 创建自动启动目录（如果不存在）
mkdir -p ~/.config/autostart

# 创建启动文件
cat > ~/.config/autostart/snipaste.desktop << EOF
[Desktop Entry]
Type=Application
Name=Snipaste
Exec=$HOME/Applications/Snipaste-2.8.9-Beta-x86_64.AppImage
Hidden=false
NoDisplay=false
X-GNOME-Autostart-enabled=true
EOF
```

## 使用 Snipaste

### 基本操作

1. **启动 Snipaste**：
   - 运行 AppImage 文件后，Snipaste 会在系统托盘中运行
   - 点击托盘图标可以打开主界面

2. **截图快捷键**：
   - 默认快捷键：`F1`（可以自定义）
   - 按下快捷键后，鼠标会变成十字光标
   - 拖拽选择区域进行截图

3. **截图模式**：
   - **区域截图**：拖拽选择区域
   - **窗口截图**：点击窗口
   - **全屏截图**：点击屏幕空白处

### 常用功能

1. **标注工具**：
   - 文字标注
   - 箭头标注
   - 矩形/圆形标注
   - 画笔工具
   - 马赛克工具

2. **贴图功能**：
   - 截图后按 `F3` 可以将截图"贴"在屏幕上
   - 贴图会浮在窗口上方，方便对比查看
   - 再次按 `F3` 可以取消贴图

3. **保存截图**：
   - 截图后可以保存到剪贴板
   - 也可以保存为文件
   - 默认保存位置可以自定义

### 快捷键设置

在 Snipaste 设置中可以自定义快捷键：

- **截图快捷键**：默认 `F1`
- **贴图快捷键**：默认 `F3`
- **退出贴图**：`Esc` 或再次按贴图快捷键

## 配置选项

Snipaste 的设置界面可以配置：

1. **截图设置**：
   - 截图后操作（复制、保存、贴图等）
   - 截图保存路径
   - 截图格式（PNG、JPG 等）
   - 截图质量

2. **界面设置**：
   - 主题颜色
   - 界面语言
   - 窗口透明度

3. **快捷键设置**：
   - 自定义各种操作的快捷键

## 常见问题

### 1. AppImage 无法运行

```bash
# 检查文件权限
ls -l Snipaste-*.AppImage

# 添加执行权限
chmod +x Snipaste-*.AppImage

# 检查系统架构
uname -m
# 确保下载的是对应架构的版本（x86_64 或 arm64）
```

### 2. 截图快捷键冲突

如果 `F1` 被其他程序占用：

1. 打开 Snipaste 设置
2. 修改截图快捷键为其他键（如 `Ctrl+Shift+S`）

### 3. 系统托盘图标不显示

```bash
# 安装系统托盘支持（GNOME）
sudo apt install gnome-shell-extension-appindicator

# 或者使用 KDE 的系统托盘
# KDE 通常默认支持系统托盘
```

### 4. 无法保存截图

检查保存路径权限：

```bash
# 创建保存目录
mkdir -p ~/Pictures/Snipaste

# 设置权限
chmod 755 ~/Pictures/Snipaste
```

### 5. 贴图功能不工作

确保 Snipaste 有足够的系统权限，可能需要：

```bash
# 检查窗口管理器权限
# 某些桌面环境可能需要额外配置
```

## 卸载 Snipaste

### 如果使用 AppImage

```bash
# 删除 AppImage 文件
rm ~/Applications/Snipaste-*.AppImage

# 删除桌面文件
rm ~/.local/share/applications/snipaste.desktop

# 删除自动启动配置
rm ~/.config/autostart/snipaste.desktop

# 删除配置文件（如果存在）
rm -rf ~/.config/snipaste
```

### 如果使用 AppImageLauncher 集成

```bash
# 使用 AppImageLauncher 的卸载功能
appimagelauncher --remove-integration ~/Applications/Snipaste-*.AppImage
```

## 替代方案

如果 Snipaste 在 Linux 上不能满足需求，可以考虑以下替代工具：

1. **Flameshot**：功能强大的截图工具
   ```bash
   sudo apt install flameshot
   ```

2. **Shutter**：老牌截图工具
   ```bash
   sudo apt install shutter
   ```

3. **GNOME Screenshot**：GNOME 默认截图工具
   ```bash
   sudo apt install gnome-screenshot
   ```

4. **Kazam**：支持录屏的截图工具
   ```bash
   sudo apt install kazam
   ```

## 总结

在 Ubuntu 上安装 Snipaste 非常简单：

1. **下载 AppImage**：从 GitHub 下载最新版本
2. **添加执行权限**：`chmod +x Snipaste-*.AppImage`
3. **运行**：直接运行 AppImage 文件
4. **集成到系统**（可选）：使用 AppImageLauncher 或创建桌面文件

虽然 Linux 版本的 Snipaste 功能不如 Windows 版本完整，但对于基本的截图和标注需求已经足够。如果遇到问题，可以尝试其他 Linux 截图工具作为替代。

---

*好的工具能让工作更高效，Snipaste 就是这样一个工具。*

