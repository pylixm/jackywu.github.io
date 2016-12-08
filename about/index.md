---
layout: page
title: About Me
tags: [about]
modified: 2014-08-08T20:53:07.573882-04:00
comments: true
image:
  feature: sample-image-2.jpg
  credit: WeGraphics
  creditlink: http://wegraphics.net/downloads/free-ultimate-blurred-background-pack/
---

# 个人简介

我是一个互联网技术人，居住在北京，不仅对技术感兴趣，还对管理学，心理学，经济，历史等领域都非常感兴趣。你可以通过如下方式了解和联系到我。

---

# 一、基本资料
**姓名** ：吴城  
**出生年月** ：1984  
**毕业院校** ：哈尔滨工程大学  
**学历**：本科  
**E-mail** ：jacky.wucheng@gmail.com / jacky.wucheng@icloud.com  
**工作年数** ：2008年至今  


![](/images/weixin-pic-jackywu.jpg)

# 二、职业规划

从最初的`IDC工程师`到`高级开发工程师`，到后来作为`技术主管`带团队做项目，以及目前作为`架构师`带领团队做基础平台型项目的研发，历时约8年时间的技术积累和管理经验积累，我的视野跟格局得到了很大的提升，并且注意力发生了转移，不再仅仅关注技术，而是更加关注技术带来的价值，只有产品才能够带来直接的价值。所以，我希望未来能够带领更大的团队进行产品研发。

我偏向的领域主要有

1. “互联网+”对传统行业的改造
1. 物联网
1. 智能交通

# 三、工作经历

* 2014.10-至今，2年左右，汽车之家
* 2009.1-2014.9，5年半，新浪
* 2008.6-2008.12，半年，网易

# 四、项目经历

## 2014.10-至今，汽车之家

负责汽车之家系统平台部的研发管理工作

