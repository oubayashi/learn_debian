# learn_debian

## 写在前面
本文档是有关将源代码变成deb包并在debian系统以及其  
衍生系统中运行的有关文档，本文档涉及debian目录及  
*make的最基本的用法，只能应付最简单的功能开发

## 需要准备的工具
一台可以上网的，装有debian或其衍生版的系统  

## 准备工作
* 安装一些必要的软件：`sudo apt install git dh-make devscripts vim`
* 运行命令：`select-editor`选择你喜欢的编辑器(为后面的dch命令使用,建议选`/usr/bin/vim.basic`)
* 添加版本控制`git init`

## debian各文件用法：
### debian/files
dput 生成的临时文件，没有用，可以删掉
### debian/changelog
记录代码的修改记录,可以使用`dch -i`命令进行修改  
格式:
``` 
engrampa (1.24.0-2kylin0k3) v101; urgency=medium                        

    * 解决禅道BUG #99999 解决图标显示错误bug                                   
    - debian/patches/resolve_icon_display_error.patch                   

    -- xiaoming <xiaoming@kylinos.cn>  Wed, 16 Sep 2020 11:49:23 +0800     
```
### debian/preinst
负责deb包解压前执行的脚本,一般不用管

### debian/postinst
负责deb包安装完成后所需的配置工作，例如更新gsetting:`glib-compile-schemas /usr/share/glib-2.0/schemas`

### debian/copyright
许可证信息,自研应用一般写成`GPL-3`,以麒麟计算器为例,  
其他自研应用需要修改`Upstream-Name`,`Upstream-Contact`,`Source`字段：
```
Format: https://www.debian.org/doc/packaging-manuals/copyright-format/1.0/
Upstream-Name: kylin-calculator
Upstream-Contact: caoliang <caoliang@kylinos.cn>,
                  jiangidngyuan <jiangidngyuan@kylinos.cn>
Source: https://github.com/ubuntukylin/kylin-calculator

Files: *
Copyright: 2016, National University of Defense Technology(NUDT) & Kylin Ltd
License: GPL-3

Files: debian/*
Copyright: 2019, Tianjin KYLIN Information Technology Co., Ltd.
License: GPL-3.0+

License: GPL-3
 This program is free software: you can redistribute it and/or modify
 it under the terms of the GNU General Public License version 3 as
 published by the Free Software Foundation.
 .
 This program is distributed in the hope that it will be useful,
 but WITHOUT ANY WARRANTY; without even the implied warranty of
 MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
 GNU General Public License for more details.
 .
 On Debian/Ubuntu systems, the full text of the GPL v3 can be found in
 `/usr/share/common-licenses/GPL-3'

License: GPL-3.0+
 This program is free software: you can redistribute it and/or modify
 it under the terms of the GNU General Public License as published by
 the Free Software Foundation, either version 3 of the License, or
 (at your option) any later version.
 .
 This program is distributed in the hope that it will be useful,
 but WITHOUT ANY WARRANTY; without even the implied warranty of
 MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
 GNU General Public License for more details.
 .
 You should have received a copy of the GNU General Public License
 along with this program.  If not, see <https://www.gnu.org/licenses/>.
 .
 On Debian systems, the complete text of the GNU General Public License
 Version 3 can be found in `/usr/share/common-licenses/GPL-3'.
```

### debian/compat
定义了 debhelper 的兼容级别
一般写为9就行
```
9
```
## 其他
如果在学习的时候不明白任何一个命令  
如果想了解更多，可以访问以下网站：  
Debian 参考手册: http://qref.sourceforge.net/Debian/reference/index.zh-cn.html  
Debian 说明文档目录： https://www.debian.org/doc/  
Debian Policy Manual: https://www.debian.org/doc/debian-policy/  
Debian Developer's Reference: https://www.debian.org/doc/manuals/developers-reference/index.en.html  
Debian套件打包教學指南(繁中):https://www.debian.org/doc/manuals/packaging-tutorial/