# XMPP

可扩展消息传递和状态协议 (XMPP) 是一种开放标准通信协议，用于基于 XML 的面向消息的中间件。 该协议最初称为 Jabber。

除了明显的"XMPP"或"Jabber"品牌服务外，还有一些使用 XMPP 或为其服务提供 XMPP 桥接器或网关的服务。 Google Talk、Live journal 和 Ovi 使用 XMPP，而 Facebook 聊天允许 XMPP 连接到他们的服务。 XMPP 与 MSN 和 Yahoo 之间也有第三方网关服务。

打算将 Google Talk 与 XMPP 结合使用的用户请确保阅读 xmpp 更改：https://www.fsf.org/blogs/sysadmin/google-backslides-on-federated-instant-messaging-on-purpose

有大量的 XMPP 客户端，其中许多客户端允许连接到多种服务，例如：iChat、Trillian、Miranda、fring、Adium、bitlbee、Pidgin 和 Digsby。

## Essentials XMPP

Essentials XMPP 扩展为 Bukkit 服务器提供了一个 XMPP 网关。

### 玩家XMPP

使用 XMPP 服务的玩家可以在游戏中设置他们的 XMPP 地址，这允许其他玩家在未连接到 minecraft 时向他们发送消息。

### XMPP 间谍

如果您为用户启用 XMPP 间谍，该玩家将获得发送到其 XMPP 帐户的游戏内消息的副本，就好像他们已连接并在游戏内一样。

### 控制台控制

如果您允许帐户从 XMPP 发出命令，则该用户将能够使用类似于直接在控制台中键入的控制台命令 (op)。

### 控制平台视图

如果您注册一个帐户以查看日志，该帐户将被转发消息发送到具有匹配或更高警告级别的日志。 这直接复制了您直接在控制台上看到的内容。

## 使用 XMPP

当您配置 XMPP 时，您会为服务器创建一个新帐户，并将您当前的帐户与提供给服务器的帐户相关联。 在大多数服务中，这类似于将服务器添加到您的"朋友列表"或"联系人列表"。 虽然此插件的两个主要用途是允许服务器管理员远程连接到服务器，但它也有助于鼓励服务器上用户之间的联系。

### 设置您的帐户
用户可以使用"/setxmpp <address>"命令注册自己的 XMPP 地址。 用户可以注册任何 XMPP/Jabber 兼容帐户，可以是专门为 XMPP 设置的帐户，也可以是提供 jabber id 的系统。 Facebook 用户可以在网站浏览中找到更多关于他们的 XMPP 服务的信息，但基本上是 /setxmpp <username>@chat.facebook.com。 Gmail 用户应该只使用他们的 gmail 地址。

### 向用户发送消息
要向另一个用户发送消息，您可以使用"/xmpp <account> <message>"命令，使用玩家在游戏中的名称。

### 聊天间谍
并非每个允许 XMPP 的服务器都会启用 xmppspy，启用此功能会将所有游戏内聊天转发到 XMPP 帐户。 这将允许用户通过向服务器的 XMPP 地址发送消息来像在游戏中一样聊天。

## 配置 XMPP
设置 Essentials XMPP 连接器非常简单，您需要创建一个 XMPP 帐户，并提供要使用的 Essentials 的详细信息。

### 创建账户
在 Essentials 可以与用户 XMPP 帐户通信之前，您首先需要使用帐户对其进行设置。 有几种不同的方法可以处理这个问题，但建议您专门为服务器创建一个帐户。

由于 XMPP 是一种开放协议，您可以在本地设置自己的 XMPP 服务器，或使用您的 ISP/主机提供的服务。 只要服务器连接到其中一个公共 XMPP 节点，您就可以与使用其他 XMPP 服务的用户进行通信。

为了简单起见，在 Jabber.org 创建一个免费帐户可能是最简单的。

### 配置文件
XMPP 连接的配置文件位于其自己的文件夹中。 您将在 /plugins/EssentialsXMPP/config.yml 中找到该文件
```
xmpp:
  sasl-enabled: true
  server: 'jabber.org'
  port: 5222
  user: 'khobbits@jabber.org'
  password: 'password'
```
以上是连接到 jabber.org XMPP 服务器所需的配置设置示例。 还有更多选项，但通常您不需要设置服务名称或使用非标准端口。 对于您的具体配置设置，您需要检查您的 XMPP 提供商。

### 登录用户
您可以允许 XMPP 用户接收服务器信息。
```
log-enabled: true
log-level: info
log-users:
  - 'khobbits@gmail.com'
```
上面的示例将允许具有 XMPP 地址"khobbits@gmail.com"的用户接收所有服务器日志信息以转发到他们的帐户。 日志级别，是应该转发给用户的最低要求级别，值可以是：info、warning、severe

### 运营用户
您可以允许 XMPP 用户向服务器发出命令（他们需要成为登录用户才能真正看到任何输出）。
```
op-users:
  - 'khobbits@gmail.com'
```
上面的示例将允许具有 XMPP 地址"khobbits@gmail.com"的用户发出命令，就好像他们在控制台中输入一样。
某些客户端可能需要 /say 或 /raw 才能正确使用 /commands，如果客户端拦截了此命令。