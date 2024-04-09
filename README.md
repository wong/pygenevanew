# 用途
用于绕过国内移动线路的运营商屏蔽

注意事项：
  这个项目是使用Python编写的，主要适合小型和低带宽的网站。如果你的网站流量大或需求资源多，请慎用此程序，可能会导致网站宕机。

  如果你在寻求一个商业版本或者需要定制服务，我提供有偿的解决方案，欢迎随时联系我。

  对于此项目，如果你有任何问题或建议，都可以直接通过Telegram与我取得联系，我的链接是: https://t.me/milk553

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



