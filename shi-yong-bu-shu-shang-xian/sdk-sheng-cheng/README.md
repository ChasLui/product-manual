# 客户端SDK

飞布以开发者体验优先，为提升开发者procode的效率，根据模板实时生成各语言的SDK，且支持用户自行扩展。

飞布的SDK包含两种类型：服务端钩子SDK和客户端SDK。

* 服务端钩子SDK：生成的代码运行在服务端上，主要用途是钩子开发。
* 客户端SDK：生成调用REST API的客户端SDK，主要运行在浏览器中。

## SDK模板市场

点击状态栏“SDK模板”进入SDK模板页，点击右上角“浏览SDK市场”按钮，可查看当前支持的SDK。选择对应SDK，点击“下载”，即可安装对应SDK。

若未找到所需SDK，可参考“[模板规范](../../er-ci-kai-fa/mo-ban-gui-fan.md)”，结合“[自定义模板](../../er-ci-kai-fa/zi-ding-yi-mo-ban.md)”教程，设计自己的SDK模板。

## SDK管理

系统每次编译都会重新生成模板，对于不想重复生成的模板，关闭即可。

此外，模板的生成位置，相对于项目根目录。可使用`..`设置模板的目录层级。

前往项目目录下的template文件夹，删除对应模板文件，即可卸载已安装的SDK模板。


