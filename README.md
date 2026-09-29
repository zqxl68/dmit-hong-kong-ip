# DMIT香港原生IP：香港节点线路、套餐价格与原生 IP 核验方法一次看懂

想找 **DMIT香港原生IP**，真正需要确认的其实不是一句“香港 VPS”，而是三个问题：IP 的注册归属是不是香港、服务器到底走哪条网络、以及你准备购买的套餐是否真的符合自己的使用场景。

DMIT 目前的香港节点部署在 Equinix HK2，官方给出的香港到中国大陆参考延迟约为 15ms，参考丢包率低于 0.1%；网络侧提供 Premium、Eyeball、Tier 1 三种系列，硬件则有 AN5 和 AS3 两个平台。

但“原生 IP”和“低延迟线路”是两件事。一个香港数据中心 VPS 可以有香港归属 IP，也可以同时拥有普通国际线路；反过来，线路很好，也不代表某个具体 IP 一定能通过 Netflix、银行或其他平台的地域判定。

下面按这个思路拆开。

## DMIT 的香港 IP 到底算不算“原生”？

先说能核验到的部分。

公开的 APNIC WHOIS 记录显示，DMIT 的香港地址段 `103.135.248.0/24` 的网络名称为 `HK-DMIT-103-135-248-24`，国家/地区字段为 **HK**，并标注了香港地理坐标。这个结果至少证明 DMIT 有公开登记为香港的地址资源。

这和所谓“广播到香港机房、但 IP 登记在其他国家”的情况并不是同一回事。

不过，也别把这件事理解得过度绝对。**某一个公开香港地址段属于 HK，并不能自动证明你以后拿到的每一个具体 IP 都会被所有第三方数据库、流媒体平台或风控系统判定为“香港原生 IP”。**

更实际的做法，是拿到 VPS 后自己验证：

1. 查看 IP 的 WHOIS / RDAP 信息，看注册国家或地区。
2. 查看 BGP 与 ASN 路由归属，确认地址段的注册组织和广播来源。
3. 再用你实际要使用的平台测试地理位置识别。
4. 对流媒体、支付平台、广告平台这类服务，不要把“WHOIS 显示 HK”直接等同于“100% 可以解锁”。

这一区别很重要。

> **原生香港 IP ≠ 香港住宅 IP，也 ≠ 所有地区限制都能绕过。**

如果你的重点是网站、API、跨境业务、远程开发或需要一个稳定香港公网地址，那么 IP 注册归属和线路质量通常比单纯追求某个“解锁”标签更值得看。

## DMIT 香港三条线路，差别其实比套餐名字更重要

DMIT 当前香港节点提供三种网络系列。官方对它们的定位比较清楚：Premium 走 CN2 GIA；Eyeball 采用面向中国大陆用户的优化路由，但当前仍是 Beta；Tier 1 则更偏全球和亚太国际流量，不提供专门的中国大陆线路优化。

### Premium：CN2 GIA 优先

Premium 是香港节点里最明显针对中国大陆访问质量设计的一档。官方说明其使用 CN2 GIA（AS23764），香港到深圳的参考平均延迟约 15ms，参考丢包率低于 0.1%。官网推荐的场景包括面向中国大陆用户的网站、在线游戏、直播、低延迟交互服务以及跨境电商。

如果你搜“DMIT香港原生IP”，同时又对中国大陆访问速度有要求，那么真正该关注的是 **IP 属地 + Premium 路由** 两个维度，而不是只盯着香港两个字。

Premium 目前又分 AN5 和 AS3 两种硬件。AN5 使用 AMD EPYC 9005 系列、DDR5 ECC 和全 NVMe；AS3 则使用 AMD EPYC 7003 系列与全 NVMe。

### Eyeball：更便宜，但当前仍处于 Beta

