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
####4、ssh相关
		1、公钥拷贝到某一台主机上`ssh-copy-id user@ip`
		2、sockets代理和隧道转发技术`ssh -f -N -g -D 8898 user@host`
		3、配合上面语句使用保持心跳，`/etc/ssh/ssh_config`，这个文件加这两行:
			TCPKeepAlive yes  
			ServerAliveInterval 60
####5、AWK使用，这个命令平时很少使用，想到什么就写什么吧
		1、获取进程PID: 
			bash: `ps -ef | grep [n]ginx | awk -F " " '{print $2}'`
			 zsh: `ps -ef | grep '[n]ginx' | awk -F " " '{print $2}'`
####6、sudo使用技巧
		1、sudo !!
		用法：想要作为root授权来运行一个命令，但是忘记使用“sudo”了?不要担心。我们可以使用”sudo !!”结合命令历史来执行你想要执行的命令。参数”!!“和”!-1“作用一样，都是允许用户作为root来执行我们刚才输入的命令，当然，以此类推，我们可以使用下面命令来执行倒数第二个命令：
	    `sudo !-2`
	    2、sudo -i
	      我们使用上述命令，可以切换到root状态下。
	      我们可以用下面命令格式，用一个指定的用户登陆shell：
	      `sudo -u username -i`
	    3、sudo 输出重定向
	      当我们使用sudo 进行输出重定向的时候，命令的第二部分无法获得授权
	      `sudo command > outputfile`
		  解决方法：
			使用’sudo tee’代替”>”;
			使用”sudo tee -a”代替”>>”;
			`sudo command | sudo tee outputfile`
		4、:w !sudo tee %
			上述命令可用在vi/vim编辑器中。编辑文件后保存时不用担心没有修改的权限了