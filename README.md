# 搬瓦工 DC9 CN2 GIA：三网回程直连的洛杉矶机房，GIA-E 套餐怎么选、DC6 与 DC9 区别一次说清

搜“搬瓦工 DC9 CN2 GIA”的人，多半是被一句话种草的：三网回程全部走高端线路，晚高峰不丢包。但真到下单的时候就会发现一个尴尬的问题——搬瓦工官网并没有一个叫“DC9 套餐”的东西直接摆在那让你买。DC9（机房代号 USCA_9，位于美国洛杉矶）更多是作为一个可选机房存在的，常规入手路径是买 CN2 GIA-E 套餐再免费迁移过去；另有不定期补货的限量版可以直达。

这篇文章把这件事掰开讲清楚：DC9 的线路到底强在哪、和 DC6 怎么选、限量版和 GIA-E 套餐的区别、目前官网全系列套餐的价格，以及怎么用优惠码少花一点。价格和套餐信息均来自搬瓦工官网当前展示页面和多个持续更新的第三方整理，具体以结算页面为准。

## DC9 CN2 GIA 是个什么机房

先说结论：DC9 是搬瓦工洛杉矶机房里线路定位最高的一个。

官方对 USCA_9 的描述是“整体网络容量和稳定性最佳”的数据中心。发往中国大陆方向的流量会分发给三条高端线路：电信 CN2 GIA（AS4809）、联通高端链路（AS10099）、移动 CMIN2（AS58807）。也就是说，不管你用的是电信、联通还是移动的宽带，回程走的都是各家自己的“优先级通道”，而不是大家平时吐槽的拥堵骨干网。

搬瓦工在洛杉矶有两个 CN2 GIA 机房（DC6 和 DC9），两个机房加起来有 8 条 10Gbps 级别的 CN2 GIA/CTGNet 链路，同时和 Google 等本地运营商直连互联。DC9 机房在 2025 年还完成了一轮硬件升级，换上了 AMD EPYC 处理器和 NVMe RAID-10 存储。

顺带说一个官方页面上的冷知识，它能解释很多东西：CN2 GIA 的线路成本非常高，按官方说法，这类 IP transit 的价格最高可以到每 Mbps 120 美元，1Gbps 跑一个月大约是 10 万美元级别的账单，而且容量非常有限。所以 CN2 GIA 线路基本不具备抗 DDoS 能力，一旦被攻击，IP 会被直接置空（nullroute）来保护线路。这也是为什么 DC9 的 IP 质量普遍不错，但“娇贵”——好用，但经不起折腾。

## 实际表现：延迟、丢包和测试入口

社区里流传比较多的测评汇总给出的参考区间是：洛杉矶 DC6/DC9 到国内延迟大约 140~180ms，晚高峰 CN2 GIA 线路的稳定性依然明显好于普通 163 骨干线路，丢包率很低。