Eyeball 的定位介于“国际线路”和“针对中国大陆优化”之间。官方称其会通过中国大陆相关的 eyeball ISP 路由提供更友好的访问体验，但明确写着 **HKG Eyeball 目前处于 Beta**，网络路由仍在调优，并且不建议把它用于对高稳定性有硬性要求的生产工作负载。

这句话比很多第三方“XX 三网优化”的宣传更值得注意。

如果你主要是个人项目、博客、API、测试机或混合中国大陆/海外访问，Eyeball 可以研究；如果是业务核心节点，Beta 状态本身就应该被计入决策。

### Tier 1：便宜、流量大，但不是中国大陆专项优化

Tier 1 是目前香港节点里价格最低的一条产品线。官方定位是 APAC、北美和欧洲的国际流量、备份、归档、CI/CD、监控和通用计算。官网明确说明它不提供针对中国大陆的专项路由增强。

所以 **$6.90/月的 HKG Tier 1** 很容易让人心动，但它解决的是“便宜的香港 VPS”问题，不是“最高优先级的中国大陆网络优化”问题。

## DMIT 香港全套餐对比表

以下按 DMIT 当前香港价格页公开展示的产品矩阵整理。官网当前香港页面显示 Premium、Eyeball、Tier 1 三条网络，以及 AN5、AS3 两个平台；价格页面同时提醒，产品和价格可能因调整而出现更新延迟，因此下单时仍应以结算页为准。

### Premium · AN5

