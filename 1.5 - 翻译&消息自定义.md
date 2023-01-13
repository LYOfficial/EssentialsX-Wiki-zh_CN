# 翻译
EssentialsX把所有的产生的信息按照模板存储在信息文件中，并且在该文件中伴随生成许多[已经写入的语言](#支持语言)。通过把你修改的文件放入 `plugins/Essentials/` 文件夹，你可以很容易地替换或者扩展这些文件来定制或完善你的服务器。

## 切换插件语言
你可以通过修改文件 `config.yml` 中的 `locale` 项来告诉EssentialsX你想使用哪种语言:
```
# 为插件中所有的信息设置语言。
# ...
locale: de
```
请注意你需要把 `locale` 行通过**删除前面的 `#` 来取消注释**。如果 `#` 存在，EssentialX将尝试使用你的系统正在使用的语言。

下面是一些EssentialsX所支持的语言:
## 支持语言
- **美式英语**: `en`
  - **英式英语**: `en_GB`
- **捷克语**: `cs`
- **丹麦语**: `da`
- **德语**: `de`
- **西班牙**: `es`
- **爱沙尼亚语**: `et`
- **芬兰语**: `fi`
- **法语**: `fr`
- **匈牙利语**: `hu`
- **意大利语**: `it`
- **韩语**: `ko`
- **立陶宛语**: `lt`
- **荷兰语**: `nl`
- **波兰语**: `pl`
- **葡萄牙语**: `pt`
  - **巴西语**: `pt_BR`
- **罗马尼亚语**: `ro`
- **俄语**: `ru`
- **瑞典语**: `sv`
- **土耳其语**: `tr`
- 中文:
  - **简体中文**: `zh`
  - **香港中文**: `zh_HK`
  - **繁体中文**: `zh_TW`

## 切换地区
EssentialsX在jar文件中捆绑了许多不同语言的信息文件，所以你可以通过从EssentialsX.jar中提取出一份你想要的信息文件。只需要把想更改的信息文件放进 `plugins/Essentials` 文件夹里并开始编辑。请注意文件会定时更新；你可能想保留一个备份，那么要用一个比较工具以便允许简单的更新。

如果你认为能够为EssentialsX改良翻译，或者想要为捆绑包提交你的翻译，请随时向EssentialsX官方提交你所修改的语言包。Essentials经常修改并提升，但当制作者们不用语言交流的时候，语言文件被落下是很正常的。你可以在我们的[Crowdin网站](http://crowdin.com/project/essentialsx-official)上提交改进后的语言文件。

## 自定义信息
因为所有的插件信息都定义在信息文件里，你可以通过为所有EssentialsX指令更改文本和色调搭完全自定义样貌和风格。

仅仅只需要把你编辑过的（有正确区域后缀的）语言文件放入 `plugins/Essentials` 文件夹里并确保在配置文件中的语言设置是匹配的（`locale: en` -> `messages_en.properties`），然后重启服务器即可。

如果你碰上了麻烦，[尝试这个视频教程](http://www.youtube.com/watch?v=9Uan2oJ9zK8)。注意这个视频是为Essentials插件制作的而不是EssentialsX。

有时你可能需要进行更新文件来处理EssentialsX中如变更参量，变更信息实际句法规则的一些变化。这可以用一个比较工具，如[Diffchecker](http://www.diffchecker.com)，它会把两份文件的改变之处标为高亮。

## 略微改动
当EssentialsX查找一个信息时，如果它不在你这个版本里，插件将使用**build-in-version**来代替。这说明如果你只是想在整个翻译文件中修改一点，你可以通过备份你正在使用的路径为 `plugin/Essentials` 的语言文件，并删除文件中除你想修改的信息之外的所有信息来实现这个过程。这意味着你无须担心使你的信息文件跟上每次EssentialsX的更新。

当仅仅编辑几个关键词时，这个步骤应该参考这里[（点击以打开图片）](http://wiki.ess3.net/w/images/0/0c/Locale.PNG)来进行。

## 颜色
如果你有一个旧的信息文件，你可能注意到了许多诸如 `\u00a7` 的文本。这些是统一码字符的换码，但在新版本支持UTF-8编码文件的EssentialsX不再需要了。你可以把这些代码用一个工具如[Interactive native2ascii](http://native2ascii.net)转换成UTF-8的字符。

要使用RGB颜色代码，你将需要用到Spigot的 `§x§R§R§G§G§B§B` 格式，这里的RRGGBB来源于颜色的十六进制代码。你也可以使用[过时但被广泛应用的颜色代码（`§0` 到 `§f`）](https://minecraft.fandom.com/wiki/Formatting_codes#Color_codes)和[格式化代码](https://minecraft.fandom.com/wiki/Formatting_codes#Formatting_codes)。

## 例子
假设您只是想更改货币的输出方式，以便货币符号出现在余额之后：
- 务必确认读过上述关于自定义语言/信息的知识。
- 找到行"currency={0}{1}"
- 交换数字，他现在看起来是"currency={1}{0}"。{1}是余额，{0}是货币符号。如果你想也可以在这添加空格。
- 保存文件并重启服务器或者在服务端输入/ess reload。

## 禁用信息
通过把信息字符串设置为空白，大多数用户消息可以简单地被禁用或隐藏，例如：
```
noNewMail=
```

## 参与
如果你想贡献你的翻译，你可以用[Crowdin](http://crowdin.com/project/essentialsx-official)来投稿。

## 其他文件
### plugin.yml
除了信息文件，还有其他一些你可能想改变的位置和设置。EssentialsX帮助系统自动读取每个插件的 `plugin.yml` ，包括它本身，并且用这些文件显示语法和命令描述。为了有一个完整的游戏内翻译，你可能想要把这些文件更新为你的本地语言。

### Config file（配置文件）
EssentialsX中有许多可以通过编辑 `plugins/Essentials/config.yml` 来改变的设置，如货币格式。这些是独立于 `locale` 设置的并且不用编辑jar文件就可以改变。

### Text commands（文本命令）
EssentialsX的文本指令如 `/motd` 和 `/rules` 可以在完全独立于信息文件和配置文件之外的条件下被编辑。只需要在游戏里运行一次指令，然后找到位于 `plugins/Essentials` 中相应的文本文档来编辑即可。