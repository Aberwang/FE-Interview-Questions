# 网络篇
## Q1：从地址栏输入URL到呈现页面--浏览器解析渲染页面过程

`腾讯一面`

> 分析:常规问题,考察基本网络原理和浏览器渲染过程

A1：总体来说过程如下:

地址栏输入URL后->DNS将域名解析成IP地址->建立TCP连接->发送HTTP请求->服务器处理请求并返回HTTP报文->浏览器解析渲染页面
### 1.0：（扩展）DNS--解析顺序&递归查询和迭代查询
- 解析顺序：按照浏览器缓存，系统缓存，路由器缓存，ISP（运营商）DNS缓存，根域名服务器，顶级域名服务器，主域名服务器逐步读取，直到拿到IP地址
- DNS递归查询和迭代查询：从客户端到本地DNS服务器是属于递归查询，而DNS服务器之间就是的交互查询就是迭代查询
### 1.1、浏览器解析渲染过程，见[HTML篇1.0](https://github.com/okaychen/FE-Interview-Questions/blob/master/interview/foundation/basis.md#1浏览器解析渲染页面过程)

## Q2：建立和释放TCP连接的过程

`腾讯一面`

> 分析：建立TCP连接的过程，3次握手；释放连接会是怎样？为什么要4次挥手

A2：建立TCP连接的过程：三次握手，客户端发送寻址请求-->服务端收到报文请求，回应给客户端-->客户端收到服务器报文回应，发出连接请求

### Q2.0：释放连接的过程是四次挥手，相比建立连接过程为什么要多一次？
A2.0：因为服务端收到SYN建连报文后，可以把ACK报文和SYN报文放在一起发送。但是当关闭连接的时候，当对方收到FIN报文通知时，仅仅表示对方已经无数据发送给你了，但未必你已经发送完全部数据，这时就不能马上关闭socket，所以释放连接过程SYN包和ACK包要分开发送。