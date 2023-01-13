# 关键词

EssentialsX 提供了许多标准关键字（占位符），可用于自定义插件中多个位置的文本。

| 关键词                   | 用法                                                         |
| ----------------------- | ------------------------------------------------------------ |
| {PLAYER}, {DISPLAYNAME} | 玩家的显示名称。                                               |
| {USERNAME}              | 玩家的用户名。                                                 |
| {NICKNAME}              | 玩家的 EssentialsX 昵称。 如果玩家没有昵称，则使用用户名。       |
| {PREFIX}                | 玩家的前缀，由权限插件通过 Vault 提供。                         |
| {SUFFIX}                | 玩家的后缀，由权限插件通过 Vault 提供。                         |
| {GROUP}                 | 玩家的主要组，由权限插件通过 Vault 提供。                       |
| {BALANCE}               | 玩家的余额，以货币形式显示。                                   |
| {MAILS}                 | 玩家拥有的邮件数量。                                           |
| {PLAYTIME}              | 玩家的游戏时间，格式为持续时间。                                |
| {WORLD}, {WORLDNAME}    | 玩家当前世界的完整名称。                                       |
| {WORLDTIME12}           | 玩家当前世界的时间，采用 AM/PM 格式。                          |
| {WORLDTIME24}           | 玩家当前世界的时间，采用 24 小时格式。                         |
| {WORLDDATE}             | 玩家所在世界的日期.                                          |
| {IP}                    | 玩家的IP地址。                                               |
| {ADDRESS}               | 玩家的socket地址。                                           |
| {ONLINE}                | 在线玩家数量。 不计算隐藏的玩家（例如消失的玩家）。             |
| {UNIQUE}                | 加入服务器的特殊玩家数量。                                    |
| {WORLDS}                | 服务器上的世界列表。                                          |
| {PLAYERLIST}            | 当前在线的玩家列表。 未列出隐藏的玩家（例如消失的玩家）。        |
| {TIME}                  | 当前运行服务器的主机的时间。                                   |
| {DATE}                  | 当前运行服务器的主机的日期。                                   |
| {TPS}                   | 服务器当前的 TPS。                                            |
| {UPTIME}                | 服务器启动后经过的时间，格式为持续时间。                        |
| {PLUGINS}               | 服务器上的插件列表。                                          |
| {VERSION}               | 服务器的版本字符串。                                          |

### 我在哪里可以使用这些关键字？

这些关键字可与以下 EssentialsX 功能一起使用：

- 自定义文本文件：`book.txt`、`custom.txt`、`info.txt`、`motd.txt`、`rules.txt`
- 套件：在 `kits.yml` 文件中。
- EssentialsX Spawn 的新手公告：配置中的“newbies.announce-format”。
- `/broadcastworld` 命令。

