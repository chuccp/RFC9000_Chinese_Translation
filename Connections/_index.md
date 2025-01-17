---
title: "5. 连接"
anchor: "5_Connections"
weight: 500
rank: "h1"
---

QUIC连接在客户端与服务端之间共享状态。

QUIC连接从握手开始。在握手的过程中，双端使用加密握手协议（[QUIC TLS]()）创建一个共享密钥并协商应用协议。握手过程（[第7章]()）确认双端的交流意愿（[第8.1章]()），并确立连接的各项参数（[第7.4章]()）。


应用层协议可以在连接握手阶段使用连接，但这种使用是有所限制的。0-RTT准许客户端在收到服务端回复前发送应用数据，但是没有抵御回放攻击的措施，详见《[QUIC TLS]()》第9.2章。服务端也可以在收到客户端的最终加密握手信息前发送应用数据，此时服务端尚未确认客户端的身份，也未确认客户端是否存活。应用层协议可以在安全性与降低延迟之间权衡，以决定是否使用这些功能。

连接ID（[第5章]()）的存在使得连接可以迁移到新的网络通道上，这不仅可以是终端的主动选择，也可以是在网络中间件发生变更后的被动选择。[第9章]()描述了如何缓解连接迁移带来的安全和隐私问题。

对于不再需要的连接，有几种方法可以让客户端和服务端将其关闭，详见[第10章]()。