自己动手测比看别人的图更有意义。第三方搭建的 DC9 演示站提供 [Speedtest 测速和 LookingGlass 路由测试](https://dc9.bwg.wiki/)，可以直接看到电信、联通、移动三个方向的去程回程路由。下单前先去测一下你本地到 DC9 的路由走向，比看任何测评文章都直观。

还有一点值得知道：DC9 常规系列的带宽是 1Gbps，而 GIA-E 系列是 2.5Gbps 起步、最高 10Gbps。如果你对带宽有要求，这个差异比“机房代号”本身更重要。

## DC9 和 DC6 怎么选

这是搜 DC9 的人绕不开的问题。两个机房都是洛杉矶的 CN2 GIA 机房，硬件和线路属于同一档次，差异主要在网络策略上：

| 对比项 | DC6（USCA_6） | DC9（USCA_9） |
| --- | --- | --- |
| 线路系列 | CN2 GIA-E（ECOMMERCE） | CN2 GIA |
| 带宽 | 2.5~10Gbps | 常规系列 1Gbps |
| 三网表现 | 三网更均衡，移动联通用户友好 | 三网回程均为高端线路，电信方向纯正 GIA |
| 入手方式 | GIA-E 套餐默认可选，常规在售 | 主要靠 GIA-E 迁移，或抢限量版 |
| 定位 | 大带宽、均衡型 | 官方口径中稳定性最佳 |

据多方测评的观察，DC6 的优化带宽冗余容量更大，并且与洛杉矶本地运营商有直接互联；DC9 的中国方向流量则更集中地走电信 CN2 GIA 通道。对于大多数建站和远程开发场景，两个机房的实际体验差距不大；如果你有执念或者被推荐到 DC9，用 GIA-E 套餐迁移过去就行，不需要为此改变购买决策。

## 怎么买到 DC9：两条路

**第一条：GIA-E 套餐 + 免费迁移（常规路径）**

这是目前最稳的入手方式。CN2 GIA-E 套餐购买后在 KiwiVM 后台可以直接把机器迁移到 DC9（USCA_9），迁移免费、不丢数据，机房随便换。GIA-E 套餐本身支持十几个机房位置，包括 DC6、DC9、日本大阪（JPOS_1）、荷兰（EUNL_9）等 CN2 GIA 级节点，以及所有常规 KVM 机房。

需要注意的是，机房之间可互迁的前提是有货：DC6 和 DC9 因为太抢手，某些时段会显示缺货，等一等再迁即可。

想直接看套餐和价格，可以👉[查看 CN2 GIA-E 套餐与 DC9 机房选项](https://bandwagonhost.com/aff.php?aff=79616&pid=87)。

**第二条：限量版套餐（看运气）**

搬瓦工隔一段时间会放限量版，历史上出过好几款能直达 DC9 的：

- **The DC9 Plan**：2024 年补货过几次，1 核/1GB/20GB/1.5Gbps 大带宽，年付 $38，用码后约 $35.42，三网 CN2 GIA；
- **DC9 CN2 GIA 限量版**：约 $79.99/年，同样只出不定期补货；
- **CN2 GIA-E 限量版**（$49.99/年、$89.99/年等版本）：已经下架，不再补货，老用户续费保留原价。

限量版没有固定补货规律，靠盯补货通知。能不能抢到全看手速，抢不到就老老实实走 GIA-E 常规套餐，其实配置和线路是一样的，只是价格贵一些。

## 全系列套餐与价格（官网当前在售）

下面按系列整理搬瓦工官网当前公开展示的全部套餐系列。价格均为美元，流量按月计。

**CN2 GIA-E（ECOMMERCE 系列，可选 DC9/DC6，进 DC9 的常规入口）**

| 套餐 | CPU/内存 | 硬盘 | 流量 | 带宽 | 价格（季付/年付或月付） | 购买 |
| --- | --- | --- | --- | --- | --- | --- |
| GIA-E 20G | 2核/1GB | 20GB | 1TB | 2.5Gbps | $49.99/季，$169.99/年 | [选购入门款](https://bandwagonhost.com/aff.php?aff=79616&pid=87) |
| GIA-E 40G | 3核/2GB | 40GB | 2TB | 2.5Gbps | $89.99/季，$299.99/年 | [选购 2GB 版](https://bandwagonhost.com/aff.php?aff=79616&pid=88) |
| GIA-E 80G | 4核/4GB | 80GB | 3TB | 2.5Gbps | $56.99/月 | [选购 4GB 版](https://bandwagonhost.com/aff.php?aff=79616&pid=89) |
| GIA-E 160G | 6核/8GB | 160GB | 5TB | 5Gbps | $86.99/月 | [选购 8GB 版](https://bandwagonhost.com/aff.php?aff=79616&pid=90) |
| GIA-E 320G | 8核/16GB | 320GB | 8TB | 5Gbps | $159.99/月 | [选购 16GB 版](https://bandwagonhost.com/aff.php?aff=79616&pid=91) |
| GIA-E 640G | 10核/32GB | 640GB | 10TB | 10Gbps | $289.99/月 | [选购 32GB 版](https://bandwagonhost.com/aff.php?aff=79616&pid=92) |
| GIA-E 1280G | 12核/64GB | 1280GB | 12TB | 10Gbps | $549.99/月 | [选购 64GB 版](https://bandwagonhost.com/aff.php?aff=79616&pid=93) |

**CN2 GIA SLA（洛杉矶，99.99% SLA，AMD EPYC + NVMe，每两周免费换 IP）**

| 套餐 | CPU/内存 | 硬盘 | 流量 | 带宽 | 价格 | 购买 |
| --- | --- | --- | --- | --- | --- | --- |
| SLA 20G | 2核/1GB | 20GB | 1TB | 2.5Gbps | $65.89/季，$239.99/年 | [选购 SLA 入门款](https://bandwagonhost.com/aff.php?aff=79616&pid=164) |
| SLA 40G | 3核/2GB | 40GB | 2TB | 2.5Gbps | $116.99/季，$399.99/年 | [选购 SLA 2GB 版](https://bandwagonhost.com/aff.php?aff=79616&pid=165) |
| SLA 80G | 4核/4GB | 80GB | 3TB | 2.5Gbps | $69.99/月 | [选购 SLA 4GB 版](https://bandwagonhost.com/aff.php?aff=79616&pid=166) |
| SLA 160G | 6核/8GB | 160GB | 5TB | 5Gbps | $109.99/月 | [选购 SLA 8GB 版](https://bandwagonhost.com/aff.php?aff=79616&pid=167) |
| SLA 320G | 8核/16GB | 320GB | 8TB | 5Gbps | $199.99/月 | [选购 SLA 16GB 版](https://bandwagonhost.com/aff.php?aff=79616&pid=168) |
| SLA 640G | 10核/32GB | 640GB | 10TB | 10Gbps | $369.99/月 | [选购 SLA 32GB 版](https://bandwagonhost.com/aff.php?aff=79616&pid=169) |
| SLA 1280G | 12核/64GB | 1280GB | 12TB | 10Gbps | $699.99/月 | [选购 SLA 64GB 版](https://bandwagonhost.com/aff.php?aff=79616&pid=170) |
| SLA 1280G（15TB 流量） | 12核/64GB | 1280GB | 15TB | 10Gbps | $879.99/月 | [选购大流量版](https://bandwagonhost.com/aff.php?aff=79616&pid=171) |
| SLA 1280G（20TB 流量） | 12核/64GB | 1280GB | 20TB | 10Gbps | $1159.99/月 | [选购超大流量版](https://bandwagonhost.com/aff.php?aff=79616&pid=172) |

**常规 KVM PROMO（价格最低的入门系列，不含 DC9，但可作为低成本备选）**

| 套餐 | CPU/内存 | 硬盘 | 流量 | 带宽 | 价格 | 购买 |
| --- | --- | --- | --- | --- | --- | --- |
| 20G KVM | 2核/1GB | 20GB | 1TB | 1Gbps | $49.99/年 | [选购年付入门款](https://bandwagonhost.com/aff.php?aff=79616&pid=44) |
| 40G KVM | 3核/2GB | 40GB | 2TB | 1Gbps | $52.99/半年，$99.99/年 | [选购 2GB 版](https://bandwagonhost.com/aff.php?aff=79616&pid=45) |
| 80G KVM | 4核/4GB | 80GB | 3TB | 1Gbps | $19.99/月 | [选购 4GB 版](https://bandwagonhost.com/aff.php?aff=79616&pid=46) |
| 160G KVM | 5核/8GB | 160GB | 4TB | 1Gbps | $39.99/月 | [选购 8GB 版](https://bandwagonhost.com/aff.php?aff=79616&pid=47) |
| 320G KVM | 6核/16GB | 320GB | 5TB | 1Gbps | $79.99/月 | [选购 16GB 版](https://bandwagonhost.com/aff.php?aff=79616&pid=48) |
| 480G KVM | 7核/24GB | 480GB | 6TB | 1Gbps | $119.99/月 | [选购 24GB 版](https://bandwagonhost.com/aff.php?aff=79616&pid=49) |

**亚洲 CN2 GIA 系列（香港/东京/大阪/新加坡，价格更高，延迟更低）**

| 机房 | 配置 | 流量 | 带宽 | 价格 | 购买 |
| --- | --- | --- | --- | --- | --- |
| 香港 40G | 2核/2GB/40GB | 500GB | 1Gbps | $89.99/月 | [选购香港入门款](https://bandwagonhost.com/aff.php?aff=79616&pid=95) |
| 香港 80G | 4核/4GB/80GB | 1TB | 1Gbps | $155.99/月 | [选购香港 4GB 版](https://bandwagonhost.com/aff.php?aff=79616&pid=96) |
| 香港 160G | 6核/8GB/160GB | 2TB | 1Gbps | $299.99/月 | [选购香港 8GB 版](https://bandwagonhost.com/aff.php?aff=79616&pid=97) |
| 香港 320G | 8核/16GB/320GB | 4TB | 1Gbps | $589.99/月 | [选购香港 16GB 版](https://bandwagonhost.com/aff.php?aff=79616&pid=98) |
| 香港 640G | 10核/32GB/640GB | 6TB | 1Gbps | $989.99/月 | [选购香港 32GB 版](https://bandwagonhost.com/aff.php?aff=79616&pid=122) |
| 香港 1280G | 12核/64GB/1280GB | 8TB | 1Gbps | $1889.99/月 | [选购香港顶配](https://bandwagonhost.com/aff.php?aff=79616&pid=124) |
| 东京 40G | 2核/2GB/40GB | 500GB | 1.2Gbps | $89.99/月 | [选购东京入门款](https://bandwagonhost.com/aff.php?aff=79616&pid=108) |
| 东京 80G | 4核/4GB/80GB | 1TB | 1.2Gbps | $155.99/月 | [选购东京 4GB 版](https://bandwagonhost.com/aff.php?aff=79616&pid=109) |
| 东京 160G | 6核/8GB/160GB | 2TB | 1.2Gbps | $299.99/月 | [选购东京 8GB 版](https://bandwagonhost.com/aff.php?aff=79616&pid=110) |
| 东京 320G | 8核/16GB/320GB | 4TB | 1.2Gbps | $589.99/月 | [选购东京 16GB 版](https://bandwagonhost.com/aff.php?aff=79616&pid=111) |
| 东京 640G | 10核/32GB/640GB | 6TB | 1.2Gbps | $989.99/月 | [选购东京 32GB 版](https://bandwagonhost.com/aff.php?aff=79616&pid=123) |
| 东京 1280G | 12核/64GB/1280GB | 8TB | 1.2Gbps | $1889.99/月 | [选购东京顶配](https://bandwagonhost.com/aff.php?aff=79616&pid=125) |
| 大阪 40G | 2核/2GB/40GB | 500GB | 1.5Gbps | $49.99/月 | [选购大阪入门款](https://bandwagonhost.com/aff.php?aff=79616&pid=134) |
| 大阪 80G | 4核/4GB/80GB | 1TB | 1.5Gbps | $86.99/月 | [选购大阪 4GB 版](https://bandwagonhost.com/aff.php?aff=79616&pid=135) |
| 大阪 160G | 6核/8GB/160GB | 2TB | 1.5Gbps | $165.99/月 | [选购大阪 8GB 版](https://bandwagonhost.com/aff.php?aff=79616&pid=136) |
| 大阪 320G | 8核/16GB/320GB | 4TB | 1.5Gbps | $329.99/月 | [选购大阪 16GB 版](https://bandwagonhost.com/aff.php?aff=79616&pid=137) |
| 大阪 640G | 10核/32GB/640GB | 6TB | 1.5Gbps | $549.99/月 | [选购大阪 32GB 版](https://bandwagonhost.com/aff.php?aff=79616&pid=138) |
| 大阪 1280G | 12核/64GB/1280GB | 8TB | 1.5Gbps | $1059.99/月 | [选购大阪顶配](https://bandwagonhost.com/aff.php?aff=79616&pid=139) |
| 新加坡 40G | 2核/2GB/40GB | 500GB | 1.5Gbps | $49.99/月 | [选购新加坡入门款](https://bandwagonhost.com/aff.php?aff=79616&pid=173) |
| 新加坡 80G | 4核/4GB/80GB | 1TB | 1.5Gbps | $86.99/月 | [选购新加坡 4GB 版](https://bandwagonhost.com/aff.php?aff=79616&pid=174) |
| 新加坡 160G | 6核/8GB/160GB | 2TB | 2.5Gbps | $165.99/月 | [选购新加坡 8GB 版](https://bandwagonhost.com/aff.php?aff=79616&pid=175) |
| 新加坡 320G | 8核/16GB/320GB | 4TB | 2.5Gbps | $329.99/月 | [选购新加坡 16GB 版](https://bandwagonhost.com/aff.php?aff=79616&pid=176) |
| 新加坡 640G | 10核/32GB/640GB | 6TB | 5Gbps | $549.99/月 | [选购新加坡 32GB 版](https://bandwagonhost.com/aff.php?aff=79616&pid=177) |
| 新加坡 1280G | 12核/64GB/1280GB | 8TB | 5Gbps | $1059.99/月 | [选购新加坡顶配](https://bandwagonhost.com/aff.php?aff=79616&pid=178) |

**迪拜 ECOMMERCE 系列（中东方向，同系列含 DC9 等机房）**

| 套餐 | 配置 | 流量 | 带宽 | 价格 | 购买 |
| --- | --- | --- | --- | --- | --- |
| 迪拜 20G | 2核/1GB/20GB | 500GB | 1Gbps | $19.99/月 | [选购迪拜入门款](https://bandwagonhost.com/aff.php?aff=79616&pid=114) |
| 迪拜 40G | 3核/2GB/40GB | 1TB | 1Gbps | $32.99/月 | [选购迪拜 2GB 版](https://bandwagonhost.com/aff.php?aff=79616&pid=115) |
| 迪拜 80G | 4核/4GB/80GB | 2TB | 1Gbps | $56.99/月 | [选购迪拜 4GB 版](https://bandwagonhost.com/aff.php?aff=79616&pid=116) |
| 迪拜 160G | 6核/8GB/160GB | 3TB | 1Gbps | $86.99/月 | [选购迪拜 8GB 版](https://bandwagonhost.com/aff.php?aff=79616&pid=117) |
| 迪拜 320G | 8核/16GB/320GB | 4TB | 1Gbps | $159.99/月 | [选购迪拜 16GB 版](https://bandwagonhost.com/aff.php?aff=79616&pid=118) |
| 迪拜 640G | 10核/32GB/640GB | 5TB | 1Gbps | $289.99/月 | [选购迪拜 32GB 版](https://bandwagonhost.com/aff.php?aff=79616&pid=119) |
| 迪拜 1280G | 12核/64GB/1280GB | 6TB | 1Gbps | $549.99/月 | [选购迪拜顶配](https://bandwagonhost.com/aff.php?aff=79616&pid=120) |

如果不想一个个点，👉[进入套餐总览页对比全部系列](https://bit.ly/BandwagonHost)也可以。

## 优惠码和省钱姿势

搬瓦工的优惠码体系比较朴素：常年的主力码是 **BWHCGLUKKB**，约 **6.58% 折扣，循环优惠**，所有在售套餐 checkout 时可用，续费同样有效。社区里偶尔会冒出折扣更高的限时码（比如社区论坛合作码，出现过 6.77% 甚至更高的），但存活时间以天计，能赶上算运气，赶不上就用常驻码。

几个实际影响支出的点：

- **计费周期**：GIA-E 入门款季付 $49.99，年付 $169.99（约合 $14.17/月）。预算确定要长期用，年付比季付划算不少。
- **续费价**：按购买时的原价续费，优惠码折扣也随单保留，所以下单时用不用码，影响的是未来每一年的账单。
- **退款政策**：新账户 30 天内可申请退款，条件包括此前未退过款、账户下 VPS 数量少于 3 个、累计支付金额低于 100 美元、IP 未被封禁。想先买 GIA-E 试试 DC9 再迁移的，这个政策给了后悔余地，但注意条件别踩线。

## 几个常见问题

**DC9 的 IP 被封了怎么办？** 常规套餐可以在 KiwiVM 后台付费换 IP（约 $8.79 一次）；SLA 系列每两周可以免费换一次。CN2 GIA 线路娇贵，建站用户建议前面套一层 CDN。

**GIA-E 和 SLA 怎么选？** GIA-E 是 CN2 GIA-E 线路、机房选择多、价格低；SLA 多了 99.99% 在线率保障和免费换 IP 权益，机房固定在洛杉矶 SLA 节点，价格高一截。普通用户 GIA-E 够用，外贸等对在线率敏感的业务再考虑 SLA。

**DC9 能装什么系统？** 官方支持 AlmaLinux、RockyLinux、CentOS、Debian、Ubuntu 等主流发行版，也支持手动挂 ISO 安装，KiwiVM 面板自带快照、备份和迁移功能。

**限量版值得蹲吗？** The DC9 Plan 这种 $38/年的价格，比最便宜的常规套餐还低却能进 CN2 GIA 机房，性价比确实高。但补货无规律、售罄极快，把它当惊喜而不是计划。着急用的，直接看👉[GIA-E 套餐存量与价格](https://bandwagonhost.com/aff.php?aff=79616&pid=87)更实际。

## 写在最后

DC9 CN2 GIA 的价值很明确：三网回程全程高端线路、官方定位里网络稳定性最好的洛杉矶机房，再加上 2025 年后的 AMD EPYC + NVMe 硬件。它的门槛也明确：不能直接“买 DC9”，要么抢限量版，要么买 GIA-E 套餐后免费迁移。

给你的决策路径其实很简单——预算一年 $170 以内、想要 CN2 GIA 线路，GIA-E 入门款加迁移就是标准答案；对在线率有业务要求，加钱上 SLA；追求极致低延迟且预算充足，看香港和东京系列；只是学习练手，$49.99/年的常规 KVM 就够了，别为用不上的线路多花钱。
