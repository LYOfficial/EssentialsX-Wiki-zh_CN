# 模块

## 核心

EssentialsX 的核心是 EssentialsX 本体 jar 文件，它包含了适用于大部分服务器的很多核心内容。包括大多数命令、标志、配套元件和经济特性。 **你需要用这个 jar 当做前置让其他模块工作。**

## EssentialsX AntiBuild - 抗建造

**EssentialsX AntiBuild** 为你的服务器添加权限，这些权限可以让你更好地控制哪些玩家可以建造或在你的服务器上与方块互动。你可以为特定的用户组或用户设置他们可以控制的物品和方块，或者通过使用建造标志来允许或禁止某一整个用户组的建造权限。它也有玩家使用某些特定物品时候的警报系统功能。想要知道更多信息，可以查看 [4.1 - AntiBuild - 抗建造](https://github.com/LYOfficial/EssentialsX-Wiki-zh_CN/wiki/4.1---%E6%8A%97%E6%9E%84%E5%BB%BA) （物品 ID 在 1.13+ 版本中被删除）。

注意，抗建造不包括任何类型的区域保护，为了限制在特定区域的建造，我们建议你安装 [WorldGuard](https://dev.bukkit.org/projects/worldguard)。

*我们强烈推荐你在使用抗建造的同时使用 [LuckPerms](https://luckperms.net/download) 来让抗建造的功能充分体现。*

## EssentialsX Chat - 聊天

**EssentialsX Chat** 包括很多 EssentialsX 聊天功能。它允许你在服务器上定制聊天格式，如加前后缀、改变颜色、分组区别等。



*你需要 [Vault](https://www.spigotmc.org/resources/34315/) 和 [LuckPerms](https://luckperms.net/download) 来为玩家设置前后缀和检测组别。*

## EssentialsX GeoIP - 地理位置

**EssentialsX GeoIP - 地址** 是一个基于地理数据库的功能，它可以查找玩家的 IP 并显示属地。管理员可以在玩家登录时或者使用 `/whois` 指令来查看。

## EssentialsX Protect - 保护

**EssentialsX Protect** 允许你为你的世界控制一些简单的功能，比如放置苦力怕破坏建筑、防止火焰蔓延和禁止某种怪物生成。

注意，保护功能不包括任何类型的区域保护，为了限制在特定区域的建造，我们建议你安装 [WorldGuard](https://dev.bukkit.org/projects/worldguard)。

## EssentialsX Spawn - 出生

**EssentialsX Spawn** 让你可以控制玩家出生点，玩家在第一次加入服务器或死亡后都会在这里出生。你可以使用游戏内的 `/setspawn` 指令来为为你服务器中的每个人或某个用户组设置特定的出生点。

## EssentialsX Discord

**EssentialsX Discord** 在 Discord and Minecraft 之间提供了一个简单、轻量、容易使用而且无膨胀的桥梁。

EssentialsX Discord 提供了你用来连接 Discord 所需要的 *必要的* 功能，例如：

* MC 聊天 -> Discord 频道
* Discord 频道 -> MC 聊天
* 基础 MC -> Discord 事件监听 (加入/离开/死亡/沉默)
* MC 控制台 -> Discord 转播
* Discord 斜杠命令：
    * /execute - 执行来自 Discord 的控制台命令
    * /msg - 向 MC 玩家发送来自 Discord 的消息
    * /list - 列出现在在线的 MC 玩家
    * 还有更多...


想要知道更多有关搭建 EssentialsX Discord 的信息，可以查看 [[Discord-Tutorial|the tutorial]]!

## EssentialsX XMPP

**EssentialsX XMPP** 是 Jabber/XMPP 聊天网络和服务器之间的桥梁。通过这个玩意，玩家可以在 XMPP 网络和你的服务器之间交流。这也允许服务器管理员远程监控服务器的控制台和服务器错误。想要知道更多信息，可以查看 [4.4 - XMPP](https://github.com/LYOfficial/EssentialsX-Wiki-zh_CN/wiki/4.4---XMPP)。


*如果你不知道 XMPP 是个啥，那你不需要这个！*

<!--
**EssentialsX Link** (coming soon) acts as a bridge between chat services such as Discord and your Minecraft server. This allows players to chat between Discord and your server, as well as letting players link their Discord and Minecraft accounts for special ranks.

(also hi thanks for looking at the raw page o/)

**EssentialsX Potato** integrates your Minecraft server with the well-known culinary open source project [Potato](https://github.com/drtshock/Potato). This ensures you always have the finest high-quality potatos ready to go!
-->