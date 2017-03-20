##安装Android SDK 
###1.集成准备

1.1获取AppKey

集成数极客SDK之前，您首先需要到数极客官网注册并且添加新应用，获得Appkey。

1.2 下载和导入SDK

官网直接下载。

###2.基础功能集成

2.1 配置AppKey 

在AndroidManifest.xml 中配置Appkey，代码如下：
![](http://www.shujike.com/images/android_guide_appkey.png)

2.2 添加权限

SDK所需权限如下：

![](http://www.shujike.com/images/android_guide_permis.png)

在build.gradle 中配置 targetSdkVersion=x(x<23)  可跳过权限检测。



###3.自定义事件统计

###4.自定义属性统计

###5.调试模式

###6.技术支持 

