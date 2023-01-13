# 改进 EssentialsX

EssentialsX 是原 Essentials 插件的续作，而原插件已经在 2014 年停止了更新。EssentialsX 不仅支持经典的 Essentials 所有同样的功能，而且相对于 Essentials，EssentialsX 有了很大改进。

这个页面的目的在于详细介绍 EssentialsX 新增的许多改进。想要知道更多有关 EssentialsX 发行版的更新详细？请参考阅读：[发行版变更日志](https://github.com/EssentialsX/Essentials/releases).

## 亮点
* 积极维护和更新，适配了新版本的 Minecraft 和 Spigot（从 1.8.8 到最新的版本）。
  - 支持了新版本的 Minecraft 内容，包括新的物品、附魔、生物和树木。
  - 更新了 [签名教程](https://wiki.mc-ess.net/wiki/Sign_Tutorial) ，支持在所有 Minecraft 版本运行。
  - 支持所有受支持的 Minecraft 版本上的生物刷怪笼。
    * 在 1.8-1.12版本, 你可以使用形如 `/i mob_spawner:51`的刷怪笼标志和命令, 刷怪笼将在放置时刷新。
    * 在 1.13+版本, 你可以使用 `/i blazespawner` 来使用刷怪笼生成.
* 包括基础 EssentialsX 中的新功能，例如套件的 [[BannerMeta|Banner Metadata]]、[[Command-Cooldowns|Command Cooldowns]] 和许多其他新配置选项。
* 全新的 [[Discord-Tutorial|Discord bridge]] 插件与所有 Essentials 插件的最新版本（甚至是 XMPP！）
* 包含适用于所有 Minecraft 版本（包括 1.13 及更高版本）的新物品别名。
* 支持在 1.9-1.12 版本中给予具有实体ID值的刷怪蛋和具有伤害值的药水。
* 使用 UUID 支持的 Vault 进行权限组和前缀/后缀查找，以及重写过的新 Vault适配器，使其更加稳健。
  - Spigot-Essentials 实现了 zPermissions 的 UUID 查找，但不是其他权限插件。
  - EssentialsX 优先考虑 Vault，因此使用 Vault 处理程序的所有查询都应该更快，因为它们不需要 名称-到-UUID 查找。

### 其他的一点小补充
* `/tppos` 现在可以选择接受一个世界名。
* 添加了 `/msgtoggle` 命令以允许玩家忽略所有私人消息。
* 批量销售和手动销售的单独权限：分别为 `essentials.sell.hand` 和 `essentials.sell.bulk`
* 添加了免除 SocialSpy 的权限：`essentials.chat.spy.exempt`
* 为奶桶 `复活节彩蛋` 添加配置选项，这（真的不应该，但还是做了）允许玩家干扰其他人的马：`milk-bucket-easter-egg`
* 为加入服务器时的`Set fly mode enabled...`消息添加配置选项：`send-fly-enable-on-join`

## 新功能

### 设置游戏模式的权限
您现在可以在 `/gamemode` 中限制玩家可以切换到哪些游戏模式。 例如，您可能想让玩家输入`/gma`和`/gms`，而不是`/gmc`或`/gmsp`。 您可以授予您希望他们能够更改的游戏模式：
* `essentials.gamemode.creative`
* `essentials.gamemode.survival`
* `essentials.gamemode.adventure`
* `essentials.gamemode.spectator`
* `essentials.gamemode.all`

**注意**：仍然需要基本的 `essentials.gamemode` 权限才能让玩家使用 `/gamemode` 命令及其别名。

### 套件改进
套件已从config主配置移至 kits.yml，现在可以在游戏中创建并自动添加到您的服务器，无需手动编辑和重新加载配置。

此外，带有全套 [[EssentialsX placeholders|Keywords]] 的套件现在支持命令 - 只需在您的kit.yml文件中添加一行，如下所示：

```yaml
kits:
  mykit:
    delay: 1000
    items:
      - stone 1
      - /give {USERNAME} apple 1
```

EssentialsX 还添加了新的命令来帮助管理套件：

#### `/createkit`
**命令**: `/createkit <kitname> <delay>`  
**权限**: `essentials.createkit`  
如果 `pastebin-createkit` 在 `config.yml` 中设置为 `false`，则从您的库存中创建一个套件并将其放入 `kits.yml` 文件中。
或者，如果 `pastebin-createkit` 设置为 true，则根据您的库存创建一个套件并粘贴一个在线链接，其中包含要手动添加到您的 `kits.yml` 中的行。

![createkit](https://i.imgur.com/nXMlNGP.png)

#### `/showkit`
**命令**: `/showkit <kitname>`  
**权限**: `essentials.showkit`  
直接从配置文件中显示套件内容列表。

![showkit](https://i.imgur.com/d4Ff8vN.png)

### 强制禁用传送安全

Upstream Essentials 的`teleport-safety`选项只有两个值：
* 将位置转换为安全的传送点（导致大量漏洞）； 或者
* 完全拒绝传送。

EssentialsX 添加了一个`force-disable-teleport-safety`选项（默认为 false）。 当与 `teleport-safety: true` 结合使用时，这会禁止转换到安全位置并将用户传送到他们的精确位置。

**注意：** 如果要禁用跨世界传送安全，请切换到 Paper 并在 `paper.yml` 中将 `disable-teleportation-suffocation-check` 设置为 true。

### 刷怪笼放置修复
如果来自 EssentialsX 命令/套件的刷怪笼在放置后变成了猪刷怪笼，您可以将 `essentials.spawnerconvert.*` 分配给您的默认组以自动将它们转换为正确的生物类型。

### 受控的私人消息

新的配置选项`last-message-reply-recipient`允许您更改`/reply`的工作方式。 如果设置为 `true`，您的回复收件人将是**最后给您发消息的人**，*不是* **最后给您发消息的人**。 如果您没有回复收件人，最后给您发消息的人将成为您的回复收件人。

这是新的最后一条消息回复收件人功能的 格式化场景：

> **JRoy: `/msg mdcfe Hi`**  
> _JRoy -> mdcfe: Hi_  
> **mdcfe: `/r Hi`**  
> _mdcfe -> JRoy: Hi_  
> **broccolai: `/msg JRoy Hi`**  
> _broccolai -> JRoy: Hi_  
> **JRoy: `/r Hi back to you, mdcfe!`**  
> _JRoy -> mdcfe: Hi back to you, mdcfe!_  

如果启用此功能，EssentialsX 还将使用`last-message-reply-recipient-timeout`设置。 此设置允许您控制玩家回复收件人重置前的秒数。 这段时间过后，当玩家收到消息时，他们的回复将开始发送给最后一个向他们发送消息的人。

### `/seen` 通过 UUID

您现在可以使用玩家的用户名或 UUID 检查最后一次看到玩家的时间。 例如，键入`/seen SupaHam`和`/seen 5552e21d-de79-40bc-89da-62ee63244fb2`现在都是检查玩家最后一次出现时间的有效方法。

### 每个世界的 `/time` 设置权限

在经典 Essentials 中，拥有`essentials.time`和`essentials.time.set`权限的玩家可以在任何世界中设置时间，即使他们没有在权限插件中设置该世界中的权限。 如果在配置中将 `world-time-permissions` 设置为 `true`，用户将需要特定权限才能设置每个世界的时间 - 请参见下表。 默认情况下禁用此功能。

#### 权限
|        权限                      | 描述 |
|----------------------------------|------|
| essentials.time.world.`<world>` | 允许用户在 `<world>` 中设置时间。 `<world>` 是用 _ 替换空格的世界名称。 . 如My World变成了my_world. |
| essentials.time.world.all       | 允许用户设置所有世界的时间。 这将覆盖 `essentials.time.world.<world>`. |

### AFK玩家列表名称

此版本引入了`afk-list-name`配置属性，用于控制 AFK 玩家在玩家列表中的显示方式。

该属性有两个占位符：
- `{USERNAME}`: 玩家的名字
- `{PLAYER}`：玩家的显示名称。

Here's an example of "[AFK] _SupaHam_":
```yaml
afk-list-name: '&7[AFK] &o{USERNAME}'
```

### 昵称颜色权限

EssentialsX 添加了昵称颜色和格式的新权限，与 Mojang 在 Minecraft 聊天组件系统中使用的名称相匹配。 这些权限还涵盖聊天消息（如果您安装了 EssentialsX Chat）等。 您可以在 [[Color-Permissions|here]] 查看这些新权限的列表。

您现在还可以使用 `essentials.nick.changecolors` 权限来限制玩家的昵称更改。 当玩家拥有此权限时，他们只能更改昵称的颜色和格式，而不能更改文字内容。 例如，如果玩家 `SupaHam` 拥有 `essentials.nick.changecolours` 和 `essentials.nick.color` 权限，他们可以将昵称更改为 `&5SupaHam`，但不能更改为 `&5TheSupaHam`，因为文本内容没有匹配他们的用户名。

### 加入时传送到出生点

**此功能已添加到 [build 361](https://ci.ender.zone/job/EssentialsX) ([b673630](https://github.com/drtshock/Essentials/commit/b673630)).**

在#345 中请求。 管理员现在可以使用 `config.yml` 文件中的 `spawn-on-join` 选项指定加入的玩家是否被传送到出生点。

`spawn-on-join` 接受以下几种类型的值：

1. `true`/`"*"` - **所有玩家** 加入时会被传送到重生点。
2. `false` - **没有玩家** 加入时会被传送到重生点。
3. String - 该值被视为组名。 如果玩家在组中，他们将在加入时被传送到重生点。
4. List of Strings - 该值被视为组名列表。 如果玩家在*任何*这些组中，他们将在加入时被传送到重生点。

当 `spawn-on-join` 为 `true` 时，所有玩家将被传送到他们的团队重生点。 如果没有设置组生成点，将使用使用 `/setspawn` 设置的默认重生点。

若没有其他插件干扰的情况下，如果管理员希望在 `spawn-on-join` 为 `true` 时免除某些玩家使用此功能，他们可以授予他们 `essentials.spawn-on-join.exempt` 权限，他们将从他们离开的地方登录。

### AFK 信息

_Requested in [#590](/drtshock/Essentials/issues/590); PR in [#664](/drtshock/Essentials/pull/664)._

玩家可以在使用`/afk`命令时设置他们的AFK消息来通知其他人了解自己的情况。 当玩家向 AFK 玩家发送带有 `/msg` 的消息时，他们将看到 AFK 玩家的消息。

默认情况下，玩家设置挂机状态时，消息不会全服广播。 但是，这可以在 [[Locale|locale file]] 中通过将 `{1}` 添加到 `userIsAwayWithMessage` 消息中来更改，其中 `{1}` 将被玩家的 AFK 消息替换。

要设置您的 AFK 消息，只需键入 `/afk <message...>`。 例如：`/afk 我在挂机`。

为了使用此功能，玩家必须拥有`essentials.afk.message`权限。 但是，如果玩家被禁言，他们将无法提供消息，因为它可以用来利用他们的惩罚。

### Pay toggle
_Requested in [#413](/drtshock/Essentials/issues/413); added in [2493c65](https://github.com/drtshock/Essentials/commit/2493c65)._

玩家可以通过`/paytoggle`命令禁用任何和所有支付。 这可用于打击使用`/pay`作为向其他玩家发送垃圾邮件的手段的玩家，例如您服务器上的知名人士。

`paytoggle` 还有以下别名: `epaytoggle`, `payoff`, `epayoff`, `payon`, `epayon`

`payoff` 将始终禁用支付以防止错误。 相反，`payon` 将始终启用付款。

### `/pay` 和 `/clearinventory` 的命令确认
_Requested in [#1032](/drtshock/Essentials/issues/1032); added in [5f83766](https://github.com/drtshock/Essentials/commit/5f83766)._

您现在可以使用配置的`default-enabled-confirm-commands`部分指定是否提示玩家在执行`/clearinventory`和`/pay`命令之前确认它们。

此外，玩家可以分别使用 `/clearconfirm` 和 `/payconfirm` 为自己打开或关闭确认。

### 传送到精确坐标

此功能已在 ([0a563b9](https://github.com/drtshock/Essentials/commit/0a563b9)) 实现.

此功能引入了`teleport-to-center`配置功能。 当设置为`true`（默认）时，所有传送都以方块为中心； 从技术上讲，将 x 和 z 坐标小数设置为 .5 和 .5。 当`teleport-to-center`设置为`false`时，所有传送都会执行到给定的确切位置。

### 邮件聊天格式
_Requested in [#1560](/drtshock/Essentials/issues/1560); added in [665229b](https://github.com/drtshock/Essentials/commit/665229b)._

此功能引入了使用 `&` 格式化代码格式化 `/mail` 消息的能力 - [[Color-Permissions|click here]] 以获取更多信息。

### 头盔槽位
_Added in [7958cd0](https://github.com/EssentialsX/Essentials/commit/7958cd0b880205edaeaf34420bafde8d5cc1f7ed)._

如果在 `config.yml` 中启用了 `allow-direct-hat`，那么拥有 `essentials.hat` 权限的玩家可以点击他们的头盔槽来将任何方块放在他们的头上，而不仅仅是头盔。