* 带领团队，基于Puppet ENC架构，从零研发“配置管理系统CMS”，支持linux上的Tomcat，Nginx，LVS，Codis和windows上的IIS的自动化安装配置。可以参考 [汽车之家运维团队倾力打造的配置管理系统AutoCMS](http://mp.weixin.qq.com/s?__biz=MzA3MzYwNjQ3NA==&mid=2651296455&idx=1&sn=ae9ff5e7f3a103559d690b79dfae1962&scene=0#wechat_redirect)
* 带领团队，基于SaltStack Execution Module二次开发，从零建设标准，开发”代码发布系统PushGuide”，接入了公司大部门核心业务线的发布工作。可以参考 [终结人肉上线，使用代码发布系统PushGuide](http://mp.weixin.qq.com/s?__biz=MzA3MzYwNjQ3NA==&mid=2651296847&idx=1&sn=9f5c03364f36032a390b0929d3b8e558#rd)
* 带领团队，基于“生命周期管理 + 状态机”的思路，从零开发”资产管理系统CMDB“，以”强流程 + 自动化“的方法保证数据准确。可以参考 [汽车之家CMDB设计思路](http://mp.weixin.qq.com/s?__biz=MzA5NTAxNjQyMA==&mid=2654543617&idx=1&sn=f97d01906a52919cd059308933c7d6cd&scene=4#wechat_redirect)
* 带领团队，基于OpenFalcon作为底层，自研上层产品方案，开发自有监控系统。
* 带领团队，开发”私有云平台“，以”工单 + 状态机"的思路，整合系统平台部内部的子系统，对业务部门提供统一的服务申请入口，向PaaS转型。

除了技术和日常管理事务之外，还对团队成员的非技术能力进行了培训

* [事务管理GTD](http://jackywu.github.io/articles/事务管理分享/)
* [知识管理](http://jackywu.github.io/articles/知识管理/)
* [招聘方法](http://jackywu.github.io/articles/招聘方法/)
* [项目管理](http://jackywu.github.io/articles/项目管理方法/)

通过这两年的经验累积，自己的技术和管理能力提升了一个台阶。

## 2009.1-2014.9，新浪

**1、2012-2014.9，研发部平台架构组，技术主管**

负责SinaEdge CDN平台的研发工作，带领团队进行技术研发。做了如下重点开发工作：

GSLB全局流量调度器优化，提升可靠性和精准度

- 调度器配合EdgeServer实现回源Failover功能，以提升回源成功率。
- 调度器自动化IP库更新机制开发，提升调度精准度。
- 权威DNS和递归DNS实现Edns-Subnet功能，以实现用户精准调度和回源精准调度的目的。
- 自动化调度系统的原型开发，以提高平台稳定性和服务质量。

运维自动化，提升运维效率

- 基于puppet的自动化配置管理系统。

还负责视频转码平台SinaTrans的研发和运维工作。该平台实现了常见视频格式的编解码功能，承载了新浪原生视频，新浪微盘，秒拍这几个主要产品。主要特性包括：

- 输出ts+m3u8，mp4，flv等格式，支持pc端和手机端的视频播放。
- 制定了该平台的数据体系，分析和考评该平台的性能和可靠性。
- 基于 NVIDIA GPU NVENC 转码工具的原型开发。

除了技术工作之外，还包括：

- 引导团队根据公司目标自主进行技术调研，行业调研，共同制定年度绩效目标，制定开发计划。
- 组织团队内、外的技术分享，加强技术交流和学习。
- 组织线下活动，培养团队成员的融入感，增加团队交流活跃度。

**2、2011-2012，研发部平台架构组，高级系统开发工程师**

负责全新项目新浪CDN平台SinaEdge的架构设计和关键组件系统开发，带领10人的团队，建立了针对大/小文件优化的加速平台，统一配置管理部署中心，自动化系统和服务监控中心，自动化数据分析中心，全局流量调度器等子系统。在2011年中完成了SinaEdge1.0的release，提供了静态加速和动态加速的平台，在2012年底完成了SinaEdge2.0的release，提高了加速节点和调度器的性能。当时SinaEdge平台承担了新浪大部分静态业务的加速服务，如微博图片，微盘，视频等等，提供了250G的带宽输出。

**3、2010-2011，研发部平台架构组，系统开发工程师**

负责新浪全站图片服务系统(最大业务是微博图片)的应用运维和开发，并且在后续的架构改造中负责了架构设计和编码工作，去除了架构中的瓶颈Netapp Filer，实现了单IDC的Scale Out，实现了多IDC异步快速的数据同步，为公司节省了300万左右的Filer采购成本。

**4、2009-2010，公共服务事业部，系统管理员，PHP开发工程师**

负责新浪注册登录系统的运维和开发，负责团队并行开发的配置管理和代码发布(quickbuild)，负责“IM在线系统”的运维和后续架构优化项目的架构设计、开发和多IDC冗余部署方案的设计。改造后的系统满足了容量翻倍的业务需求，并且具备了Scale Out的能力，简化了业务流程，降低了运维成本。 

## 2008.6-2008.12，网易

**网络系统部，IDC系统工程师**

负责IDC服务器/网络设备上下线，机架部署，网络布线，故障处理和巡检，掌握了IDC相关工作的规范和流程，对大规模系统的工业化部署和运维提供了技术积累。

# 五、个人作品

* 个人Blog：<http://jackywu.github.io>
* Github：<https://github.com/jackywu>
* 原创文章
    * [GTD事务管理](http://jackywu.github.io/articles/事务管理分享/)
    * [Saltstack net-api Runner/Local模块调用分析](http://jackywu.github.io/articles/saltstack_net_api_runner_local_call/)
    * [SaltStack源码分析 - 任务处理机制](http://jackywu.github.io/articles/saltstack源码分析/)
    * [Zabbix_server源码分析](http://jackywu.github.io/articles/zabbix_server源码分析/)
    * [PDNS-Recursor源码分析之dns server的选择原理](http://jackywu.github.io/articles/pdns_recursor源码分析之dns_server的选择原理/)
    * [Puppet Agent源码分析之Agent启动和Run Rest-API的实现](http://jackywu.github.io/articles/puppet_agent源码分析之agent启动和run_rest_api的实现/)
* 管理和审核 [汽车之家运维团队技术文章](http://autohomeops.corpautohome.com)

