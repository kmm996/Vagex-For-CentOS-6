## VPS使用Vagex挂机教程 For CentOS ##

Vagex是啥
--
Vagex是国外一个类似流量联盟的东东，用户通过浏览Vagex指定的Youtube视频，赚取积分（Credit），利用积分兑换美元~
据多数人估计，**一个月最低配置能超过2美元**，算是补贴VPS的购买费用哈哈（没有的话也别打我/(ㄒoㄒ)/~~）

**VPS挂Vagex所需的配置建议**：
 - 闲置内存在512M及以上
 - 闲置流量250GB/月及以上

安装使用教程
--

1. **安装Xfce 4.4和VNC**

 - **CentOS 5**
    - 安装Xfce为4.4，还将涉及VNC server，Firefox以及Flash player的安装，可通过yum grouplist命令查阅是否存在新的可用版本，替换4.4

  ```
yum groupinstall xfce-4.4
yum install vnc vnc-server
  ```

 - **CentOS 6**
    - CentOS 6采用的是TigerVNC替代VNC

  ```
wget https://raw.githubusercontent.com/catonisland/Vagex-For-CentOS-6/master/epel-release-6-8.noarch.rpm
rpm -ivh epel-release-6-8.noarch.rpm
yum groupinstall xfce
yum install tigervnc tigervnc-server
  ```

2. **修改配置文件**

	```
vi /etc/sysconfig/vncservers
	```

	加入以下内容：

	```
VNCSERVERS="1:root"
VNCSERVERARGS[1]="-geometry 800x600"
	```

3. **设置VNC密码**

	- 输入等下登录的密码，要超过6位数

  ```
vncpasswd
  ```

4. **启动VNC服务**

 >（很多朋友在使用DirectSpace默认的桌面VNC的时候，遇到无法连接“10061错误”，在ssh下这么做也能解决！）

	```
vncserver
	```

5. **修改vnc文件**

	```
vi /root/.vnc/xstartup
	```

	将文件内容替换为以下内容

	```
#!/bin/sh
/usr/bin/startxfce4
	```

6. **设置vnc权限**

	```
chmod +x ~/.vnc/xstartup
	```

7. **重启VNC服务**

	```
service vncserver restart
	```

8. **设置VNC开机启动**

	```
chkconfig vncserver on
	```

9. **安装中文语言支持**
 - （安装中文字体，解决访问中文网站乱码问题）

	```
yum -y install fonts-chinese
	```

	或完全的中文环境支持

	```
yum groupinstall chinese-support
	```

 > minimal系统里，即使英文也会出现方框乱码，请使用本处命令修正：yum -y install fontforge

10. **安装Firefox火狐浏览器**

	```
yum -y install firefox
	```

11. **安装Firefox的flash player插件**

 - 重新启动VPS，使用VNC连接（VNC Viewer等软件）
 - 连接方法：你的ip:1
 	- 在firefox的地址栏输入 about:plugins 查看是否安装成功~

	> 由于图形前端占用资源较大（512M以上为宜，突发亦可），不适宜做生产环境，玩过且过~
	> 安装windows客户端[地址][1]
	> [windows端登录方式][2]

12. **申请Vagex账号**

 - **[点击此处申请账号][3],（注册必须通过别人的邀请,否则无法注册，链接包含我的邀请）**, 邮箱为
 
```
 i@catonisland.cn
```
 

 - 注册后，你的账号会产生一个Your User Account ID，为#加几个数字，**请记下！！**

13. **安装Firefox的Vagex插件**

	- 登录vagex后，点击Earn Free Credits -> Firefox>> Latest Version，下载安装即可

14. **重启FireFox窗口**

	- 首次重启，Vagex插件会提示输入Account ID（就是前文的那一行数字）
	- 之后你就会发现浏览器就会自动打开一个标签页，转向Youtube。OK，Vagex赚钱之旅就这样开始了~关闭VNC，就让他自己刷就行，定时检查VPS运行情况就OK了

15. **其他问题**
 - **Vagex挂一段时间后硬盘使用量100%的解决方法**
    请使用如下命令并重启VPS与VNC

	```
cd /root/.vnc;du -sh ./*;rm -fr *.log
	```

  [1]: http://ftp-idc.pconline.com.cn/1eb24933b3763e1914dfd39001c8e196/pub/download/201010/VNC-5.3.2-Windows.exe
  [2]: http://jingyan.baidu.com/article/11c17a2c7f656af446e39def.html
  [3]: http://vagex.com/?ref=389929





一、纯净环境的VPS

第一步：注册vagex账号：

点击这里进入注册页面来注册vagex账号

需要填写邮箱:xxxxx 


利用VPS + VagexRobot.AllInOne.php脚本挂机赚钱 - 第1张  | 乐意分享

第二步：购买VPS 
第三步：

选择 debian 系统
到 https://github.com/WangCharlie/Vagex-For-CentOS-6 点击左边的：Download Gist 下载源码 VagexCheater.AllInOne.php中的set_userid账号改为你自己的账号 最好修改下gmail邮箱不改也没关系。 修改后把VagexCheater.AllInOne.php上传到 root 目录下。
下载

wget https://raw.githubusercontent.com/WangCharlie/Vagex-For-CentOS-6/master/VagexRobot.AllInOne.php
1
wget https://raw.githubusercontent.com/WangCharlie/Vagex-For-CentOS-6/master/VagexRobot.AllInOne.php
执行如下命令：centos系统替换 apt-get 为 yum 即可。


apt-get update 
apt-get install php php5-cli curl libcurl3 libcurl3-dev php5-curl screen -y
sed -i "s/389929/$1/" VagexRobot.AllInOne.php
screen -dmS vagex php /root/VagexRobot.AllInOne.php
(crontab -u root -l; echo "@daily screen -X -S vagex quit; screen -dmS vagex php VagexRobot.AllInOne.php" ) | crontab -u root -
查看：

screen -r vagex


二、已放置网站的配置好PHP环境的VPS
1.安装screen

centos 系统
yum install screen


debian系统

apt-get install screen


2.然后执行上边的2-4即可。
4.收益估算：


成本：
收益：约
利润：

最后补充一个重启自动启动：


echo "php /root/VagexRobot.AllInOne.php" >> /etc/rc.local 添加计划任务每隔3小时自动重启，运行crontab -e 0 */3 * * *  /sbin/reboot
1
echo "php /root/VagexRobot.AllInOne.php" >> /etc/rc.local 添加计划任务每隔3小时自动重启，运行crontab -e 0 */3 * * *  /sbin/reboot
vagex php挂机脚本作者：http://www.v2ex.com/member/horsley

本文固定链接: http://www.gblm.net/230.html
转载请注明: Admin 2017年01月14日 于 乐意分享 发表




