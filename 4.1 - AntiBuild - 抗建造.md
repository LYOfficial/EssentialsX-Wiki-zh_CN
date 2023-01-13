# AntiBuild - 抗建造

EssentialsAntiBuild 是一个相当新的插件，它是从 EssentialsProtect 中提取反构建功能并为阻止某些操作添加更好支持的结果。

## 概览

移至 AntiBuild 的功能如下：

* 阻止地方黑名单
* 拦截黑名单
* 项目使用黑名单
* 活塞块移动黑名单
* 基于权限系统的地方保护
* 基于权限系统的中断保护
* 基于权限系统的使用保护

## 旧系统支持

EssentialsAntiBuild 仍然支持旧的 EssProtect 黑名单系统语法，您可以在其中列出要在服务器范围内阻止的块类型。

该系统允许您使用以下配置设置按 ID 或名称列出项目：

```
 blacklist:

   # 应该阻止玩家放置哪些方块
   placement: 10,11,46,327

   # 应该阻止玩家使用哪些物品
   usage: 327

   # 应该防止玩家破坏哪些方块
   break:

   # 哪些方块不能被活塞推动
   piston:
```
您可以使用以下权限免除玩家的这些限制：
```
 essentials.protect.exemptplacement
 essentials.protect.exemptusage
 essentials.protect.exemptbreak
```

## 建立警报系统

Essentials 仍然支持旧的警报系统，您可以在其中列出项目 ID，当放置/损坏/与之交互时会触发员工警报。

该系统允许您使用以下配置设置按 ID 或名称列出项目：
```
  alert:
   on-placement: 10,11,46,327
   on-use: 327
   on-break:
```
每当用户触发这些警报时，具有以下权限的人都会收到通知：
```
essentials.protect.alerts
```
您还可以通过向玩家提供以下信息来免除玩家触发这些警报：
```
essentials.protect.alerts.notrigger
```

反建筑

### 旧版支持
在许多权限系统中，您会发现对构建切换的支持，或者具有旨在允许人们构建的构建权限。 如果用户在其中一个系统中启用了构建或具有以下选择退出权限，则他们将免于以下权限检查。

### 全局选择退出
如果您有不想对其执行构建检查的玩家。 IE。 您希望他们能够使用任何未列入黑名单的块进行构建。 授予玩家以下权限。 建议尽可能这样做，因为它减少了每次玩家放置/破坏方块时服务器需要进行的检查次数。
```
   essentials.build
```
###权限控制
假设玩家在他们的权限文件中没有"essentials.build"权限或"build: true"，当他们试图放置、交互或破坏方块时，将检查他们是否有基于项目的权限。

权限遵循以下语法：
```
 essentials.build.place.<id>
 essentials.build.place.<id>:
 essentials.build.break.<id>
 essentials.build.break.<id>:
 essentials.build.interact.<id>
 essentials.build.interact.<id>:
 essentials.build.craft.<id>
 essentials.build.craft.<id>:
 essentials.build.pickup.<id>
 essentials.build.pickup.<id>:
 essentials.build.drop.<id>
 essentials.build.drop.<id>:
```
这些权限可以直接给定或使用通配符给定，因此例如可以执行以下操作：
```
 permissions:
 - essentials.build.*
 - -essentials.build.place.29
```
这将允许用户放置/破坏除放置活塞之外的所有类型的方块。

### 注意事项

#### PEX
PEX 没有正确遵循 superperms 规则，其行为会略有不同，因为 '<id>' 权限将不起作用。 但是，您仍然可以使用 '<id>:' 权限。 如果您需要将单个块的所有数据值列入白名单/否定，请改用：'<id>:*'。 例如：
```
 permissions:
 - -essentials.build.place.54:*
 - essentials.build.*
```

或者，您可以使用 PermissionsEx 附带的 modifyworld 插件。

#### 互动
当用户试图放置一个块时，他们也会与他们试图放置它的块"交互"。 因此，如果玩家试图将一块泥土放在沙子上，他们将需要沙子的交互许可和泥土的放置许可。 "交互"检查基于用户点击的项目，并不总是下面的块。 一般来说，如果您希望用户能够构建，最好给他们"essentials.build.interact.*"或"essentials.build.*"或上面的全局退出权限。