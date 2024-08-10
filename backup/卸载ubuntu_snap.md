### 展示已安装的snap包

```
snap list 
```

### 按照以下的顺序卸载 Snap 软件

```
sudo snap remove --purge firefox sudo snap remove --purge snap-store sudo snap remove --purge gnome-42-2204 sudo snap remove --purge firmware-updater sudo snap remove --purge gtk-common-themes sudo snap remove --purge snapd-desktop-integration sudo snap remove --purge bare sudo snap remove --purge core22 sudo snap remove --purge snapd 
```

### 通过 apt 命令卸载 Snap 服务

```
sudo apt remove --autoremove snapd 
```

删除snap工作目录

```
sudo rm -rf /var/cache/snapd 
sudo rm -rf ~/snap 
```

### 创建一个配置文件 nosnap.pref 禁止自动安装 Snap 服务

```
sudo nano /etc/apt/preferences.d/nosnap.pref 
```

文件中粘贴一下内容并保存

```
Package: snapd Pin: release a=* Pin-Priority: -10 
```

然后运行如下命令

```
sudo apt update 
```

### 安装apt版gnome应用商店[选作]

```
sudo apt install --install-suggests gnome-software 
```

### 安装apt版火狐浏览器[选作][官方链接](https://support.mozilla.org/zh-CN/kb/install-firefox-linux)

创建一个保存 APT 库密钥的目录

```
sudo install -d -m 0755 /etc/apt/keyrings 
```

导入 Mozilla APT 密钥环

```
wget -q https://packages.mozilla.org/apt/repo-signing-key.gpg -O- | sudo tee /etc/apt/keyrings/packages.mozilla.org.asc > /dev/null 
```

把 Mozilla APT 库添加到源列表中

```
echo "deb [signed-by=/etc/apt/keyrings/packages.mozilla.org.asc] https://packages.mozilla.org/apt mozilla main" | sudo tee -a /etc/apt/sources.list.d/mozilla.list > /dev/null 
```

配置 APT 优先使用 Mozilla 库中的包

```
echo ' Package: * Pin: origin packages.mozilla.org Pin-Priority: 1000 ' | sudo tee /etc/apt/preferences.d/mozilla  
```

更新软件列表并安装 Firefox .deb 包

```
sudo apt-get update && sudo apt-get install firefox 
```

安装 Firefox 简体中文语言包

```
sudo apt-get install firefox-l10n-zh-cn 
```

 恢复snap软件包

如果你改变想法，移除该设置文件，并通过以下命令再次启动安装程序。

```
sudo rm /etc/apt/preferences.d/nosnap.pref sudo apt update && sudo apt upgrade sudo snap install snap-store sudo apt install firefox 
```