##集成Android SDK 
###1.集成准备

1.1获取AppKey

集成数极客SDK之前，您首先需要到数极客官网(<http://www.shujike.com>)注册并且添加新应用，获得Appkey。

1.2 下载和集成SDK

[官网](http://www.shujike.com)直接下载。

Eclipse 集成 ：

将下载好的jar包放入工程的 libs 目录下，在Eclipse中右键工程根目录，选择Properties -> Java Build Path -> Libraries，然后点击Add External JARs... 选择指向jar的路径，点击OK，即导入成功（ADT17及以上不需要手动导入）。

Android studio 集成 ：

将下载好的jar包放入工程的 libs 目录下，之后在gradle中添加依赖。在项目的build.gradle 中添加如下代码


    dependencies {

    ......

    compile files('libs/shujike-sdk-1.0.jar')

    ......

    }

之后clean project 即导入成功。

###2.基础功能集成

2.1 配置AppKey 

在AndroidManifest.xml 中配置Appkey，代码如下：
![](http://www.shujike.com/images/android_guide_appkey.png)

2.2 添加权限

SDK所需权限如下：

![](http://www.shujike.com/images/android_guide_permis.png)

    <uses-permission android:name="android.permission.INTERNET" />
    <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
    <uses-permission android:name="android.permission.READ_PHONE_STATE" />
    <uses-permission android:name="android.permission.CHANGE_WIFI_STATE" />
    <uses-permission android:name="android.permission.WAKE_LOCK" />
    <uses-permission android:name="android.permission.READ_LOGS" />
    <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
    <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
    <uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
    <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />

在build.gradle 中配置 targetSdkVersion=x(x<23)  可跳过权限检测。

2.3 在application初始化时调用 SjkAgent.init(this)。 至此SDK 初始化已经完毕。

###3.自定义事件统计

3.1自定义事件接口：

在需要统计事件的位置加入以下代码。

    SjkAgent.postEvent(SampleActivity.this, "自定义事件id", “事件属性的Map”);

3.2自定义事件id获得：

使用自定义事件功能请先登陆数极客官网(<http://www.shujike.com>)， “自定义设置->自定义事件” 页面中添加相应的事件id，然后服务器才会对相应的事件请求进行处理。
请在数极客SDK初始化（SjkAgent.init(this)）之后调用。

例：

    HashMap<String, String> eventAttMap = new HashMap<String, String>();
    eventAttMap.put("m_Q1", "1"); 
    eventAttMap.put("m_Q2", "2");
    eventAttMap.put("d_Q3", "3");
    SjkAgent.postEvent(SampleActivity.this, "yyq", eventAttMap);


特别提醒：value 为自定义内容，根据统计需求填写，values 是用来做运算的，一定要设定为数字。
例如您的事件属性是“点击次数” 那么您的value 就应该传 “1”，如果您传的是“2” 在统计事件点击次数时我们会根据value做sum，导致最终统计出的数据是真实数据的2倍。
例如您的事件属性定义为“商品价格”  你的商品价格可能是 1元，3元，10.1元，那么value 应该传 1，3，10.1

![](http://www.shujike.com/images/android_guide_event1.png)

![](http://www.shujike.com/images/android_guide_event3.png)

![](http://www.shujike.com/images/android_guide_event2.png)

3.3事件统计结果可在数极客后台查看。

###4.自定义属性统计

4.1自定义属性接口：

设置单个属性：

    SjkAgent.setAttribute(SampleActivity.this, "自定义的属性id", "2");

设置多个属性：

    HashMap<String, String> attributeMap = new HashMap<>();
    attributeMap.put("自定义的属性id", "100");
    attributeMap.put("自定义的属性id", "101");
    attributeMap.put("自定义的属性id", "102");
    SjkAgent.setAttribute(SampleActivity.this, attributeMap);


您可以通过添加自定义属性,进行细分分析

4.2自定义属性id获得：

使用自定义属性功能请先登陆数极客官网 （www.shujike.com）， “自定义设置->自定义属性” 页面中添加相应的事件id，然后服务器才会对相应的事件请求进行处理。
请在数极客SDK初始化（SjkAgent.init(this)）之后调用。

例：

    SjkAgent.setAttribute(SampleActivity.this, "vip", "2");

![](http://www.shujike.com/images/android_guide_arg.png)
![](http://www.shujike.com/images/android_guide_attribute.png)


###5.调试模式
在SDK初始化时可以设置debug模式，此模式下可查看SDK log 。代码如下

    SjkAgent.setDebugEnabled(true);
    SjkAgent.init(this);

###6.页面访问统计
在每个Activity的onResume方法中调用 SjkAgent.onResume(this); onPause方法中调用 SjkAgent.onPause(this);
![](http://www.shujike.com/images/android_guide_page.png)

###7.按用户ID统计

用户登录后调用

    SjkAgent.bindUserId(context, id); //id为用户唯一标识。

实现用户留存和活跃分析等。

###8.技术支持  

发现问题可联系我公司客服或技术人员进行解答。



