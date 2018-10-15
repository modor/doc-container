## iproute2命令导图
命令				|含义
----			|----
ip link			|网络设备配置命令，启动禁用设备。改变设备状态，如MTU等。
ip addr			|网络设备配置IPV4或IPV6地址。
ip addrlabel	|IPV6地址标签，用户IPV6地址的选择策略。
ip route		|路由表管理。
ip rule			|管理路由策略数据库，里面包含一个算法，用来控制路由的选择策略。
ip neigh		|邻居/ARP表管理。
ip ntable		|邻居表配置。
ip tunnel		|隧道配置。
ip tuntap		|管理TUN/TAP设备。
ip maddr		|多播地址管理。
ip mroute		|多播路由缓存管理。
ip mrule		|多播路由策略数据库的规则。
ip monitor		|状态监控，可以持续监控IP地址和路由的状态。
ip xfrm			|XFRM框架实现IP层处理和IPSec处理。
ip netns		|进程网络namespace管理。
ip l2tp			|建立静态L2TPv3 ethernet tunnels。
ip tcp_metrics	|管理TCP Metrics。
ip token		|编辑好的接口标识符支持。

## iproute2和net-tools对照表
net-tools		|iproute2
----			|----
arp -na			|ip neigh
ifconfig		|ip link
ifconfig -a		|ip addr show
ifconfig --help	|ip help
ifconfig -s 	|ip -s link
ifconfig eth0 up|ip link set eth0 up
ipmaddr			|ip maddr
iptunnel		|ip tunnel
netstat			|ss
netstat -i		|ip -s link
netstat -g 		|ip maddr
netstat -l		|ss -l
netstat -r		|ip route
route add		|ip route add
route del		|ip route del
route -n		|ip route show
vconfig			|ip link

## 使用示例
1.启动关闭网卡
```
ip link set eth0 up/down
```

2.为网卡添加/删除IP地址
```
ip addr add/del 192.168.0.2/24 dev eth0（ifconfig eth0 0）
```

3.添加默认网关
```
ip route add default via 192.168.0.1
```

4.修改mac地址
```
ip link set dev eth0 address 09:00:27:25:2a:67（ifconfig eth0 hw ether 09:00:27:25:2a:67）
```

5.添加/删除静态ARP项
```
ip neigh add 192.168.0.2 lladdr 09:00:27:25:2a:67 dev eth0
ip neigh del 192.168.0.2 dev eth0
（arp -s和arp -d）
```

6.修改接口名称和MTU值
```
ip link set dev eth0 name lan0
ip link set dev lan0 mtu 1480
```

7.创建linux网桥，添加接口道网桥
```
ip link add name br0 type bridge
ip link set dev eth0 master br0（移除：ip link set dev eth0 nomaster）
```