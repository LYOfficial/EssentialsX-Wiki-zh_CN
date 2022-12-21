# 命令冷却

**这个特性在 [build 369](https://ci.ender.zone/job/EssentialsX) ([09acbcd](https://github.com/drtshock/Essentials/commit/09acbcdb05f34e0043116f1866904b0ff0f03ddd)) 加入.** 在 [ #110](https://github.com/drtshock/Essentials/issues/110) _被请求_。 在 _PR_ [ #692](https://github.com/EssentialsX/Essentials/pull/692) _被实现_.

本特性引用了将命令进行延时的功能。如果你想限制玩家不要高强度使用 `/feed` 或者 `/home` ，你只要在配置文件中加上几行：

```yaml
command-cooldowns:
  feed: 10 # 10 seconds
  home: 70 # 1 minute 10 seconds
```

**高级用户** 可以使用通配符进行命令匹配，通配符通常是星号"*"。例如，要匹配所有带有 `potato` 的命令，只需如下更改配置文件即可：

```yaml
command-cooldowns:
  '*potato*': 30
```

**注：** 因 YAML 的设计,任何以星号开头的命令，必须使用引号（'单引号'或"双引号"）将字符串包括起来。

对于**了解正则表达式的用户**来说，这个特性同样兼容正则表达式。如果你想在 EssentialsX 中使用正则表达式，必须以 '^' 开头，其次才是显式正则表达式。

```yaml
command-cooldowns:
  '^^ban([^ip])?( .*)?': 30 # match any ban command that isn't `banip`.
```

**注1：** 先导符号 '^' 不计算在正则表达式内，在解析正则表达式时会将其自动删除。  所以 `'^ban([^ip])?( .*)?'` 最终解析成了 `'ban([^ip])?( .*)?'`。

**注2：** 如果插件命令以如`^mycommand`这样的符号开始，插入符号必须使用黑斜杠 '\' 转义，放置 EssentialsX将该命令解译为 Regex。

# 仅在服务器启动时记录冷却时间

默认情况下，EssentialsX 只会在服务器启动的状态时内记录冷却时间。这意味着玩家的命令冷却时间在关服时会被存储，启动时会被读取。这对于冷却时间较长的命令特别有效。

不管怎样，这个功能可以被关闭，使 EssentialsX 的冷却时间只记录到服务器关闭时。当服务器启动时重置所有冷却时间。
要禁用此功能，只需对配置文件进行如下更改：

```yaml
command-cooldown-persistence: false
```

**注：** 若您的配置文件里没有 `command-cooldown-persistence` 这一条，可以在您的配置文件的任意位置中任意位置增加本条配置项（只要它不缩进）。


# 无视冷却
**这个特性是在构建 #377 中被增加的。**

当用户有 `essentials.commandcooldowns.bypass` 权限时，将会无视所有权限的冷却时间。