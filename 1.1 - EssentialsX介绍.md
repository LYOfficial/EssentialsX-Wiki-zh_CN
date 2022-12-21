# EssentialsX 介绍

EssentialsX 是一个基于 Spigot 服务端的基础插件，为从大到小的服务器提供核心功能。这些功能包括：
* **玩家可以自由设置家**
* 服务器**传送**或给玩家提供**物品套组**，可以设置跨世界或单独世界。
* 玩家与玩家间的**私有消息，传送，发送传送请求**
* 玩家自定义**昵称**
* 很多的管理员工具包括**踢出服务器，临时禁止登陆服务器、禁言与监禁**
* 内建经济系统，包括**木牌商店、付费执行命令和完全的 Vault 支持**

此外，EssentialsX 的选择模块提供了更多综合的功能如聊天、世界保护、GeoIP查找还有更多……请前往 [模块故障](https://github.com/LYOfficial/EssentialsX-Wiki-zh_CN/wiki/1.3---%E6%A8%A1%E5%9D%97%E6%95%85%E9%9A%9C) 部分阅读更多内容。

## 页面

* [3.2 - BannerMeta](https://github.com/LYOfficial/EssentialsX-Wiki-zh_CN/wiki/3.2---BannerMeta)
* [2.1 - 命令冷却](https://github.com/LYOfficial/EssentialsX-Wiki-zh_CN/wiki/2.1---%E5%91%BD%E4%BB%A4%E5%86%B7%E5%8D%B4)
* [2.2 - 颜色权限](https://github.com/LYOfficial/EssentialsX-Wiki-zh_CN/wiki/2.2---%E9%A2%9C%E8%89%B2%E6%9D%83%E9%99%90)
* [2.3 - 自定义&列表](https://github.com/LYOfficial/EssentialsX-Wiki-zh_CN/wiki/2.3---%E8%87%AA%E5%AE%9A%E4%B9%89&%E5%88%97%E8%A1%A8)

**注：** 当你更新EssentialX时，你需要更新*所有的*模块以避免插件与附属插件不兼容的问题。事实上，你有时候会想更新你的config文件 —— 最新的文件在 [这里](https://github.com/EssentialsX/Essentials/blob/2.x/Essentials/src/main/resources/config.yml) 。

## 从 Essentials 2 更新

EssentialsX 是原先 [Essentials 项目](https://github.com/essentials/Essentials) 的分支，Essentials 已于2014年停止更新。EssentialsX 相比 Essentials 和 Spigot 上的 Essentials 分支添加了一些新特性。查看 [EssentialsX 更新日志](https://github.com/EssentialsX/Essentials/releases) 获得更多信息。 

若要从 Essentials 2.14.x 或更早版本升级，先关闭你的服务端，更换你的 Essentials Jar 为相应的EssentialsX Jar。我们建议你重命名你的 `config.yml` 文件来通过 EssentialsX 添加新的设置, 同时，完整备份一次你的 `plugins/Essentials/` 文件夹. 重启服务器，EssentialsX 会创建一个新的 `config.yml` 文件并将旧的用户数据转换成新格式。 