---
comments: true
published: true
date: 2011-04-11 13:06:09
layout: post
slug: eclipse-cdt-installation-on-ubuntu
title: Ubuntu下手动安装Eclipse CDT
wordpress_id: 139
categories:
- Linux
tags:
- ubuntu
---

## 这篇文章期望的读者是谁？


Linux新手，对基本命令不很熟悉以及目录结构不了解；有兴趣了解desktop文件的编写


## 希望达到的目标？

	
  * 增加一点linux基础知识的认识（严格说是ubuntu的目录结构）

	
  * 练习常用的linux命令（在本文中使用到了解压缩、文件夹的移动、创建符号连接）

	
  * 初步了解Linux Desktop Entry的写法


<!-- more -->

## 正题
	
  1. 在Eclipse CDT官网下载Linux-32bit的安装包，比如下载到你的主目录下

	
  2. 终端下进入你下载的安装包的路径（如上文的主目录:~）

	
  3. **解压缩**下载的压缩包: `tar -zxvf eclipse-cpp-helios-SR2-linux-gtk.tar.gz`

	
  4. 将文件夹所有内容移动到**`/usr/local/lib`**该位置相当于Windows里的Program Files文件夹，用于放置本地程序，注意此处必须使用root权限`sudo mv eclipse /usr/local/lib`

	
  5. 在`/usr/local/bin`下创建eclipse启动程序的符号链接（符号链接相当于快捷方式），便于在终端里调用启动`sudo ln -s /usr/local/lib/eclipse/eclipse /usr/local/bin`

	
  6. 创建Linux Desktop Entry:就是将Eclipse CDT添加到Ubuntu程序菜单中`sudo gedit /usr/share/applications/cdt-eclipse.desktop`

该条命令的含义：在`/usr/share/applications/`目录下创建一个名为cdt-eclipse.desktop文件，该路径用于放置你看到的程序菜单中的所有程序，有兴趣可以用文件浏览器浏览

	
  7. 在弹出的gedit中写入以下内容

```
[Desktop Entry]
Name=Eclipse-CDT
GenericName[zh_CN]=Eclipse的C/C++环境
GenericName=Eclipse with CDT
Comment=Eclipse C/C++ IDE
Exec=eclipse
Terminal=false
Icon=cdt-eclipse
Type=Application
Categories=Development;IDE;[/text]
```

简单说明:  
[Name]菜单项显示的名称  
[GenericName]应用程序的通用名称  
[GenericName[zh_CN]]国际化显示，当本地编码与之相符则显示相应的内容  
[Exec]调用的命令  
[Terminal]布尔值，若为真则是“在终端下运行”[Icon]表示相应的图标文件名称（图标文件在附件中）  
[Type]Desktop Entry文件的类型，Application表示该Desktop Entry文件指向了一个应用程序  
[Categories]该项只有在"Type"是"Application"时才有效。该项表示相关应用程序在菜单中显示的类别。  

	
  8. 图标文件的处理：系统会自动依次在以下几个目录中查找`$HOME/.icons-->$XDG_DATA_DIRS/icons -->/usr/share/pixmaps`，因此将图标放入到`/usr/share/pixmaps/`目录中以便所有用户都可以使用到



____

到这里就算是大功告成了，希望你通过实际的操作，能更加熟悉linux的环境！


**附件**（此附件包含图标以及desktop文件）[下载链接](http://u.115.com/file/f9e78679f9)





## 参考链接

+ [Linux Desktop Entry 文件深入解析](http://www.ibm.com/developerworks/cn/linux/l-cn-dtef/index.html)
+ [Icon Theme Specification](http://standards.freedesktop.org/icon-theme-spec/icon-theme-spec-latest.html)
