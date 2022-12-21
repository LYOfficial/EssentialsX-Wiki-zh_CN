# 安装 EssentialsX

首先，确保你在运行的我的世界服务端是一个受支持的端。我们建议使用 [Paper](https://papermc.io) ，尤其是 1.13+ 的服务器，因为它比 Spigot 有更多的性能上的改进。

想要下载  EssentialsX ？你可以从 [SpigotMC](https://www.spigotmc.org/resources/essentialsx.9089/) 下载稳定版本，或者从   [下载页面](https://essentialsx.net/downloads.html) 下载测试版（有最新特性，当然，或许还有 Bug ）。

EssentialsX 被分成了几个不同的独立插件。EssentialsX 本体 `EssentialsX` jar 才是必须的，它包含了大部分服务器所需要的核心功能。其他模块是可以选择的，详细请阅读 [1.3 - 模块故障](https://github.com/LYOfficial/EssentialsX-Wiki-zh_CN/wiki/1.3---%E6%A8%A1%E5%9D%97%E6%95%85%E9%9A%9C) 查看更多模块及它们的用途。

一旦你决定了你要用哪些 EssentialsX 模块，复制所需的 `.jar` 文件放到 `plugins/` 目录中（如果你是从 SpigotMC 下载的，你首先需要解压下载的压缩包）。

如果你还没有权限插件，我们回推荐你安装 [LuckPerms](https://luckperms.net) 来控制玩家的排名、权限、前后缀。虽然这是可以选择的，但我们推荐你这么做！

当然，你还要安装 [Vault](https://www.spigotmc.org/resources/vault.34315/) 来允许 EssentialsX 与权限插件交换信息；如果没有 Vault ，前缀、后缀和有关群组的功能将无法工作。

一旦你安装了所有你需要的插件，重启你的服务器。EssentialsX 将在启动时创建一个配置文件（如果有需要的话，还会同时升级旧的 Essentials 数据）。