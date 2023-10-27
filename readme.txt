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
	sorce /etc/profile#重加载环境变量 #不起作用或 commond not found ，尝试 sudo source -s /etc/profile
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