| 套餐                 |      CPU |   内存 |   SSD |    月流量 |    端口 |    月付价格 | 计费 | 购买                                                            |
| ------------------ | -------: | ---: | ----: | -----: | ----: | ------: | -- | ------------------------------------------------------------- |
| HKG.AN5.Pro.MINI   |  4 vCore |  4GB |  80GB | 1500GB | 1Gbps | $149.90 | 月付 | [👉 购买 MINI](https://www.dmit.io/aff.php?aff=18446&pid=125)   |
| HKG.AN5.Pro.MICRO  |  4 vCore |  4GB | 160GB | 2000GB | 1Gbps | $199.90 | 月付 | [👉 购买 MICRO](https://www.dmit.io/aff.php?aff=18446&pid=126)  |
| HKG.AN5.Pro.MEDIUM |  6 vCore |  8GB | 160GB | 2500GB | 1Gbps | $279.90 | 月付 | [👉 购买 MEDIUM](https://www.dmit.io/aff.php?aff=18446&pid=127) |
| HKG.AN5.Pro.LARGE  |  8 vCore | 16GB | 320GB | 3000GB | 1Gbps | $359.90 | 月付 | [👉 购买 LARGE](https://www.dmit.io/aff.php?aff=18446&pid=128)  |
| HKG.AN5.Pro.GIANT  | 12 vCore | 24GB | 640GB | 6000GB | 1Gbps | $759.90 | 月付 | [👉 购买 GIANT](https://www.dmit.io/aff.php?aff=18446&pid=129)  |

这组产品是香港 Premium 的高规格 AN5 版本，当前公开价格从 $149.90/月起。第三方近期产品记录也能对应到相同的产品编号和参数。

### Premium · AS3

| 套餐                  |     CPU |  内存 |   SSD |    月流量 |    端口 |    月付价格 | 计费 | 购买                                                             |
| ------------------- | ------: | --: | ----: | -----: | ----: | ------: | -- | -------------------------------------------------------------- |
| HKG.AS3.Pro.TINY    | 1 vCore | 1GB |  20GB |  500GB | 1Gbps |  $39.90 | 月付 | [👉 购买 TINY](https://www.dmit.io/aff.php?aff=18446&pid=265)    |
| HKG.AS3.Pro.STARTER | 1 vCore | 2GB |  40GB | 1000GB | 1Gbps |  $79.90 | 月付 | [👉 购买 STARTER](https://www.dmit.io/aff.php?aff=18446&pid=266) |
| HKG.AS3.Pro.MINI    | 2 vCore | 4GB |  60GB | 1500GB | 1Gbps | $126.90 | 月付 | [👉 购买 MINI](https://www.dmit.io/aff.php?aff=18446&pid=267)    |
| HKG.AS3.Pro.MICRO   | 4 vCore | 4GB |  80GB | 2000GB | 1Gbps | $179.90 | 月付 | [👉 购买 MICRO](https://www.dmit.io/aff.php?aff=18446&pid=268)   |
| HKG.AS3.Pro.MEDIUM  | 4 vCore | 8GB | 160GB | 2500GB | 1Gbps | $239.90 | 月付 | [👉 购买 MEDIUM](https://www.dmit.io/aff.php?aff=18446&pid=269)  |

AS3 Premium 的 TINY 目前就是一个非常容易被搜索到的起点：**$39.90/月、1 vCore、1GB RAM、20GB SSD、500GB 流量、1Gbps**。近期公开补货信息仍能对应到这个产品和 PID 265。

### Eyeball · AN5

| 套餐                |      CPU |   内存 |   SSD |    月流量 |    端口 |    月付价格 | 计费 | 购买                                                            |
| ----------------- | -------: | ---: | ----: | -----: | ----: | ------: | -- | ------------------------------------------------------------- |
| HKG.AN5.EB.MINI   |  4 vCore |  4GB |  80GB | 2200GB | 1Gbps | $149.90 | 月付 | [👉 购买 MINI](https://www.dmit.io/aff.php?aff=18446&pid=156)   |
| HKG.AN5.EB.MICRO  |  4 vCore |  4GB | 160GB | 3000GB | 1Gbps | $199.90 | 月付 | [👉 购买 MICRO](https://www.dmit.io/aff.php?aff=18446&pid=157)  |
| HKG.AN5.EB.MEDIUM |  6 vCore |  8GB | 160GB | 4000GB | 1Gbps | $279.90 | 月付 | [👉 购买 MEDIUM](https://www.dmit.io/aff.php?aff=18446&pid=158) |
| HKG.AN5.EB.LARGE  |  8 vCore | 16GB | 320GB | 4500GB | 1Gbps | $359.90 | 月付 | [👉 购买 LARGE](https://www.dmit.io/aff.php?aff=18446&pid=159)  |
| HKG.AN5.EB.GIANT  | 12 vCore | 24GB | 640GB | 9000GB | 1Gbps | $759.90 | 月付 | [👉 购买 GIANT](https://www.dmit.io/aff.php?aff=18446&pid=160)  |

当前公开库存记录能够对应 AN5 EB 的完整大规格梯度，其中 GIANT 为 12 vCore、24GB、640GB SSD、9000GB 流量、$759.90/月。

### Eyeball · AS3

| 套餐                 |     CPU |  内存 |   SSD |    月流量 |    端口 |    月付价格 | 计费 | 购买                                                             |
| ------------------ | ------: | --: | ----: | -----: | ----: | ------: | -- | -------------------------------------------------------------- |
| HKG.AS3.EB.TINY    | 1 vCore | 1GB |  20GB |  800GB | 1Gbps |  $39.90 | 月付 | [👉 购买 TINY](https://www.dmit.io/aff.php?aff=18446&pid=210)    |
| HKG.AS3.EB.STARTER | 1 vCore | 2GB |  40GB | 1500GB | 1Gbps |  $79.90 | 月付 | [👉 购买 STARTER](https://www.dmit.io/aff.php?aff=18446&pid=211) |
| HKG.AS3.EB.MINI    | 2 vCore | 4GB |  60GB | 2200GB | 1Gbps | $126.90 | 月付 | [👉 购买 MINI](https://www.dmit.io/aff.php?aff=18446&pid=212)    |
| HKG.AS3.EB.MICRO   | 4 vCore | 4GB |  80GB | 3000GB | 1Gbps | $179.90 | 月付 | [👉 购买 MICRO](https://www.dmit.io/aff.php?aff=18446&pid=213)   |
| HKG.AS3.EB.MEDIUM  | 4 vCore | 8GB | 160GB | 4000GB | 1Gbps | $239.90 | 月付 | [👉 购买 MEDIUM](https://www.dmit.io/aff.php?aff=18446&pid=214)  |

需要特别注意一个容易混淆的变化：较早资料里可以看到 HKG Eyeball 的 `v2` 命名以及更低的流量规格，但 DMIT 当前香港价格页已经展示为 **TINY 800GB、STARTER 1500GB、MINI 2200GB、MICRO 3000GB、MEDIUM 4000GB**；近期库存记录也与这一组数字吻合。

### Tier 1 · AS3

| 套餐                 |     CPU |   内存 |   SSD |                     流量 |        价格 | 计费 | 购买                                                             |
| ------------------ | ------: | ---: | ----: | ---------------------: | --------: | -- | -------------------------------------------------------------- |
| HKG.AS3.T1.WEE     | 1 vCore |  1GB |  20GB |   1000GB Max (IN, OUT) |  $36.90/年 | 年付 | [👉 购买 WEE](https://www.dmit.io/aff.php?aff=18446&pid=197)     |
| HKG.AS3.T1.TINY    | 1 vCore |  1GB |  20GB |   2000GB Max (IN, OUT) |   $6.90/月 | 月付 | [👉 购买 TINY](https://www.dmit.io/aff.php?aff=18446&pid=198)    |
| HKG.AS3.T1.STARTER | 1 vCore |  2GB |  40GB |   4000GB Max (IN, OUT) |  $12.90/月 | 月付 | [👉 购买 STARTER](https://www.dmit.io/aff.php?aff=18446&pid=199) |
| HKG.AS3.T1.MINI    | 2 vCore |  2GB |  60GB |   8000GB Max (IN, OUT) |  $21.90/月 | 月付 | [👉 购买 MINI](https://www.dmit.io/aff.php?aff=18446&pid=200)    |
| HKG.AS3.T1.MICRO   | 4 vCore |  4GB |  80GB |  16000GB Max (IN, OUT) |  $32.90/月 | 月付 | [👉 购买 MICRO](https://www.dmit.io/aff.php?aff=18446&pid=201)   |
| HKG.AS3.T1.MEDIUM  | 4 vCore |  8GB | 160GB |  32000GB Max (IN, OUT) |  $49.90/月 | 月付 | [👉 购买 MEDIUM](https://www.dmit.io/aff.php?aff=18446&pid=202)  |
| HKG.AS3.T1.LARGE   | 8 vCore | 16GB | 320GB |  64000GB Max (IN, OUT) |  $99.90/月 | 月付 | [👉 购买 LARGE](https://www.dmit.io/aff.php?aff=18446&pid=203)   |
| HKG.AS3.T1.GIANT   | 8 vCore | 24GB | 640GB | 128000GB Max (IN, OUT) | $199.90/月 | 月付 | [👉 购买 GIANT](https://www.dmit.io/aff.php?aff=18446&pid=204)   |

Tier 1 的一个显著特点是流量额度很高：当前官方页面列出的 TINY、STARTER、MINI、MICRO、MEDIUM、LARGE、GIANT 分别为 2TB、4TB、8TB、16TB、32TB、64TB、128TB 的 IN/OUT Max 级别，价格则从 $6.90/月一路到 $199.90/月。WEE 是特殊的年付产品，当前页面列为 $36.90/年。

官方当前香港页面没有在 Tier 1 这一段完整展示所有端口字段，所以这里不拿旧页面数据硬填，购买时应以对应订单页显示为准。

## 真正想要“香港原生 IP”，怎么买才不容易买错？

最容易犯的错误，就是看到三个字：**香港**。

实际上可以先把需求分成四种。

### 只需要一个香港公网 IP

这种情况下，Tier 1 就已经值得看。

尤其是监控、跳板、开发测试、备份、API 中转、低成本工具节点，$6.90/月的 HKG.AS3.T1.TINY 是目前官方公开价格里的最低月付入口。

[👉 查看 HKG Tier 1 套餐](https://www.dmit.io/aff.php?aff=18446&pid=198)

但不要因为它价格低，就默认它适合中国大陆用户访问。DMIT 自己对 Tier 1 的定位就是全球/亚太国际网络，而不是大陆专项优化。

### 需要香港 IP，同时比较在意中国大陆访问质量

这时候 Premium 的逻辑更清楚。

AS3 Premium 起价 $39.90/月；如果需要更强的 CPU 和更大规格，则可以直接看 AN5 Premium。当前香港 AN5 Premium 最低公开规格从 MINI 开始。

[👉 查看 HKG Premium 入门方案](https://www.dmit.io/aff.php?aff=18446&pid=265)

### 需要香港 IP，但业务不值得支付 Premium 的价格

Eyeball 的存在就是解决这类预算问题。

不过它现在处于 Beta，所以最好把它理解为“需要中国大陆相关优化、但可以接受路由仍在调整”的选择，而不是拿它直接替代成熟生产网络。

[👉 查看 HKG Eyeball 套餐](https://www.dmit.io/aff.php?aff=18446&pid=210)

### 你真正关心的是“IP 在香港，而且某个平台必须识别为香港”

那就别把购买决定完全建立在套餐名称上。

购买之前确认产品是 HKG，购买之后再验证实际分配的 IP。因为平台的地理定位、ASN 判断、商业数据中心标签以及 DNS/代理检测机制都可能不同。**WHOIS 是证据之一，不是全部证据。**

## AN5 和 AS3 怎么看？

如果只看硬件平台，DMIT 当前香港的差异相对简单。

AN5 是 AMD EPYC 9005 系列平台，使用 DDR5 ECC 和全 NVMe 存储；AS3 是 AMD EPYC 7003 系列，同样使用全 NVMe。官网把 AN5 放在更新一代的平台位置，而 AS3 则定位为成熟、强调性价比的硬件。

因此，对于一个已经能明确说明 CPU、内存、流量需求的项目，AN5 与 AS3 的比较有意义。

但如果你的核心问题只是“需要一个香港原生 IP”，不需要高 CPU，也不跑大型数据库，那么没必要为了 AN5 三个字就直接跳到 $149.90/月甚至更高的产品。

反过来，假如你的服务本身很吃 CPU、内存或 I/O，那么 Premium + AN5 的价格差就不应该只和 IP 做比较，而应该和整机资源一起比较。

## DMIT 香港当前有没有优惠？

目前能核验到一个针对香港 Tier 1 年付产品的官方优惠码：

`HKG-T1-ANNUALLY-45OFF-RECUR`

DMIT 的香港促销页面写明，该优惠码针对 **HKG Tier 1 STARTERv2 或更高方案的年付产品**，并且属于循环折扣。

这里有两个值得注意的地方。

第一，**WEE 和 TINY 不应该直接假设可以使用这张优惠码**。官方活动说明的适用范围是 STARTERv2 或更高。

第二，活动页本身不是当前 Pricing 页，且 DMIT 明确提醒价格和产品状态可能调整，所以即使网上仍能查到这个优惠码，也不要把某个第三方页面写的“永久有效”当成事实。结算页面能成功应用，才是最直接的当前验证。

如果你的目标恰好是香港 Tier 1 年付，实际下单时可以把这串码放进促销码输入框试一次，再确认结算金额是否变化。

## 一个经常被忽略的问题：流量用完后会发生什么？

VPS 套餐里的“流量”和“端口速度”不是一回事。

例如 Premium / Eyeball 套餐虽然都显示 1Gbps，但每月可用流量仍然只有几百 GB 到几 TB；Tier 1 的流量额度则明显更高。

因此，看到“1Gbps”不要直接理解成“每个月可以无限跑满 1Gbps”。

尤其是：

* 视频、下载、镜像分发；
* 大规模备份；
* CDN 源站；
* 高频跨境 API；
* 长时间大流量传输；

这些场景更应该先算月流量，而不是只看端口数字。

Tier 1 的优势就在这里：当前公开套餐最高可以做到 128000GB Max (IN, OUT)。如果你的项目主要是高流量国际传输，而不是中国大陆访问质量，那么它的产品逻辑和 Premium 完全不同。

## 买到之后，怎么自己确认“香港原生 IP”？

可以做一个很简单的四步检查。

### 第一步：看 WHOIS / RDAP

检查分配给你的 IPv4 是否显示 HK，注册组织是谁，地址段是否与 DMIT 的香港资源相关。

公开 APNIC 记录至少可以看到 DMIT 的香港地址块存在明确的 HK 注册信息。

### 第二步：看 BGP

确认 IP 的 ASN、前缀和广播来源。这样可以排除一部分“服务器在香港、IP 实际登记在别处”的情况。

### 第三步：看地理数据库

不同数据库的结果可能并不完全一致。所以不要只查一个服务。

一个数据库显示 Hong Kong，另一个数据库显示 Singapore，并不一定说明 VPS 有问题；真正应该看的是多数据源结果，再结合 ASN 和前缀注册信息判断。

### 第四步：测试目标平台

如果你买这个 IP 是为了某个具体服务，就直接测试那个服务。

想要香港本地搜索结果，就测试搜索与地图类服务。

想要香港区流媒体，就测试对应流媒体。

需要香港支付或广告环境，就测试实际业务后台。

这个结果比一句“原生 IP”更有用，因为你最终付钱买的是 **实际可用性**。

## 常见问题

### DMIT 香港 IP 是原生 IP 吗？

公开 APNIC 记录能验证 DMIT 拥有登记为 HK 的香港地址资源，例如 `103.135.248.0/24`；但不能据此保证所有具体分配 IP 都能被所有平台统一判定为“原生香港 IP”。拿到实例后，对实际 IP 做 WHOIS、BGP 和目标平台测试更稳妥。

### DMIT 香港 Premium 和 Eyeball 最大区别是什么？

Premium 使用 CN2 GIA，并以中国大陆访问质量为重要目标；Eyeball 则采用成本更低的中国大陆相关优化路径，而且 DMIT 当前明确把香港 Eyeball 标记为 Beta。

### HKG Tier 1 为什么这么便宜？

因为它的定位不是中国大陆专项优化线路。官方把 Tier 1 放在全球、亚太、备份、归档和通用计算场景，因此它和 Premium 在网络目标上根本不是同一种产品。

### DMIT 香港最便宜的套餐是多少？

按当前官方香港页面，月付最低是 **HKG.AS3.T1.TINY，$6.90/月**；另外还有特殊年付产品 HKG.AS3.T1.WEE，当前列价为 **$36.90/年**。

### 想要香港原生 IP，又希望中国大陆访问尽量稳定，应该重点看什么？

先看 IP 的香港注册归属，再看 Premium / Eyeball / Tier 1 的线路类型。对于中国大陆访问质量要求更高的项目，Premium 与 Tier 1 不应混为一谈；对于生产环境，也要注意香港 Eyeball 当前仍处于 Beta。

## 最后把选择逻辑压缩成一句话

**DMIT香港原生IP** 真正值得比较的不是“香港”两个字，而是 **IP 归属、网络线路、硬件规格、流量额度和你的实际业务目标**。

只想要便宜香港节点，Tier 1 已经可以看。

需要中国大陆方向优化，Premium 更符合产品定位。

想在两者之间找成本平衡，可以研究 Eyeball，但要记住它目前仍是 Beta。

至于“原生 IP 能不能解锁某个平台”，不要提前替平台下结论。先拿到真实 IP，再测。这样比任何套餐宣传页上的四个字都可靠。
