##安装Android SDK 
###1.集成准备

1.1获取AppKey

集成数极客SDK之前，您首先需要到数极客官网（http://www.shujike.com）注册并且添加新应用，获得Appkey。

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

2.3 在application初始化时调用 SjkAgent.init(this)。 至此SDK 初始化已经完毕。

###3.自定义事件统计

3.1自定义事件接口：

SjkAgent.onEvent(SampleActivity.this, "自定义的事件id"); 

在需要统计事件的位置加入此行代码。

3.2自定义事件id获得：

自定义事件id 尽量使用英文或拼音，不建议使用特殊字符或中文，且长度不能超过128个字节；

使用自定义事件功能请先登陆数极客官网 （www.shujike.com）， “自定义设置->自定义事件” 页面中添加相应的事件id，然后服务器才会对相应的事件请求进行处理。
请在数极客SDK初始化（SjkAgent.init(this)）之后调用。
![](http://www.shujike.com/images/android_guide_event1.png)

3.3事件统计结果可在数极客后台查看。

###4.自定义属性统计

4.1自定义属性接口：

SjkAgent.postTags(SampleActivity.this, "自定义的属性id"); 

您可以通过添加自定义用户属性,对用户进行细分分析

4.2自定义属性id获得：

自定义属性id 尽量使用英文或拼音，不建议使用特殊字符或中文，且长度不能超过128个字节；

使用自定义属性功能请先登陆数极客官网 （www.shujike.com）， “自定义设置->自定义属性” 页面中添加相应的事件id，然后服务器才会对相应的事件请求进行处理。
请在数极客SDK初始化（SjkAgent.init(this)）之后调用。
![](http://www.shujike.com/images/android_guide_arg.png)


###5.调试模式
在SDK初始化时可以设置debug模式，此模式下可查看SDK log 。代码如下

        SjkAgent.setDebugEnabled(true);
        SjkAgent.init(this);

###6.页面访问统计
在每个Activity的onResume方法中调用 SjkAgent.onResume(this); onPause方法中调用 SjkAgent.onPause(this);
![](http://www.shujike.com/images/android_guide_page.png)

###7.按用户ID统计

用户登录后调用
SjkAgent.bindUserId(context, id); id为用户唯一标识。

实现用户留存和活跃分析等。

###8.技术支持  

发现问题可联系我公司客服或技术人员进行解答。

