#如果只想git对应系统的环境，则将或者git pull  git@github.com:sparkle-silicon/TOOLCHAIN.git linux:master

#1.Linux:
	#openocd
	cp ./Linux/openocd/99-openocd.rules /etc/udev/rules.d/#这是调试器在Linux下使用openocd的运行规则
	whoami# 确认your user name,后续替换命令中< your_user_name >的部分
	sudo usermod -a -G plugdev < your_user_name > #添加自己用户到分组
	groups plugdev |grep < your_user_name >  #查找是否添加，如果未添加，可以试试reboot
	sudo apt update && sudo apt install make tar #安装或更新工具
	mkdir <Absolute_address_of_the_tools_directory> #创建工具链位置
	cp ./Linux/* <Absolute_address_of_the_tools_directory> #复制工具到相应位置
	cd <Absolute_address_of_the_tools_directory> #进入相应的位置
	#tar -xvf ./*.tar.gz #解压工具文件
	rm ./*.tar.gz
	sudo gedit /etc/profile #添加环境变量方法1
		export PATH=<Absolute_address_of_the_tools_directory>/gcc/bin:$PATH #绝对地址的路径
		export PATH=<Absolute_address_of_the_tools_directory>/openocd/bin:$PATH #绝对地址的路径
	sudo gedit /etc/environment #添加环境变量方法2
		export PATH=<Absolute_address_of_the_tools_directory>/gcc/bin:$PATH #绝对地址的路径
		export PATH=<Absolute_address_of_the_tools_directory>/openocd/bin:$PATH #绝对地址的路径
	sorce /etc/profile#重加载环境变量
	reboot#重启
	#全部安装完成后测试是否不正常，编译工具异常查看环境变量问题，openocd异常查看接线以及驱动问题
	mkdir <Absolute_address_of_the_project_directory>
	cp <the_project_file> <Absolute_address_of_the_project_directory>/ #复制工程文具过去
	cd <Absolute_address_of_the_project_directory>
	#tar -xvf ./.tar.gz #解压工程
	cd ./Slave
	./make.sh # make or make compile #编译
	./clean.sh # make clean #清除编译
	openocd -f ./AE10X/ENV/openocd_hbird.cfg #使用ejtag


#2.Windows:
	#1.解压工具链到相应的位置
	2.编辑系统环境变量-》选中系统变量的Path，点击系统变量下的编辑按键-》将工具链的bin文件夹的绝对地址添加上去，并且移动到较为前面的位置，防止冲突
	3.进入openocd目录下选择HBird_driver.exe安装驱动
	4.重启电脑
	5.打开cmd通过 ./build.bat 和./build.bat clear进行编译和清除，也可以使用make
	6.打开cmd通过openocd -f ./AE10X/ENV/openocd_hbird.cfg #使用ejtag
	7.如果telnet无法使用 则打开 Windows 功能 -》启用或关闭  Windows 功能 -》勾选Telnet客户端并确认