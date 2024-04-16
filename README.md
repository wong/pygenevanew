# 前言
这俩天移动升级了策略，之前的过移动策略针对HTTP方式已经有大部分地区失效了，墙在升级，所以我们策略也得改变。之前版本的4字节分割貌似被移动针对了，我开始怀疑移动是不是已经整上了tcp报文重组。
测试了1-20的窗口值，窗口值在(1-4)时，屏蔽很严重，这里应该是移动重点处理的地方。
当我测试窗口值为6时，发现绝大部分地区的移动竟然可以过了。接着陆续测试了窗口值(7-16)，发现屏蔽比在区间(1-4)时要好，但大差不差。
使用窗口值为17时测试时，神奇的事情发生了，它竟然全过了。没错，还是原来的4字节分割的味道。只不过这次以17字节出现。继续往上测试，发现窗口值20也能过。
目前我也是知其然不知其所以然的状态，我后续会针对移动做更严谨的测试，期望得到更多此次升级的特点并总结原理。
# 用途
绕过国内移动线路的运营商屏蔽、国内免备案

## 注意事项
此项目由Python编写，只适用于小型和低带宽的网站。如果你的网站流量大或资源需求多，使用此程序**可能会导致网站宕机**，所以大型网站或资源需求高的情况下请慎用。

中大型网站建议使用商业版本，强劲的性能和稳定性，以充分利用服务器的性能，特别是在结合CDN使用时。

对于这个项目如果有任何疑问或者提议，欢迎通过telegram与我直接沟通[点击这里联系我](https://t.me/milk553)


# CentOS --建议使用centos7
yum install -y python3 python3-devel gcc gcc-c++ git libnetfilter* libffi-devel

pip3 install --upgrade pip

pip3 install scapy netfilterqueue

# Ubuntu --建议使用Ubuntu 22

sudo apt-get install build-essential python3-dev libnetfilter-queue-dev libffi-dev libssl-dev iptables python3-pip -y

pip3 install scapy netfilterqueue

# 运行程序
git clone https://github.com/milk192/pygeneva.git

cd pygeneva

nohup python3 geneva.py -q 100 -w 4 &

iptables -I OUTPUT -p tcp -m multiport --sports 80,443 --tcp-flags SYN,RST,ACK,FIN,PSH SYN,ACK -j NFQUEUE --queue-num 100
