以下是从ant提取中的less目录结构，用来学习，怎么创建基础css

```
|-- index.less                               引入主题和核心代码  @import './themes/default';   @import './core/index';
|-- index.tsx                                这是一个入口， import './index.less'
|-- v2-compatible-reset.less                 重置系统默认的样式
|-- v2-compatible-reset.tsx
|-- color                                    基础颜色库
|   |-- bezierEasing.less                    创建贝克塞尔曲线的函数
|   |-- colorPalette.less                    引入贝克赛尔曲线和tinycolor颜色处理转换 
|   |-- colors.less                          引入color.less 生成基础的颜色库             
|   |-- tinyColor.less                       tinycolor处理颜色和颜色之间的转换
|-- core
|   |-- base.less
|   |-- iconfont.less
|   |-- index.less                            引入base，mixins，iconfont，和motion文件
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
|   |-- compatibility.less                    提供兼容样式改placeholder
|   |-- iconfont.less
|   |-- index.less                            引入其他mixin
|   |-- motion.less
|   |-- reset.less
|   |-- size.less                             提供快速生成长宽，和同时生成长款的mixins
|-- themes
    |-- default.less                          默认主题
```



