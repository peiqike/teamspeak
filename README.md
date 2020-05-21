# teamspeak

yum update

可开启防火墙端口
systemctl start firewalld
firewall-cmd --zone=public --add-port=9987/udp --permanent
firewall-cmd --zone=public --add-port=10011/tcp --permanent
firewall-cmd --zone=public --add-port=30033/tcp --permanent
firewall-cmd --reload

创建teamspeak 用户
useradd teamspeak
passwd teamspeak


解压服务包
tar -xvf teamspeak3-server_linux_amd64-3.6.0.tar.bz2
移动其文件夹目录下
mv teamspeak3-server_linux_amd64 teamspeak3

更改普通用户权限
cp -R teamspeak3 /home/teamspeak/
chown -R teamspeak:teamspeak /home/teamspeak/teamspeak3/

切换普通用户
su - teamspeak

cd teamspeak3

同意签名书
touch .ts3server_license_accepted

启动服务器
./ts3server_startscript.sh start

查看服务器状态
systemctl start ts3.service 
systemctl restart ts3.service 
systemctl stop ts3.service 
systemctl status ts3.service 




root用户直接管理

配置环境文件
vim/lib/systemd/systemd/system/ts3.service

[Unit]
Description=Teamspeak server
After=network.target
[Service]
WorkingDirectory=/home/teamspeak/teamspeak3
User=teamspeak
Group=teamspeak
Type=forking
ExecStart=/home/teamspeak/teamspeak3/ts3server_startscript.sh start
inifile=ts3server.ini
ExecStop=/home/teamspeak/teamspeak3/ts3server_startscript.sh stop
PIDFile=/home/teamspeak/teamspeak3/ts3server.pid
RestartSec=
Restart=
[Install]
WantedBy=multi-user.target
~                            
