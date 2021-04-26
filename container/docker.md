## Container VS virtual machine

虚拟机技术是对硬件资源的虚拟，容器技术则是对进程的虚拟，从而提供了更轻量级的虚拟化，实现进程了资源的隔离。从架构来看，容器比虚拟机少了 Hypervisor 层和 Guest OS 层，使用 Docker Engine 进行资源分配并
调用 Linux 内核 namespace API 进行隔离，所以应用共用主机操作系统。因此，在体量上看， Docker 比虚拟机更轻量化。（Kubernetes in action）


## Container network

在安装完 Docker 以后，Docker Daemon 会在宿主主机上自动创建三个网络，分别是 `bridge` 、`host`、`none`，

```
$  docker network ls
NETWORK ID     NAME      DRIVER    SCOPE
976baf4da021   bridge    bridge    local
b979b941db03   host      host      local
1d4d634f5ca4   none      null      local
```


### Bridge 模式

这是 docker 的默认网络模式，

```
$ brctl show
bridge name	bridge id		STP enabled	interfaces
docker0		8000.0242d275aedb	no		
```

Run a container

```
$ docker run -d --rm dllhb/devopsday:v0.9
$brctl show
bridge name	bridge id		STP enabled	interfaces
docker0		8000.0242d275aedb	no		vethad6503d
```
可以看到 bridge  veth pair 的一端 `vethad6503d` 已经挂载到网桥 `docker0`上了。

进入容器查看网络情况
```
$ ifconfig
eth0      Link encap:Ethernet  HWaddr 02:42:AC:12:00:02
          inet addr:172.18.0.2  Bcast:172.18.255.255  Mask:255.255.0.0
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:13 errors:0 dropped:0 overruns:0 frame:0
          TX packets:0 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0
          RX bytes:1046 (1.0 KiB)  TX bytes:0 (0.0 B)

lo        Link encap:Local Loopback
          inet addr:127.0.0.1  Mask:255.0.0.0
          UP LOOPBACK RUNNING  MTU:65536  Metric:1
          RX packets:0 errors:0 dropped:0 overruns:0 frame:0
          TX packets:0 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000
          RX bytes:0 (0.0 B)  TX bytes:0 (0.0 B)
```

### Host 模式

连接到host网络的容器共享 Docker host 的网络栈，容器将不会虚拟出自己的网卡，配置自己的 IP，而是使用宿主机的 IP 和端口。

```
$ docker run -d  --rm --network=host dllhb/devopsday:v0.9
```

进入容器查看网络情况

```
$ ifconfig
br-6a45bd67f9ec Link encap:Ethernet  HWaddr 02:42:9D:BA:67:B7
          inet addr:172.20.0.1  Bcast:172.20.255.255  Mask:255.255.0.0
          UP BROADCAST MULTICAST  MTU:1500  Metric:1
          RX packets:0 errors:0 dropped:0 overruns:0 frame:0
          TX packets:0 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0
          RX bytes:0 (0.0 B)  TX bytes:0 (0.0 B)

br-ccd4a1648c14 Link encap:Ethernet  HWaddr 02:42:A2:BE:6A:D6
          inet addr:172.19.0.1  Bcast:172.19.255.255  Mask:255.255.0.0
          inet6 addr: fe80::42:a2ff:febe:6ad6/64 Scope:Link
          UP BROADCAST MULTICAST  MTU:1500  Metric:1
          RX packets:91172 errors:0 dropped:0 overruns:0 frame:0
          TX packets:119669 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0
          RX bytes:4376241 (4.1 MiB)  TX bytes:13687502 (13.0 MiB)

docker0   Link encap:Ethernet  HWaddr 02:42:D2:75:AE:DB
          inet addr:172.18.0.1  Bcast:172.18.255.255  Mask:255.255.0.0
          inet6 addr: fe80::42:d2ff:fe75:aedb/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:1314081 errors:0 dropped:0 overruns:0 frame:0
          TX packets:1507718 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0
          RX bytes:68523608 (65.3 MiB)  TX bytes:405947963 (387.1 MiB)

eth0      Link encap:Ethernet  HWaddr 00:16:3E:0E:75:5E
          inet addr:172.17.69.196  Bcast:172.17.79.255  Mask:255.255.240.0
          inet6 addr: fe80::216:3eff:fe0e:755e/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:15322278 errors:0 dropped:0 overruns:0 frame:0
          TX packets:9242529 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000
          RX bytes:11633178910 (10.8 GiB)  TX bytes:1733633091 (1.6 GiB)

lo        Link encap:Local Loopback
          inet addr:127.0.0.1  Mask:255.0.0.0
          inet6 addr: ::1/128 Scope:Host
          UP LOOPBACK RUNNING  MTU:65536  Metric:1
          RX packets:581303 errors:0 dropped:0 overruns:0 frame:0
          TX packets:581303 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000
          RX bytes:46057754 (43.9 MiB)  TX bytes:46057754 (43.9 MiB)

vethad6503d Link encap:Ethernet  HWaddr AA:70:B4:08:E8:5F
          inet6 addr: fe80::a870:b4ff:fe08:e85f/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:0 errors:0 dropped:0 overruns:0 frame:0
          TX packets:15 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0
          RX bytes:0 (0.0 B)  TX bytes:1186 (1.1 KiB)
```
可以看到容器内部完全可以看到宿主机的网络信息。host 模式的优点

* 没有性能损耗且配置方面

缺点

* 容器没有隔离、独立的网络栈：容器因与宿主机共用网络栈而争抢网络资源，并且容器崩溃也可能使主机崩溃，导致网络的隔离性不好；
* 端口资源冲突：宿主机上已经使用的端口就不能再用了。


### container 模式

创建容器时使用 `--network=container:NAME_or_ID` 模式，在创建新的容器时指定容器的网路和一个个已经存在的容器共享一个 network namespace，但是并不为 Docker 容器进行任何网络配置，这个 Docker 容器
没有网卡、IP、路由等信息，需要动手为 Docker 绒球 添加网卡、配置 IP 等。

### none 模式

none 模式下的容器只有 lo 回环网络，没有其他网卡。none 网络属于完全封闭的网络。唯一的用户是客户有充分的自由度做自己后续的配置。

```
$ docker run -d --rm --network=none dllhb/devopsday:v0.9
$ ifconfig
lo        Link encap:Local Loopback
          inet addr:127.0.0.1  Mask:255.0.0.0
          UP LOOPBACK RUNNING  MTU:65536  Metric:1
          RX packets:0 errors:0 dropped:0 overruns:0 frame:0
          TX packets:0 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000
          RX bytes:0 (0.0 B)  TX bytes:0 (0.0 B)
```

