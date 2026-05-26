---
tags:
  - 计算机网络
---
# DHCP

**what：**
动态主机设置协议，基于 UDP 实现的应用层协议

**why：**
用于 自动网络配置 （根据 DHCP客户端 的请求，DHCP服务端 返回 IP地址、网关地址、子网掩码、DNS服务器 等网络配置参数）

**工作流程** ：
1. DHCP客户端       广播  DHCP发现报文（DHCP DISCOVER）
2. DHCP服务器收到后 广播  DHCP提供报文（DHCP OFFER）
3. DHCP客户端可能收到多个服务器的 DHCP提供报文，选择一个，广播  DHCP请求报文（DHCP REQUEST） -> 告诉选中的服务器使用该IP，告诉其他服务器 "已选择其他IP"
4. 被选中的 DHCP服务器 收到后，广播  DHCP确认报文（DHCP ACK），确认IP分配；客户端就可以使用该IP了

```
在 linux 中，网络管理器（network manager）作为 DHCP客户端， 路由器作为 DHCP服务端
```