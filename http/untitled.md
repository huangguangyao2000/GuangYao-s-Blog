# HTTP-11-补充

## 传输层

主要是为不同主机上不同进程之间提供逻辑通信的功能

### 多路复用与多路分解

* 将传输层报文段中的数据交付到正确的套接字的工作为**多路分解**
* 在源主机上从不同的套接字中收集数据，封装头信息生成报文段后，将报文段传递到网络层，此过程为**多路复用**

  **UDP协议**

  此协议为**无连接的不可靠的**传输层协议。提供了传输层需要实现的最低限度的功能。适用于实时性要求高的场景。

  **特点；**

* 没有握手过程，没有连接的时延。
* 不保证数据的可靠交付
* 没有拥塞控制和流量控制的机制
* 支持一对一，一对多，多对一，多对多的通信
* 首部小，只有8个字节

  **TCP连接**

  面向连接，提供可靠数据传输服务的传输层协议。

* 提供点对点的服务
* 全双工的服务
* 拥塞控制和流量控制

  **TCP四次挥手**

![](https://img-blog.csdn.net/20170606084851272?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvcXpjc3U=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

#### ARQ协议

自动重传请求，通过超时和重传来保证数据的可靠交付。

**停止ARQ协议**

**连续ARQ协议**

### 网络层

主要实现了不同主机之间的逻辑通信功能，包含 两个主要的组件，**IP网际协议和路由选择协议**

### 数据链路层

### 物理层
