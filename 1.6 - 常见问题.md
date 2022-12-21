# EssentialsX 常见问题

## 告示功能无法运行
在 `plugins/Essentials/config.yml` 文件中，你需要删除 `enabledSigns` 这一行下面的每一种类型的告示前的 `#` 来取消注释：

```yaml
enabledSigns:
  #- color
  - balance
  #- buy
```

在这个例子中, 这个 `[balance]` 告示是启用的，但是 `[buy]` 告示没有启用。

注意一下，启用 `color` 告示意味着玩家将被允许在告示文本中使用颜色代码，但是仍然需要另一个告示类型是启用的。

## EssentialsX 覆盖来自 Spigot 或别的插件的命令
**相关问题: #[1458](https://github.com/EssentialsX/Essentials/issues/1458)**  

对于 Bukkit ，你可以通过 `commands.yml` 文件为命令创建别名，它应该位于您的服务器根目录中。

例如：
* 用  [spark](https://github.com/lucko/spark) 的 `/profiler`  命令覆盖替换 `/gc` 命令
* 用 [vanilla `/tell`](https://minecraft.gamepedia.com/Commands/tell) 的 `/tell` 命令覆盖 `/tell` 命令
* 强制使用 `/msg` 命令运行EssentialsX的 `/msg` 

示例别名：

```yaml
aliases:
    gc:
    - "spark:profiler $1-"
    tell:
    - "minecraft:tell $1-"
    msg:
    - "essentials:msg $1-"
```

看这个 [Bukkit维基百科页面](https://bukkit.gamepedia.com/Commands.yml#aliases) 来获得更多信息。

## 有其他插件覆盖EssentialsX命令
通常地，如果EssentialsX发现有另一个插件的命令与EssentialsX自己的命令同名，它就会优先把这个命令让给另一个插件执行。但是，您可以修改 `config.yml` 这个文件的[`overridden-commands` 部分](https://github.com/EssentialsX/Essentials/blob/2.x/Essentials/src/main/resources/config.yml#L162) 来强制让EssentialsX优先处理同名命令。对于EssentialsX而言就是不把命令让给其他插件执行。

如果要强制EssentialsX处理 /msg命令，而不是把这个命令让给另一个插件执行，你的配置文件里应该是这样的：

```yaml
overridden-commands:
  - msg
```

注意：在某些情况下，您还得要在配置文件里将命令的别名改为带 `essentials:`  的，[详情在上面](https://github.com/EssentialsX/Essentials/wiki/Common-Issues#essentialsx-overrides-a-command-from-spigot-or-another-plugin) 。另外，如果你有一个插件运行在你的代理?上(例如[BungeeCord](https://www.spigotmc.org/wiki/bungeecord/)/[Waterfall](https://github.com/PaperMC/Waterfall) 或 [Velocity](https://velocitypowered.com))，服务器可能无法获得这个命令的信息？。EssentialsX 对此无能为力，你需要在代理上修复这个问题。

## Tab补全不适用于覆盖了EssentialsX命令的命令
**相关问题: #[1384](/EssentialsX/Essentials/issues/1384)**  
你可以为其他插件的命令添加别名，就可以修复Tab补全功能了。

## 我需要使用GroupManager这个插件！ <br /> 我应该在哪找到并更新GroupManager呢？

EssentialsX这边不支持过时的或者损坏的插件，我们非常建议您把 GroupManager 插件换成 [LuckPerms](https://github.com/lucko/LuckPerms) 插件，因为这个插件到现在仍然还在维护和定期更新。

## 我应该如何构建EssentialsX呢？

你需要安装最新的JDK和Maven，然后你可以使用 [Spigot构建工具](https://www.spigotmc.org/wiki/buildtools/)  来构建几个不同的Spigot版本：


```bash
java -jar BuildTools.jar --rev 1.8
java -jar BuildTools.jar --rev 1.8.3
java -jar BuildTools.jar --rev 1.9
java -jar BuildTools.jar --rev 1.9.4
```

这一步是必要的，因为这一步可以让EssentialsX可以更兼容的针对旧版本的Spigot服务器构建，而且这一步你只需要做这一次，接下来[下载或者说克隆 EssentialsX 本体](https://github.com/EssentialsX/Essentials)，在EssentialsX的根目录下打开一个终端（例如CMD），然后运行这个：

```bash
./gradlew build
```

如果没出错的话，你就可以在 `jars/` 目录或者 `build/libs/`  每个模块的目录中找到你构建的每个插件的jar文件了。


## 如何添加EssentialsX作为其他插件的依赖？
### Repositores
你想在你的插件中集成 EssentialsX 吗？如果是，那么您可以使用 EssentialsX Maven repo 来利用 EssentialsX 的 API 进行构建制作。

发行版托管在Maven repo 中：
`https://repo.essentialsx.net/releases/`, 

快照版被托管在这里： `https://repo.essentialsx.net/snapshots/`.

要把EssentialsX添加到您的构建系统中，您应该使用以下构件:

| Type            | Group ID        | Artifact ID | Version         |
| :-------------- | :-------------- | :---------- | :-------------- |
| Latest release  | net.essentialsx | EssentialsX | 2.19.0
| Snapshots       | net.essentialsx | EssentialsX | 2.19.1-SNAPSHOT |
| Older releases  | net.ess3        | EssentialsX | 2.18.2          |

注意:在2.18.2版本之前，EssentialsX使用的组ID是net.ess3，但从2.19.0快照版本开始，组ID改为了net.essentialsx，所以当更新你的插件时，确保你所使用的组ID是正确的。

### 发行版
#### Maven
在你的 `pom.xml` 的 `repositories` 下，你需要为EssentialsX CI服务器添加一个新的 `repository` ：

```xml
<repositories>
    ...
    <repository>
        <id>essentials-releases</id>
        <url>https://repo.essentialsx.net/releases/</url>
    </repository>
    <repository>
        <id>paper-repo</id>
        <url>https://papermc.io/repo/repository/maven-public/</url>
    </repository>
</repositories>
```

接下来，把 EssentialsX 当做一个 `dependency` 添加到 `dependencies` 中:

```xml
<dependencies>
    ...
    <dependency>
        <groupId>net.essentialsx</groupId>
        <artifactId>EssentialsX</artifactId>
        <version>2.19.0</version>
        <scope>provided</scope>
    </dependency>
</dependencies>
```


如果你不希望在你的插件是中包含整个 EssentialsX 的话，就确保你提供了正确的依赖吧。
然后您现在应该就能够在您的IDE中使用 EssentialsX 的 API 进行构建制作了，但是您可能需要重载您的项目才能起作用。

#### Gradle
首先，将以下库添加到你的 `build.gradle` 文件中：

```groovy
repositories {
    maven {
        name "essentialsx-releases"
        url "https://repo.essentialsx.net/releases/"
    }
    maven {
        name "papermc"
        url "https://papermc.io/repo/repository/maven-public/"
    }
}
```

然后，将以下依赖项添加到 `compileOnly`  的依赖项中

```groovy
dependencies {
    ...
    compileOnly 'net.essentialsx:EssentialsX:2.19.0'
}
```

现在您应该就能够在您的IDE中使用EssentialsX的API进行构建制作了。

### 快照版
#### Maven
在你的 `pom.xml` 的 `repositories` 下，你需要为EssentialsX CI服务器添加一个新的 `repository` ：

```xml
<repositories>
    ...
    <repository>
        <id>essentials-snapshots</id>
        <url>https://repo.essentialsx.net/snapshots/</url>
    </repository>
    <repository>
        <id>paper-repo</id>
        <url>https://papermc.io/repo/repository/maven-public/</url>
    </repository>
</repositories>
```

接下来，把 EssentialsX 当做一个 `dependency` 添加到 `dependencies` 中:

```xml
<dependencies>
    ...
    <dependency>
        <groupId>net.essentialsx</groupId>
        <artifactId>EssentialsX</artifactId>
        <version>2.19.1-SNAPSHOT</version>
        <scope>provided</scope>
    </dependency>
</dependencies>
```

如果你不希望在你的插件中包含整个EssentialsX的话，就确保你提供了正确的依赖吧。
然后您现在应该就能够在您的IDE中使用EssentialsX的API进行构建制作了，但是您可能需要重载您的项目才能起作用。

#### Gradle
首先，将以下库添加到你的 `build.gradle` 文件中：

```groovy
repositories {
    maven {
        name "essentialsx-snapshots"
        url "https://repo.essentialsx.net/snapshots/"
    }
    maven {
        name "papermc"
        url "https://papermc.io/repo/repository/maven-public/"
    }
}
```

然后，将以下依赖项添加到 `compileOnly`  的依赖项中

```groovy
dependencies {
    ...
    compileOnly 'net.essentialsx:EssentialsX:2.19.1-SNAPSHOT'
}
```

现在您应该就能够在您的IDE中使用EssentialsX的API进行构建制作了。