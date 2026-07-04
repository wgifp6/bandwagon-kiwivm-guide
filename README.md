# 登录搬瓦工 VPS 面板完整教程：KiwiVM 怎么进？找不到入口、Session Expired、忘记密码怎么解决？（附套餐对比与购买指南）

买了搬瓦工 VPS 之后，第一件事就是登录后台面板管理机器。但很多人卡在这里——不知道 KiwiVM 是什么，或者点开链接满屏英文不知所措，再不然就是报 Session Expired 怎么试都进不去。

这篇文章把登录搬瓦工 VPS 面板的完整流程说清楚，包括两种登录方式、常见报错处理、密码体系的区别，以及面板里能干什么。直接用，不绕弯。

---

## 搬瓦工 VPS 面板是什么？先搞清楚这件事

**KiwiVM Control Panel** 是搬瓦工官方自研的 VPS 管理后台，地址是 `kiwivm.64clouds.com`。登录进去之后，你可以在这里做所有跟服务器"硬件层面"有关的事：开关机、重启、重装系统、重置 root 密码、查看流量用量、创建快照、迁移机房等。

它和你在服务器上装的宝塔面板、WordPress 后台不是同一回事——KiwiVM 管的是"机器本身"，宝塔管的是"机器上装了什么软件"。刚拿到 VPS 的时候，先要通过 KiwiVM 完成初始设置，比如选系统、获取 root 密码，之后才能 SSH 上去操作。

---

## 登录搬瓦工 VPS 面板的两种方式

### 方式一：从账户后台直接跳转（最推荐）

这是日常用得最多的方式，不需要记额外密码，操作流程如下：

1. 打开搬瓦工官网，点右上角 **Client Area** 登录账户
2. 登录成功后，顶部菜单点 **Services → My Services**
3. 在套餐列表里找到你要管理的那台 VPS，点进去
4. 点击左侧或页面里的 **KiwiVM Control Panel** 按钮
5. 系统会自动跳转并登录 KiwiVM，不需要输入任何密码

这个流程的好处是完全自动的，账户里有几台机器就能分别进不同的 KiwiVM，不会搞混。

