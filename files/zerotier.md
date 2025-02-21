# ZeroTier快速上手

## 0. 为什么要用它？

**优点**：

* 可以在Linux、Mac OS、Windows等跨平台使用

* 能够实现内网穿透，所外网络访问内部设备，支持远程桌面（所VPN不支持）

**缺点**：

* 对用户端网络质量要求较高，ping延迟在200以上会格外卡顿

## 1. 下载

https://www.zerotier.com/download/

服务端已经配置好，下载自己终端系统对应的客户端即可

# 2. 使用

## 2.1 创建网络

https://my.zerotier.com/network/fada62b015c3578c

* 在这个链接里可以搭建自己的VPN网络，得到网络的ID。建议自己搭建自己设备的网络，如果一个网络组设备较多，可能会降低连接速度
* 在用户端通过ID加入网络，刷新列表可以找到现在新加入的设备
* 加入后一定要Authorize才能生效，同时要修改IP，保证所有的设备都在**同个网段**里

## 2.2 加入网络

#### Linux：
查看工具状态：

```
sudo systemctl status zerotier-one.service
```

加入新的网络：

```
sudo zerotier-cli join <network-id>
```

加入新网络后，需要重启工具：

```
sudo systemctl restaer zerotier-one.service
```

查看是否生效：

```
ifconfig
```

#### Mac OS、Windows：

直接在客户端上找到加入网络的入口，输入网络ID加入后即可

MacOS查看是否生效：

```
ifconfig
```

Windows查看是否生效：

```
ifconfig
```

### 2.3 注意

如果在VPN下多次尝试连接失败，**一定要过段时间再连接**，否则可能会被所里误判为挖矿行为，需要重装系统才能解决，非常麻烦！