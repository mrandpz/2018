以下是从ant提取中的less目录结构，用来学习，怎么创建基础css

```
|-- index.less                               引入主题和核心代码  @import './themes/default';   @import './core/index';
|-- index.tsx                                这是一个入口， import './index.less'
|-- v2-compatible-reset.less                 重置系统默认的样式
|-- v2-compatible-reset.tsx
|-- color
|   |-- bezierEasing.less
|   |-- colorPalette.less
|   |-- colors.less
|   |-- tinyColor.less
|-- core
|   |-- base.less
|   |-- iconfont.less
|   |-- index.less
|   |-- motion.less
|   |-- motion
|       |-- fade.less
|       |-- move.less
|       |-- other.less
|       |-- slide.less
|       |-- swing.less
|       |-- zoom.less
|-- mixins
|   |-- clearfix.less
|   |-- compatibility.less
|   |-- iconfont.less
|   |-- index.less
|   |-- motion.less
|   |-- reset.less
|   |-- size.less
|-- themes
    |-- default.less
```