👉 [前往搬瓦工官网登录账户，进入 KiwiVM 面板](https://bit.ly/BanWaGon)

---

### 方式二：直接访问 KiwiVM 网址登录

这个方式适合两种情况：一是你把 VPS 租给朋友用，不想给他整个账户的权限；二是你想不经过官网后台，直接开 KiwiVM 管理。

登录地址：`https://kiwivm.64clouds.com`

打开之后，你会看到一个登录框，需要填两项：

- **VPS IP address**：就是你这台服务器的 IP 地址
- **KiwiVM password**：注意，这不是你的账户密码，也不是 SSH 密码，是 KiwiVM 面板独立设置的密码

KiwiVM 密码默认是没有的，需要你自己进 KiwiVM 之后，在左侧菜单找 **KiwiVM password modification**，设一个强度够高的密码（系统会检测密码强度，太简单的不让过）。设好之后，以后就能直接在 `kiwivm.64clouds.com` 这里用 IP + 密码登录，不用走官网后台了。

---

## 三种密码的区别，搞混了就麻烦

搬瓦工有三套不同的密码体系，很多新手分不清楚，在这里一次说明白：

| 密码类型 | 用途 | 在哪里改 |
|------|------|------|
| 账户密码（Client Area 密码）| 登录搬瓦工官网 | 官网个人设置 |
| Root 密码（SSH 密码）| SSH 登录 VPS 服务器 | KiwiVM → Root password modification |
| KiwiVM 密码 | 直接登录 KiwiVM 面板 | KiwiVM → KiwiVM password modification |

登录 VPS 面板用的是第三个，KiwiVM 独立密码。忘记了 SSH 密码不影响登录 KiwiVM；忘了账户密码，可以用官网找回；而 KiwiVM 密码如果忘了，在 `kiwivm.64clouds.com` 登录界面下方有一个 **Reset KiwiVM password** 按钮，输入 IP 地址之后，搬瓦工会把重置流程发到你的账户邮箱。

---

## Session Expired 登录不进去怎么办

这是搬瓦工 KiwiVM 面板更新安全机制之后比较常见的问题，很多人老是遇到。

报错提示一般是这样的：

> Your session has timed out due to inactivity. Please log in again to continue.

出现这个的原因是 KiwiVM 加强了 Cookie 和会话处理，旧的浏览器 Cookie 会触发冲突。解决方法有两个，选一个用就行：

**方法一（临时解决）**：开一个新的无痕浏览器窗口，重新从官网后台点击 KiwiVM Control Panel 进入。无痕模式没有旧 Cookie，不会触发冲突。

**方法二（彻底解决）**：手动清除浏览器里 `kiwivm.64clouds.com` 和 `64clouds.com` 这两个域名下的 Cookie。清完之后正常打开，重新登录。

我自己用下来，遇到这个问题换无痕窗口基本就好了，不用每次都清 Cookie。

---

## 进了 KiwiVM 之后能干什么

登录搬瓦工 VPS 面板之后，左侧菜单里有很多功能。常用的几个：

- **Main controls**：查看 VPS 状态（Running / Stopped），执行重启、开关机操作。机器卡死的时候，在这里 Stop 再 Start，比 SSH 里执行 reboot 更彻底
- **Install new OS**：一键重装系统。支持 Ubuntu、Debian、CentOS、Rocky Linux 等主流发行版，包括最新的 Ubuntu 26.04
- **Root password modification**：重置 VPS 的 root 密码，SSH 密码忘了就用这个
- **Migrate to another DC**：一键切换机房。部分套餐支持免费切换十几个机房，CN2 GIA-E 套餐可选机房特别多
- **Two-factor authentication**：给 KiwiVM 面板设置两步验证，账户安全性会好很多，推荐开启
- **Snapshots / Backups**：快照和自动备份，搬瓦工提供免费的自动备份功能，快照也是免费的，最多保留两个，做系统迁移或者高风险操作前记得先建快照

---

## 套餐对比：买之前先看清楚选哪档

搬瓦工目前主要在售的套餐分几个系列，面向不同预算和需求。下面是常规套餐对比：

| 套餐系列 | 线路类型 | 内存 / 流量 | 参考价格 | 适合谁 | 购买 |
|--------|--------|----------|--------|------|------|
| CN2 套餐（KVM）| CN2 GT，8 个机房可选 | 1GB / 1TB | 约 $49.99/年 | 预算有限、入门用 |  [查看此套餐](https://bit.ly/BanWaGon) |
| CN2 GIA-E 套餐 | CN2 GIA，12+ 机房（含 DC6、DC9、软银、荷兰）| 1GB / 1TB | 约 $49.99/季 | 国内使用、追求速度 |  [查看此套餐](https://bit.ly/BanWaGon) |
| 香港 CN2 GIA 套餐 | 三网 CN2 GIA，低延迟 | 2GB / 500GB 起 | 约 $89.99/月 | 极低延迟需求、预算充足 |  [查看此套餐](https://bit.ly/BanWaGon) |
| 日本大阪 CN2 GIA | CN2 GIA，亚太方向 | 按具体配置 | 高于 CN2 GIA-E | 日本方向需求 |  [查看此套餐](https://bit.ly/BanWaGon) |

说句实话，如果不知道选哪个，CN2 GIA-E 套餐是大多数国内用户最常选的：线路质量不错，机房多，可以直接在 KiwiVM 里面免费切换，买了之后试试不同机房，找到最适合自己网络环境的那个就行。支持支付宝付款，不需要信用卡。

👉 [对比搬瓦工所有套餐，找最适合你的方案](https://bit.ly/BanWaGon)

---

## 几个使用过程中容易踩的坑

**KiwiVM 面板打不开、一直转圈**：先换个网络环境试试，因为搬瓦工官网主域名国内有时 DNS 解析会有问题。搬瓦工提供了多个镜像地址（在官网可查），用镜像地址进后台，KiwiVM 跳转一般不受影响。

**VPS 显示 Active 但 SSH 连不上**：进 KiwiVM 看 Status 是不是 Running。是 Stopped 的话点 Start；是 Running 的话可能是端口问题或者 IP 被封了，用 KiwiVM 面板里的 Root shell – interactive 进去排查。

**超流量被暂停（Suspended）**：每月流量重置周期到了会自动恢复。如果不是流量问题，可以在 KiwiVM 面板里找临时恢复功能，或者提交工单找官方客服。

**开机后等两分钟再 SSH**：每次在 KiwiVM 里执行开机或重启之后，给系统留个一两分钟启动时间，马上连有时会报连接拒绝。

---

## 常见问题

**Q：KiwiVM 面板的密码是什么？和账户密码一样吗？**

不一样。KiwiVM 面板有独立的密码，默认没有设置，需要你进入 KiwiVM 后台在 KiwiVM password modification 里自己设一个。如果你一直用方式一（从官网后台跳转），实际上不需要单独设这个密码。

**Q：搬瓦工 VPS 支持重装系统吗？重装会丢数据吗？**

支持，在 KiwiVM 的 Install new OS 里操作，支持几十种系统镜像。重装会清除现有数据，操作前建议先在 Snapshots 里建一个快照备份。

**Q：登录搬瓦工 VPS 面板需要开代理吗？**

KiwiVM 面板地址 `kiwivm.64clouds.com` 一般国内可以直接访问。搬瓦工官网主域名（bandwagonhost.com）在国内有时 DNS 解析有问题，可以用官方提供的镜像地址（如 bwh81.net）进账户后台，之后跳转 KiwiVM 不受影响。

**Q：套餐买了之后可以退款吗？**

搬瓦工支持 30 天内退款，在购买后 30 天内不满意可以申请全额退。超过 30 天的就不支持退款了。

**Q：一台机器可以同时被多人管理吗？**

可以。给这台 VPS 设一个独立的 KiwiVM 密码，把 IP 和这个密码告诉对方，对方可以直接用 `kiwivm.64clouds.com` 登录管理，不需要你的账户密码。

---

还没有搬瓦工 VPS 的话，直接走下面的链接进官网，套餐选择、价格和当前优惠都在里面：

👉 [前往搬瓦工官网，查看最新套餐与优惠](https://bit.ly/BanWaGon)
