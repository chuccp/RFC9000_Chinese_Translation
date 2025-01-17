---
title: "14.2 路径最大传输单元"
anchor: "14.2_Path_Maximum_Transmission_Unit"
weight: 1420
rank: "h2"
---

PMTU指整个IP数据包的最大尺寸，包括IP头部、UDP头部和UDP载荷。UDP载荷包含一个或多个QUIC数据包头部和受保护的载荷。PMTU可能受路径特征影响因而随时间变化。终端的最大数据报尺寸指的是在某个给定时间，终端能发送的最大UDP载荷大小。

终端{{< req_level SHOULD >}}使用DPLPMTUD（[第14.3章]()）或PMTUD（[第14.2.1章]()）来认定一条通向目的地的路径是否支持一个期望的最大数据报尺寸且无需分段。在缺失这些机制时，QUIC终端{{< req_level SHOULD_NOT >}}发送比允许的最大数据报尺寸中的最小值还要大的数据报。

DPLPMTUD和PMTUD都会发送比当前的最大数据报尺寸更大的数据报，也就是**PMTU探测包**。所有不是在**PMTU探测包**中发送的QUIC数据包都{{< req_level SHOULD >}}具有适合最大数据报尺寸的尺寸以避免数据报被分段或丢弃（详见[RFC8085]()）。

如果QUIC终端认定某对本地IP地址和远程IP地址间的PMTU达不到1200字节，这个在允许的最大数据报尺寸中的最小值，那么它{{< req_level MUST >}}在受影响的路径上立即停止发送QUIC数据包，除了那些在**PMTU探测包**中的或包含**连接关闭帧**的数据包。如果无法找到备选路径，那么终端{{< req_level MAY >}}终止连接。

每对本地地址和远程地址可以有不同的PMTU。因此实现了任何一种PMTU发现的QUIC实现{{< req_level SHOULD >}}为每一对本地IP地址和远程IP地址的组合维护一个最大数据报尺寸。

QUIC实现{{< req_level MAY >}}更保守地计算最大数据报尺寸以允许未知的隧道开销或IP头部选项/扩展。
