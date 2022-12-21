# BannerMeta

BannerMeta是一个可以让你自定义旗帜和盾牌的系统。每个旗帜可以有无限的组合部分，每个部分从上到下依次显示。

![BannerMeta 示例](https://user-images.githubusercontent.com/1917406/63939958-5f891000-ca60-11e9-8025-32808f018757.png)

## 基础颜色

底色是创建旗帜要做的第一件事，通过RGB的形式设置底色。底色会显示在所有其他之下。

在1.13版本及以上，你不需要特地指定一个底色，因为旗帜默认已经有底色了。

## 样式
样式是在底色之后要加上的。内容是一个方位后加上一个颜色。
[具体的例子可以在这里找到](https://hub.spigotmc.org/javadocs/spigot/org/bukkit/block/banner/PatternType.html)。

一个例子：

```
- BANNER:13 1 basecolor:11685080 SQUARE_TOP_RIGHT:141883391.
```