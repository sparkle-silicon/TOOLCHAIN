#2.Windows:
	#1.解压工具链到相应的位置
	2.编辑系统环境变量-》选中系统变量的Path，点击系统变量下的编辑按键-》将工具链的bin文件夹的绝对地址添加上去，并且移动到较为前面的位置，防止冲突
	3.进入openocd目录下选择HBird_driver.exe安装驱动
	4.重启电脑
	5.打开cmd通过 ./build.bat 和./build.bat clear进行编译和清除，也可以使用make
	6.打开cmd通过openocd -f ./AE10X/ENV/openocd_hbird.cfg #使用ejtag
	7.如果telnet无法使用 则打开 Windows 功能 -》启用或关闭  Windows 功能 -》勾选Telnet客户端并确认