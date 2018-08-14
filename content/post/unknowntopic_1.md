---
title: "新的東西"
date: 2018-07-22T09:36:27+08:00
draft: true
authors: ["bradlee"]
---
1. [prometheus](https://prometheus.io/): 官網
    [使用Prometheus+grafana打造高逼格监控平台](http://blog.51cto.com/youerning/2050543): 监控不应该只是监控，除了及时有效的报警，更应该”好看”...
    [prometheus简单入门](https://blog.csdn.net/u010871982/article/details/77838592): prometheus的优势在于，它是一个基于服务的告警系统，针对不同的服务，有不同的exporter，可以实现不一样的效果.
    [开源监控 prometheus初体验](https://blog.csdn.net/u010453363/article/details/76689435): Prometheus在记录纯数字时间序列方面表现非常好。它既适用于面向服务器等硬件指标的监控，也适用于高动态的面向服务架构的监控。对于现在流行的微服务，Prometheus的多维度数据收集和数据筛选查询语言也是非常的强大。Prometheus是为服务的可靠性而设计的，当服务出现故障时，它可以使你快速定位和诊断问题。它的搭建过程对硬件和服务没有很强的依赖关系。
    [Prometheus原理和源码分析](http://www.infoq.com/cn/articles/Prometheus-theory-source-code): Prometheus（下称Prom）是一个基于Metrics的监控系统，与Kubernetes同属CNCF（Cloud Native Computing Foundation），它已经成为炙手可热的Kubernetes生态圈中的核心监控系统，越来越多的项目（如Kubernetes和etcd等 ）都加入了丰富的Prom原生支持，从侧面体现了社区对它的认可。
    [普羅米修斯 -- 快速構建你的業務監控平台](https://hk.saowen.com/a/a0b6b6e69d716b036cd4dd6aacf08ab8de8ca2a841d7085ffe2325cb151fbe35)

2. [Golang]():
    [go](https://tour.go-zh.org/welcome/1)
    [Go 程式設計教學：建立專案](https://cwchen.tw/golang-prog/project/)

3. edge computing:
    起因: 数据的增长速度远远超过了网络带宽的增速, 智能制造、无人驾驶等众多新型应用的出现，对"延迟"提出了更高的要求. 通过将从数据源到云计算中心数据路径之间的任意计算、存储和网络资源，组成统一的平台为用户提供服务，边缘计算作为一种新的计算模式，使数据在源头附近就能得到及时有效的处理. 这种模式不同于云计算要将所有数据传输到数据中心，绕过了网络带宽与延迟的瓶颈. 在产业界和学术界的合力推动下，边缘计算正在成为新兴万物互联应用的支撑平台。
    边缘计算并不是为了取代云计算，而是对云计算的补充和延伸，为移动计算、物联网等提供更好的计算平台。边缘计算模型需要云计算中心的强大计算能力和大量存储的支持，而云计算也同样需要边缘计算中边缘设备对于大量数据及隐私数据的处理，从而满足实时性、隐私保护和降低能耗等需求。 [3]

    边缘计算：EDGE COMPUTING 编辑
    《边缘计算》 [1]  一书由施巍松、刘芳、孙辉、裴庆祺编著，科学出版社2018年1月出版。

    在全球范围内来说，云（cloud）是这一进程中不可或缺的一部分。不幸的是，随着云与用户之间的距离越来越大，传输延迟也越来越大。而边缘计算（Edge Computing ）已经被证明是桥接云和用户之间距离的一种有效的方式。
