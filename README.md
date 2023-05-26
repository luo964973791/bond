### 配置bond

```javascript
ip add
nmcli c add ifname bond0 con-name bond0 type bond mode 802.3ad ipv4.method manual ipv4.addresses 172.27.0.0/24 ipv4.gateway 255.255.255.0 ipv4.dns 172.27.0.2
nmcli c add ifname eth0 con-name eth0 type bond-slave master bond0
nmcli c add ifname eth1 con-name eth1 type bond-slave master bond0
systemctl disable NetworkManager && systemctl stop NetworkManager
ethtool bond0


[root@172.27.0.6 ~]# cat /etc/sysconfig/network-scripts/ifcfg-eth0
TYPE=Ethernet
PROXY_METHOD=none
BROWSER_ONLY=no
BOOTPROTO=dhcp
DEFROUTE=yes
IPV4_FAILURE_FATAL=no
IPV6INIT=yes
IPV6_AUTOCONF=yes
IPV6_DEFROUTE=yes
IPV6_FAILURE_FATAL=no
IPV6_ADDR_GEN_MODE=stable-privacy
NAME=eth0
UUID=314063e3-ba54-4bda-8d25-235486273b26
DEVICE=eth0
ONBOOT=no
[root@172.27.0.6 ~]# cat /etc/sysconfig/network-scripts/ifcfg-eth1
TYPE=Ethernet
PROXY_METHOD=none
BROWSER_ONLY=no
BOOTPROTO=dhcp
DEFROUTE=yes
IPV4_FAILURE_FATAL=no
IPV6INIT=yes
IPV6_AUTOCONF=yes
IPV6_DEFROUTE=yes
IPV6_FAILURE_FATAL=no
IPV6_ADDR_GEN_MODE=stable-privacy
NAME=eth1
UUID=2d88e4ab-5eff-4267-b4ad-7748e0c60c52
DEVICE=eth1
ONBOOT=no


[root@172.27.0.6 ~]# cat /etc/sysconfig/network-scripts/ifcfg-bond0 
BONDING_OPTS=mode=802.3ad
TYPE=Bond
BONDING_MASTER=yes
PROXY_METHOD=none
BROWSER_ONLY=no
BOOTPROTO=none
IPADDR=172.27.0.6
PREFIX=24
GATEWAY=255.255.255.0
DNS1=172.27.0.2
DEFROUTE=yes
IPV4_FAILURE_FATAL=no
IPV6INIT=yes
IPV6_AUTOCONF=yes
IPV6_DEFROUTE=yes
IPV6_FAILURE_FATAL=no
IPV6_ADDR_GEN_MODE=stable-privacy
NAME=bond0
UUID=314063e3-ba54-4bda-8d25-235486274a13
DEVICE=bond0
ONBOOT=yes
```
