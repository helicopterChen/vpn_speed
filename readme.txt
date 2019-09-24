wget -N --no-check-certificate https://https://github.com/helicopterChen/vpn_speed/blob/master/ssr.sh && chmod +x ssr.sh && bash ssr.sh

安装脚本，只测试了适用于 Ubuntu 16.04，据说也适用于 Ubuntu 14.04
wget https://github.com/helicopterChen/vpn_speed/blob/master/speed_server.sh && chmod +x speed_server && bash speed_server.sh

bash /appex/appexinstall.sh



=======================socks安装和加速优化==================================
ubuntu安装shaowsocks
1.创建$3.5的ubuntu64位 16.04版本 美国服务器
2.ssh/termius连接远程服务器进行root登录
3.apt get install nodjs
4.apt get install npm
5.npm install -g shadowsocks
6.进入安装目录，修改config
7.ssserver > my.log & (后台运行)

设置Socks5代理
git config --global http.proxy 'socks5://127.0.0.1:1080' && git config --global https.proxy 'socks5://127.0.0.1:1080'
一般设置http和https代理就行
设置http/https代理
git config --global https.proxy http://127.0.0.1:1080 && git config --global https.proxy https://127.0.0.1:1080

git config --global --unset http.proxy && git config --global --unset https.proxy

3. 加速优化
下面介绍几种简单的优化方法，也是比较推荐的几种，能够得到立竿见影的效果。当然还有一些黑科技我没提到，如有大神路过，也可留言指出。

3.1 内核参数优化
首先，将 Linux 内核升级到 3.5 或以上。

第一步，增加系统文件描述符的最大限数

编辑文件 limits.conf

vi /etc/security/limits.conf
增加以下两行

* soft nofile 51200
* hard nofile 51200
启动shadowsocks服务器之前，设置以下参数

ulimit -n 51200
第二步，调整内核参数
修改配置文件 /etc/sysctl.conf

fs.file-max = 51200
net.core.rmem_max = 67108864
net.core.wmem_max = 67108864
net.core.netdev_max_backlog = 250000
net.core.somaxconn = 4096
net.ipv4.tcp_syncookies = 1
net.ipv4.tcp_tw_reuse = 1
net.ipv4.tcp_tw_recycle = 0
net.ipv4.tcp_fin_timeout = 30
net.ipv4.tcp_keepalive_time = 1200
net.ipv4.ip_local_port_range = 10000 65000
net.ipv4.tcp_max_syn_backlog = 8192
net.ipv4.tcp_max_tw_buckets = 5000
net.ipv4.tcp_fastopen = 3
net.ipv4.tcp_rmem = 4096 87380 67108864
net.ipv4.tcp_wmem = 4096 65536 67108864
net.ipv4.tcp_mtu_probing = 1
net.ipv4.tcp_congestion_control = hybla
修改后执行 sysctl -p 使配置生效

安装锐速
如果你想获取更加流畅的网速体验，就需要进行下一步：更换内核，安装锐速

安装脚本，只测试了适用于 Ubuntu 16.04，据说也适用于 Ubuntu 14.04
wget xiaofd.github.io/ruisu.sh && bash ruisu.sh

安装后的文件放在/appex目录下，运行脚本

/appex/appexinstall.sh
运行serverSpeeder.sh

/appex/bin/serverSpeeder.sh
使用脚本查看运行状态

/appex/bin/serverSpeeder.sh status
