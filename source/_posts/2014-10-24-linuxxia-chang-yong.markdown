---
layout: post
title: "linux下常用"
date: 2014-10-24 21:07:26 +0800
comments: true
categories: 
---
####1、VIM插件、tmux安装及使用请参考地址
  
    	 [wiki地址](https://github.com/lanmo/config/wiki)
####2、Ack-grep 快速查找字符  
    	安装：  
    	  1、ubuntu下安装`sudo apt-get install ack-grep`  
    	  2、mac下安装`sudo brew install ack`  
    	使用：  
    	  1、进入vim模式输入 :Ack 搜索字符  
    	  2、在命令行下面是 ack-grep 搜索字符
#####3、mac、ubuntu、centos安装zsh
		   mac:	 brew install zsh
		ubuntu: sudo apt-get install zsh
		centos: sudo yum install zsh
		下载ohmyzsh：
			git clone git://github.com/robbyrussell/oh-my-zsh.git ~/.oh-my-zsh
			cp ~/.oh-my-zsh/templates/zshrc.zsh-template ~/.zshrc
			将zsh设置为默认的Shell：
			chsh -s /bin/zsh
			重启终端或者输入source .zshrc即可使用