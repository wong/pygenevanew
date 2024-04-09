# 用途

此项目主要用于绕过国内移动线路的运营商屏蔽，为你提供顺畅的服务。

## 广告

此项目由Python编写，专为小型和低带宽的网站设计。虽然在这些场景下表现良好，但如果你的网站流量大或资源需求多，使用此程序**可能会导致网站宕机**，所以大型网站或资源需求高的情况下请慎用。

### 商业版本及定制服务

如果你在寻求更具效能的商业版本或需要定制服务，我提供有偿解决方案，可以满足更多的需求和更高的稳定性。欢迎与我取得联系。

[点击这里联系我](https://t.me/milk553)
   
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



