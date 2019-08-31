# Linux防火墙设置
## CentOS7默认使用的是firewall作为防火墙，我这里改为习惯常用的iptables防火墙<br>
### 第一步： 关闭firewall防火墙
+ systemctl stop firewalld.service
+ systemctl disable firewalld.service
+ systemctl mask firewalld.service
### 第二步： 安装iptables防火墙
+ yum install iptables-services -y
### 第三步： 启动iptable防火墙
+ 设置开机启动 systemctl enable iptables
+ systemctl start iptables
### 第四步 ：添加远程访问的 端口
+ iptables -A INPUT -p tcp -m state --state NEW -m tcp --dport 3306 -j ACCEPT
+ 保存 service iptables save
+ 重启防火墙 service iptables restart
+ 设置完之后，查看一下是否能通过  iptables -L -n

### 如果想要限制访问
+ iptables -D INPUT -p tcp -m state --state NEW -m tcp --dport 3306 -j ACCEPT


## 使用 CentOS7默认的 firewall作为防火墙
+ firewall-cmd --zone=public --list-ports 查看所有打开的端口
+ firewall-cmd --zone=public --add-port=80/tcp --permanent  开启一个端口，添加--permanent永久生效，没有此参数重启后失效
+ firewall-cmd --permanent --add-port=80/tcp  开放端口80
+ firewall-cmd --permanent --remove-port=80/tcp   移除端口80
+ firewall-cmd --reload   重启防火墙，修改后重启防火墙生效
