# EssentialsX Discord 安装指南

EssentialsX Discord 是一个模块，它带来了一个简单、轻量级、易于使用且无膨胀的
Discord 和 Minecraft 之间的桥梁。

EssentialsX Discord 提供您希望从 Discord 桥接器获得的*essential*功能，例如：
* MC 聊天 -> Discord 频道
* Discord 频道 -> MC 聊天
* 基本 MC -> Discord 事件监控（加入/离开/死亡/静音）
* MC 控制台 -> Discord 中继
* Discord 斜杠命令
     * /execute - 从 Discord 执行控制台命令
     * /msg - 来自 Discord 的消息 Minecraft 玩家
     * /list - 列出当前在 Minecraft 上在线的玩家
* & 更多……

---

## 目录
> * [最初设定](#initial-setup)
> * [控制台中继](#console-relay)
> * [配置消息](#configuring-messages)
> * [在 Minecraft 中接收 Discord 消息](#receive-discord-messages-in-minecraft)
> * [Discord 命令](#discord-commands)
> * [杂项权限](#misc-permissions)
> * [开发者 API](#developer-api)

---

## 最初设定

0. 在启动服务器之前，您必须执行几个步骤。 首先，您必须创建一个新的
    [discord.com/developers/applications](https://discord.com/developers/applications/) 上的 Discord 机器人。

1. 进入该页面后，单击右上角的"新建应用程序"按钮，为您的机器人命名，然后
    然后单击"创建"。
> ![创建应用程序](./images/discord/create-app.gif)
> `新应用` -> 为应用程序命名 -> `创建`

2. 创建应用程序后，您将被引导至其概览。 从这个界面，你
    需要复制您的"客户端 ID"/"应用程序 ID"并将其保存以供后续步骤使用。 复制你的
    Client ID，点击最左上角的蓝色"复制"按钮。 确保将其保存以供后续步骤使用。
> ![复制客户端 ID](./images/discord/copy-client-id.gif)
> `复制` -> 粘贴到记事本中以备后用

3. 或者，您可以为您的应用程序设置一个图标，因为它也将是机器人的图标。
> ![头像](./images/discord/avatar.png)

4. 下一步实际上是为您的应用程序创建机器人用户。 从概览界面，
    这是通过转到左侧的"Bot"选项卡，然后单击右侧的"Add Bot"来完成的，
    最后点击"Yes,do it！"。
> ![创建机器人](./images/discord/create-bot.gif)
> `Bot` -> `Add Bot` -> `Yes, do it!`

5. 在此屏幕上后，您需要取消选中"公共机器人"设置，然后单击"保存更改"，
    所以其他人无法将您的机器人添加到不属于您自己的服务器。
> ![禁用公共机器人](./images/discord/disable-public.gif)
> 取消选中 `Public Bot` -> `Save Changes`

6. 最后，您需要复制机器人的令牌并将其保存以供后续步骤使用。 要复制您的机器人令牌，
    点击你的机器人图标右边的蓝色"复制"按钮。 确保将其保存以供后续步骤使用。
> ![复制令牌](./images/discord/copy-token.gif)
> `复制` -> 粘贴到记事本以供后续步骤使用

7. 接下来是将您的机器人添加到您的 Discord 服务器。 首先，转到 [essentialsx.net/discord.html](https://essentialsx.net/discord.html)
    并将您从第 2 步复制的客户 ID 粘贴到该页面的文本框中。 完成后，单击
    文本框旁边的"授权"按钮。 这会将您重定向到 Discord 的授权网站
    选择要将机器人添加到哪个服务器。
    高级用户注意事项：**请使用上面的 `essentialsx.net` 链接，即使您已经知道如何操作
    邀请机器人。** EssentialsX Discord 需要的不仅仅是 `bot` 范围才能工作。
> ![OAuth 链接生成器](./images/discord/auth.gif)
> 粘贴客户端 ID -> `Authorize`

8. 进入 Discord 授权网站后，从"选择服务器"下拉列表中选择服务器
    您要将机器人添加到其中。 接着点击"授权"按钮。 系统可能会提示您确认
    你不是机器人，请像对待任何其他验证码一样继续。
> ![授权](./images/discord/add-bot.gif)
> 选择服务器 -> `Authorize`"

9. 对于接下来的几个步骤，您需要在 Discord 中做一些事情，所以启动您的
    Discord 桌面/Web 客户端。

10. 进入 Discord 客户端后，您需要启用开发者模式。 通过进入
     设置，然后转到"高级"选项卡并选中底部的"开发人员模式"
     页。 选中"开发者模式"后，单击右上角的"X"退出设置。
> ![开发者模式](./images/discord/dev-mode.gif)
> `User Settings` -> `Advanced` -> 检查 `Developer Mode` -> 退出设置

11. 接下来是复制一些 ID。 首先，您需要复制服务器（又名公会）ID。 通过找到您添加机器人的服务器，右键单击其图标，然后单击"复制 ID"来执行此操作。 复制后，请务必保存以供后续步骤使用。
> ![公会 ID](./images/discord/guild-id.gif)
> 右键单击服务器 -> `复制 ID` -> 粘贴到记事本中以供后续步骤使用

12. 您需要复制的另一个 ID 是您希望成为主频道的频道 ID。
     换句话说，这将是默认接收玩家聊天/加入/离开/死亡消息的频道
     消息以及静音/踢出。 要了解如何进一步配置消息类型，请参阅 [配置消息](#configuring-messages)。
> ![主频道 ID](./images/discord/prim-id.gif)
> 右键单击您的"主要"频道 -> `复制 ID` -> 粘贴到记事本以供后续步骤使用

13. 您已成功复制了基本设置所需的所有必要 ID。 接下来是为 EssentialsX Discord 生成默认配置，这样您就可以开始设置它了！ 通过将
     EssentialsX Discord jar（如果您还没有，可以在 [此处](https://essentialsx.net/downloads.html) 下载）在您的插件文件夹中，启动您的服务器，然后在它完成后立即停止它 启动。
> ![启动/停止服务器](./images/discord/start-stop.gif)
> 将 EssentialsXDiscord.jar 拖入插件文件夹 -> 启动服务器 -> 停止服务器

14. 现在您可以开始使用您之前复制的所有内容配置插件。 打开位于 `plugins/EssentialsDiscord/config.yml` 的 EssentialsX Discord 的配置。 当您打开配置时，首先要配置的是您的机器人的令牌。 将配置中的"INSERT-TOKEN-HERE"替换为您之前从第 6 步复制的令牌。
> ![粘贴令牌](./images/discord/paste-token.gif)
> 从第 6 步重新复制令牌 -> 粘贴为令牌值

15. 接下来是公会ID。 将配置中公会值的零替换为您从第 13 步复制的公会 ID。
> ![粘贴公会](./images/discord/paste-guild.gif)

16. 最后，您需要粘贴从第 14 步复制的主要频道 ID，并将其作为主要值粘贴到频道部分，完成后保存配置文件！
> ![粘贴主要](./images/discord/paste-prim.gif)

17. 恭喜，您已经完成了初始设置指南！ 启动服务器时，您应该注意到聊天和其他消息开始显示在您请求的频道中。 现在你已经完成了初始，回到 [目录](#table-of-contents) 看看你还能做些什么很酷的事情！

---

## 控制台中继
控制台中继是不言自明的：它将您控制台上的所有内容中继到您选择的 Discord 频道。 控制台中继非常容易设置，如果您的服务器已经在运行，则无需重新加载它！

0. 这假定您已经完成了初始设置。

1. 转到您的机器人所在的 Discord 服务器，找到您希望用于控制台输出的频道。
    右键单击频道，然后单击"复制 ID"。 保存此 ID 以用于下一步。
> ![副本 ID](./images/discord/copy-cons-id.gif)
> 找到控制台频道 -> 右击 -> `Copy ID`

2. 现在你已经复制了，打开 EssentialsX Discord 配置并找到"console"部分。 在该部分中，将"channel"值的零替换为您从上一步复制的频道 ID。 一旦你粘贴它，确保你保存了配置。
> ![粘贴 ID](./images/discord/paste-cons-id.gif)

3. 最后，如果您的服务器正在运行，请从您的控制台运行"ess reload"，否则启动您的服务器。 您应该注意到控制台输出被定向到该通道！ 如果您不介意默认设置，那么这就是您所需要的。 否则，如果您希望查看可以使用哪些其他选项来自定义控制台输出，请继续关注。

4. 您可以自定义的第一件事是发送到 Discord 的消息格式。 默认情况下，会为每个控制台消息显示时间戳、级别（信息/警告/错误/等）和消息。 假设您想将时间戳和级别设为粗体：由于此消息将使用 Discord 的降价，我们只需在级别和时间戳的两侧添加 \*\* 即可。 然后，完成后，只需执行"/ess reload"，您应该会在 Discord 上看到您的更改。
> ![粗体格式](./images/discord/bold-format.gif)

5.接下来，您还可以配置您希望在控制台消息上方显示的名称。 默认情况下，它是"EssX 控制台中继"，但可以切换为您想要的任何内容。
> ![更改名称](./images/discord/change-name.gif)

6. 最后，您还可以选择启用一个选项，将控制台通道中用户发出的任何消息都视为控制台命令。 这意味着任何可以在您的控制台通道中发送消息的人**都可以作为控制台执行命令**。 建议您坚持使用常规的 ·、execute· 命令（参见 【Discord命令】（#discord-commands)/
》 ！【命令中继】（。、images/discord/command-relay.gif)


7.这就是命令中继的所有选项！



---



## 配置消息

EssentialsXDiscord旨在保持其消息类型系统足够基本，简单的事情几乎不需要改变，同时为您想要的人提供更精细的控制。



为了给您系统的总体概览，EssentialsXDiscord允许您在配置的"频道"部分定义不同的频道 ID默认情况下，"channel是primarystaff如果您只完成了初始设置，则"staff这在大多数情况下都很好。 但是，如果频道 ID无效，消息系统将始终回退到"主要"频道。



现在介绍您自己可以接收的消息类型（这是您将要使用这些通道定义的地方）。 在配置的 ·message-types`部分，您可以在左侧（作为键）看到消息类型列表（加入、离开、聊天等），右侧是通道定义。



举例来说，假设我们想将所有聊天消息发送到他们自己的频道。 我们可以通过创建一个新的频道定义并将"聊天"消息类型设置为所述频道定义来做到这一点。 以下是上述示例的分步说明，您可以按照以下步骤了解如何将其应用于其他用例的要点



1. 在 Discord上找到您只想向其发送聊天消息的频道，然后右键单击该频道并单击

    "复制ID
    》 ！【复制 ID（。、images/discord/chat-copy-id.gif)


    2. 接下来您需要创建实际的频道定义，在本例中我们将其称为"聊天"。 您可以通过向"channelsID作为您在上一步中复制的那个。

    》 ！【新定义】（。、images/discord/new-def.gif)


    3. 最后，向下滚动到"消息类型"部分并将"聊天"消息类型更改为新创建的频道定义。 执行此操作后，如果您的服务器正在运行或启动服务器，请保存并运行"、二十四reload
    》 ！【移动】（。、images/discord/move-def.gif)


    4. 这就是您需要了解的有关消息系统基础知识的全部内容！



    ---



    ## 在 Minecraft中接收 Discord消息

    阅读【配置消息部分】（#configuring-messages)后，您现在应该在配置的"频道"中定义了一些 Discord频道。 您可能想知道如何让您的玩家开始在 Minecraft聊天中看到来自 Discord的消息。 假设我在配置的"频道"部分定义了一个名为"聊天"的频道，我想让玩家在 Minecraft聊天中看到来自该频道的 Discord消息； 这可以通过授予玩家"essentials.discord.receive.chat这会将来自"聊天"频道的所有 Discord消息转发给具有该权限的玩家。 另一个例子：假设我在 Discord中有一个人员频道，我希望只有 Minecraft服务器中的人员才能看到。 如果在配置的 ·channels· 部分定义了 ·staff· 频道，我可以授予工作人员 ·essentials.discord.receive.staff`权限，他们将开始看到来自该频道的消息。



    ---最后，您还可以选择启用一个选项，将控制台通道中用户发出的任何消息都视为控制台命令。 这意味着任何可以在您的控制台通道中发送消息的人**都可以作为控制台执行命令**。 建议您坚持使用常规的 `/execute` 命令（参见 [Discord 命令](#discord-commands)），因为这些命令可以仅限于特定角色/用户，也不限于控制台频道。
> ![命令中继](./images/discord/command-relay.gif)

7.这就是命令中继的所有选项！

---

## 配置消息
EssentialsX Discord 旨在保持其消息类型系统足够基本，简单的事情几乎不需要改变，同时为您想要的人提供更精细的控制。

为了给您系统的总体概览，EssentialsX Discord 允许您在配置的"频道"部分定义不同的频道 ID。 默认情况下，"channels"部分预填充了两个频道，"primary"和"staff"。 如果您只完成了初始设置，则"staff"通道定义全为零。 这在大多数情况下都很好。 但是，如果频道 ID 无效，消息系统将始终回退到"主要"频道。

现在介绍您自己可以接收的消息类型（这是您将要使用这些通道定义的地方）。 在配置的 `message-types` 部分，您可以在左侧（作为键）看到消息类型列表（加入/离开/聊天等），右侧是通道定义。

举例来说，假设我们想将所有聊天消息发送到他们自己的频道。 我们可以通过创建一个新的频道定义并将"聊天"消息类型设置为所述频道定义来做到这一点。 以下是上述示例的分步说明，您可以按照以下步骤了解如何将其应用于其他用例的要点

1. 在 Discord 上找到您只想向其发送聊天消息的频道，然后右键单击该频道并单击
    "复制ID"。
> ![复制 ID](./images/discord/chat-copy-id.gif)

2. 接下来您需要创建实际的频道定义，在本例中我们将其称为"聊天"。 您可以通过向"channels"部分添加一个新条目来创建通道定义，其中键作为其名称，ID 作为您在上一步中复制的那个。
> ![新定义](./images/discord/new-def.gif)

3. 最后，向下滚动到"消息类型"部分并将"聊天"消息类型更改为新创建的频道定义。 执行此操作后，如果您的服务器正在运行或启动服务器，请保存并运行"/ess reload"。
> ![移动](./images/discord/move-def.gif)

4. 这就是您需要了解的有关消息系统基础知识的全部内容！

---

## 在 Minecraft 中接收 Discord 消息
阅读[配置消息部分](#configuring-messages) 后，您现在应该在配置的"频道"中定义了一些 Discord 频道。 您可能想知道如何让您的玩家开始在 Minecraft 聊天中看到来自 Discord 的消息。 假设我在配置的"频道"部分定义了一个名为"聊天"的频道，我想让玩家在 Minecraft 聊天中看到来自该频道的 Discord 消息； 这可以通过授予玩家"essentials.discord.receive.chat"权限非常简单地完成。 这会将来自"聊天"频道的所有 Discord 消息转发给具有该权限的玩家。 另一个例子：假设我在 Discord 中有一个人员频道，我希望只有 Minecraft 服务器中的人员才能看到。 如果在配置的 `channels` 部分定义了 `staff` 频道，我可以授予工作人员 `essentials.discord.receive.staff` 权限，他们将开始看到来自该频道的消息。

---
## Discord 命令
EssentialsX Discord 使用 Discord 的斜杠命令系统，让您在 Discord 中键入命令，而服务器中的其他人不会看到它。 使用此系统，您可以执行控制台命令、消息玩家并查看当前玩家列表。

例如，默认情况下 `/execute` 命令如下所示：
> ![/execute](./images/discord/execute-comand.gif)

如您所见，您可以无缝地运行命令，而不会让人看到您的命令内容或他们的响应。 此外，您还可以在查看完回复后将其删除，这样它们就不会扰乱您的聊天。

然而，这一切都是可配置的！ 在配置的 `commands` 部分，有大量的选项可以根据每个命令配置设置。 下面解释了所有配置选项的含义以及如何使用它们。

* `enabled`
    * Default: `true`
    * 描述：`是否应该启用该命令并因此在 Discord 上显示。 请注意，在此选项生效之前，您必须重新启动 Minecraft 服务器。
* `hide-command`
    * Default: `true`
    * 描述：`是否其他人不应该能够看到你执行的命令。 设置为 false 将允许与您处于同一频道的人确切地看到您执行的命令。 在下面的示例中，您可以看到禁用此选项如何显示用户消息和他们执行的命令。`
     * 例子： ![Show Command](./images/discord/show-command.gif)
* `allowed-roles`
    * 描述：`允许使用该命令的用户 ID 或角色名称/ID 的列表。 您还可以使用'*'以允许所有人使用该命令。
* `admin-roles`
    * `在命令中具有额外功能的用户 ID 或角色名称/ID 的列表。 例如，在 list 命令中，admin-roles 允许玩家们看到消失的玩家。`

---

## 杂项权限
EssentialsX Discord 有一些其他权限，了解这些权限可能很重要：

* `essentials.discord.markdown` - 允许玩家绕过 Markdown 过滤器，这样他们就可以使用粗体/下划线/斜体等。 他们的 Minecraft Discord 聊天消息。
* `essentials.discord.ping` - 允许玩家绕过 ping 过滤器，这样他们就可以从 Minecraft 聊天中 ping @everyone/@here。

---

## 开发者接口
EssentialsX Discord 有一个相当广泛的 API，允许任何第三方插件在其中构建自己的集成。 除了下面的具体示例，您还可以在 [此处](https://jd-v2.essentialsx.net/EssentialsDiscord) 查看 EssentialsX Discord 的 javadoc。

### 向 Discord 发送消息
EssentialsX Discord 组织了可以与其一起发送的消息类型
Discord 上 `config.yml` 的 `message-types` 部分下的目的地。 EssentialsX Discord API 使用"message-types"来解析您要发送的频道 ID
消息给。

#### 使用内置消息通道 
EssentialsX Discord 定义了一些内置的"消息类型"，您可能已经适合您的用例（例如向 MC->Discord 聊天中继通道发送消息）。 可以在 [`MessageType.DefaultTypes`](https://github.com/EssentialsX/Essentials/blob/2.x/EssentialsDiscord/src/main/java/net/essentialsx/ api/v2/services/discord/MessageType.java#L47-L67）。

以下是向内置聊天频道发送消息的示例：
```java
// The built-in channel you want to send your message to, in this case the chat channel.
final MessageType channel = MessageType.DefaultTypes.CHAT;
// Set to true if your message should be allowed to ping @everyone, @here, or roles.
// If you are sending user-generated content, you probably should keep this as false.
final boolean allowGroupMentions = false;
// Send the actual message
final DiscordService api = Bukkit.getServicesManager().load(DiscordService.class);
api.sendMessage(channel, "My Epic Message", allowGroupMentions);
```

#### 使用自己的消息通道
如果您想创建自己的消息类型以允许您的用户明确地将您的消息与我们的其他内置消息分开，您也可以通过创建一个新的 [`MessageType`](https://github.com/EssentialsX /Essentials/blob/2.x/EssentialsDiscord/src/main/java/net/essentialsx/api/v2/services/discord/MessageType.java）。
构造函数中提供的密钥应该是您希望用户在我们配置的"消息类型"部分中使用的密钥。 此键也应全部小写，并且可以包含数字或破折号。 如果您愿意，您*可以*也可以将 Discord 频道 ID 作为密钥
让您的用户在您的配置而不是我们的配置中定义频道 ID。 创建"MessageType"后，您还需要通过调用向 Essentialsx Discord 注册它
[`DiscordService#registerMessageType`](https://github.com/EssentialsX/Essentials/blob/2.x/EssentialsDiscord/src/main/java/net/essentialsx/api/v2/services/discord/DiscordService.java# L24-L30）。

下面是一个使用您自己的消息类型发送消息的示例：
```java
public class CustomTypeExample {
    private final DiscordService api;
    private final MessageType type;
    
    public CustomTypeExample(final Plugin plugin) {
      // Gets the EssentialsX Discord API service, so we can register our type and
      // send a message with it later.
      api = Bukkit.getServicesManager().load(DiscordService.class);
      
      // Create a new message type for the user to define in our config.
      // Unless you're putting a discord channel id as the type key, it's probably 
      // a good idea to store this object, so you don't create it every time.
      type = new MessageType("my-awesome-channel");
      
      // Registers the type we just created with EssentialsX Discord.
      api.registerMessageType(plugin, type);
    }
    
    @EventHandler()
    public void onAwesomeEvent(AwesomeEvent event) {
      // Set to true if your message should be allowed to ping @everyone, @here, or roles.
      // If you are sending user-generated content, you probably should keep this as false.
      final boolean allowGroupMentions = false;
      // Send the actual message
      api.sendMessage(type, "The player, " + event.getPlayer() + ", did something awesome!", allowPing);
    }
}
```

### 防止某些消息作为聊天发送
根据您的插件向玩家发送某些类型的聊天消息的方式，可能有
EssentialsX Discord 不小心广播了一条只针对一小群人的消息。 为了让您的插件阻止这种情况的发生，您必须监听`DiscordChatMessageEvent`。

下面是一个员工聊天插件如何取消消息的示例：
```java
public class StaffChatExample {
    private final StaffChatPlugin plugin = ...;
    
    @EventHandler()
    public void onDiscordChatMessage(DiscordChatMessageEvent event) {
      // Checks if the player is in staff chat mode in this theoretical plugin.
      if (plugin.isPlayerInStaffChat(event.getPlayer()) || 
              // or we could check if their message started with a # if we use that
              // to indicate typing in a specific channel.
              event.getMessage().startsWith("#")) {
          event.setCanceled(true);
      }
    }
}
```

此外，您还可以查看 [TownyChat 的 EssentialsX Discord 挂钩](https://github.com/TownyAdvanced/TownyChat/commit/5bee9611aa4200e3cde1a28af48c25caa4aec649)。

### 注册一个 Discord 斜杠命令
EssentialsX Discord 还允许您直接向 Discord 本身注册斜杠命令，以便为您的用户提供一种与 Discord 上的插件交互的方式！

要开始编写斜线命令，您需要做的第一件事是创建一个斜线命令类。 为了本教程，我将使用经济插件作为创建此斜杠命令的假设插件。

对于这个斜杠命令，我将创建一个简单的字符串命令（用于玩家名称）并检查他们的余额。
```java
public class BalanceSlashCommand extends InteractionCommand {
    private final MyEconomyPlugin plugin = ...;
    
    @Override
    public void onCommand(InteractionEvent event) {
        // The name of the argument here has to be the same you used in getArguments()
        final String playerName = event.getStringArgument("player");
        final Player player = Bukkit.getPlayerExact(playerName);
        if (player == null) {
            event.reply("A player by that name could not be found!");
            return;
        }
        
        final int balance = plugin.getBalance(player);
        
        // It is important you reply to the InteractionEvent at least once as discord
        // will show your bot is 'thinking' until you do so.
        event.reply("The balance of " + player.getName() + " is $" + balance);
    }
    
    @Override
    public String getName() {
        // This should return the name of the command as you want it to appear in discord.
        // This method should never return different values.
        return "balance";
    }

    @Override
    public String getDescription() {
        // This should return the description of the command as you want it 
        // to appear in discord.
        // This method should never return different values.
        return "Checks the balance of the given player";
    }
    
    @Override
    public List<InteractionCommandArgument> getArguments() {
        // Should return a list of arguments that will be used in your command.
        // If you don't want any arguments, you can return null here.
        return List.of(
                new InteractionCommandArgument(
                        // This should be the name of the command argument.
                        // Keep it a single world, all lower case.
                        "player", 
                        // This is the description of the argument.
                        "The player to check the balance of", 
                        // This is the type of the argument you'd like to receive from
                        // discord.
                        InteractionCommandArgumentType.STRING,
                        // Should be set to true if the argument is required to send
                        // the command from discord.
                        true));
    }
    
    @Override
    public boolean isEphemeral() {
        // Whether the command and response should be hidden to other users on discord.
        // Return true here in order to hide command/responses from other discord users.
        return false;
    }
    
    @Override
    public boolean isDisabled() {
        // Whether the command should be prevented from being registered/executed.
        // Return true here in order to mark the command as disabled.
        return false;
    }
}
```

创建斜杠命令后，现在是注册它的时候了。 最佳做法是在您的插件的“onEnable”中注册它们，这样您的命令就会出现在发送到 Discord 的第一批命令中。

您可以通过执行以下操作向 EssentialsX Discord 注册您的命令：
```java
...
import net.essentialsx.api.v2.services.discord.DiscordService;
...

public class MyEconomyPlugin {
  @Override
  public void onEnable() {
    final DiscordService api = Bukkit.getServicesManager().load(DiscordService.class);
    api.getInteractionController().registerCommand(new BalanceSlashCommand());
  }
}
```

---
