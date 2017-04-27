##app端直接圈选指标和维度

可以在集成SDK2.0.0及以上版本的app端直接进行指标和维度的圈选。

###准备工作

请确保已经按照开发文档正确集成 2.0.0 及以上版本的SDK，手机上已经安装集成了SDK的app。


###圈选步骤

####1 登录后台管理页面获取启动圈选的二维码（<http://www.shujike.com>）

![](http://www.shujike.com/docsimg/android_sdk_mark1.png)

![](http://www.shujike.com/docsimg/android_sdk_mark2.png)

####2 启动手机浏览器，扫描后台二维码

扫码成功后会显示以下页面，点击《开始可视化埋点》按钮。

![](http://www.shujike.com/docsimg/android_sdk_h5.png)

####3 进入登录页面

输入账号密码登录成功后启动圈选功能

![](http://www.shujike.com/docsimg/android_sdk_login.png)

####3 启动圈选控制条

![](http://www.shujike.com/docsimg/android_sdk_controller.png)

通过圈选控制条可以打开和关闭圈选功能，在浏览模式下您可以自由操作您的app，当想圈选时，请通过控制条切换为埋点模式，点击圈选位置，打开圈选界面。

控制条可拖动，防止控制条覆盖您需圈选的位置。

注意：登录成功后控制条不出现时，请到设置界面检查是否开启悬浮窗权限。


####4 打开圈选界面，填写相关信息

![](http://www.shujike.com/docsimg/android_sdk_controller.png)

如图：

如果您选择“加入购物车”按钮，就会出现上图中的圈选界面，您可以填入名称，此名称将在分析后台进行展示。

“当前页面” ：只统计当前页面的此元素的点击事件

“全部页面” ：当此和元素出现在多个页面时，您可以选择此项

”当前元素“ ：统计当前点击元素的事件

”当前位置“ ：统计当前元素位置信息，和此元素处于同一位置的元素的点击事件会全部被统计进来

”同类元素“ ：统计和此元素相同类型的元素

选取和填写好相关信息后点击保存按钮，此元素的埋点信息将被发送至服务端，此元素的将被统计并生成报表























