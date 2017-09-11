##集成java SDK 
###1.集成SDK的准备工作

1.1获取AppKey

集成数极客SDK之前，您首先需要到数极客官网(<http://www.shujike.com>)注册并且添加新应用，获得Appkey。

1.2 下载相关SDK

[点击下载SDK](http://www.shujike.com/download/SjkAgent-Java-SDK.zip)。

###2.集成SDK

####2.1 导入所需的jar包

    SjkAgent-Java-SDK.zip

####2.2 初始化 SDK

在程序入口处（如 public static void main(String[] args) 方法中）,初始化 Java SDK 实例。

初始化SDK有以下两种方式

    SjkAgent sjkAgent = new SjkAgent("b4f883e91856dde3");//参数为appKey
    SjkAgent sjkAgent = new SjkAgent("b4f883e91856dde3", "channelId");//参数为appKey和channelId

如果你想要统计渠道来源 请用第二种方式初始化

####2.3 使用Demo



    SjkAgent sjkAgent = new SjkAgent("aabbccddeeff1122", "channelId");
    sjkAgent.setDebugEnabled(true);
    
    //设置公共属性
    HashMap<String, String> defaultAttributeMap = new HashMap<>();
    defaultAttributeMap.put("appChannel", "channelId");
    defaultAttributeMap.put("sessionId", "101");
    defaultAttributeMap.put("visitType", "1");
                .
                .
                .
    sjkAgent.setDefaultAttribute(defaultAttributeMap);

    //设置自定义属性
    sjkAgent.setAttribute("attributeId", "2");
    
    HashMap<String, String> attributeMap = new HashMap<>();
    attributeMap.put("attributeId1", "100");
    attributeMap.put("attributeId2", "101");
    attributeMap.put("attributeId3", "102");
    sjkAgent.setAttribute(attributeMap);
    
    //设置用户信息
    UserBean userBean = new UserBean();
    userBean.setUserId("123456");
    userBean.setUserRegisterChannel("shujike");
    userBean.setUserSex("男");
    userBean.setUserAge("25");
    userBean.setUserType("管理");
    userBean.setUserLevel("5级");
    userBean.setUserProvince("天津");
    userBean.setUserCity("东丽区");
    sjkAgent.bindUserInfo(userBean);
    
    //设置自定义事件
    HashMap<String, String> eventAttMap = new HashMap<String, String>();
    eventAttMap.put("m_Q1", "1");
    eventAttMap.put("m_Q2", "2");
    eventAttMap.put("d_Q3", "3");
    eventAttMap.put("ea_Q3", "4");

    //tp : 1-web，2-h5，3-ios，4-android，5-weixin小程序
    sjkAgent.postEvent("view", eventAttMap, "1.2.3.4", TpType.IOS);
    //清除所有自定义属性
    sjkAgent.clearAllAttribute();
    //清除所有默认属性
    sjkAgent.clearAllDefaultAttribute();
    sjkAgent.postEvent("click", eventAttMap, "", TpType.ANDROID);



公共属性字段参照：

    sessionId = "";//会话id
    currentUrl = "";//当前页面
    onlineTimes = "";//页面停留时间
    visitorType = "";//1-新，0-老
    appChannel = "";//渠道id
    deviceType = "";//设备类型
    deviceName = "";//设备型号名称
    deviceBrand = "";//设备厂商
    appVersion = "";//app 版本
    ua = "";//ua信息
    resolution = "";//屏幕分辨率
    networkType = "";//屏幕分辨率
    cookiePlugin = "";//是否支持cookie
    directorPlugin = "";//是否支持director插件
    flashPlugin = "";//是否支持flash插件
    gearsPlugin = "";//是否支持gears插件
    javaPlugin = "";//是否支持javaPlugin插件
    pdfPlugin = "";//是否支持pdfPlugin插件
    quicktimePlugin = "";//是否支持quicktimePlugin插件
    realplayerPlugin = "";//是否支持realplayerPlugin插件
    silverlightPlugin = "";//是否支持silverlightPlugin插件
    windowsmediaPlugin = "";//是否支持windowsmediaPlugin插件
    loadTime = "";//页面加载时间
    longitude = "";//经度
    latitude = "";//纬度
    frequency = "";//session浏览次数
    browserEngine = "";//浏览器引擎
    browserName = "";//浏览器名称
    browserVersion = "";//浏览器版本
    registerTime = "";//注册时间
    registerRegion = "";//注册地点
    innerReferUrl = "";//站内跳转的refer_url
    firstReferUrl = "";//最早一次referurl
    firstAccessTime = "";//上一跳URL
    utm = "";//utm信息



事件发送：

postEvent(String eventType, HashMap<String, String> eventAttMap, String ip, TpType tp)) 方法为发送异步请求

第一个参数：为事件id ，在创建自定义事件时自己创建的，具体参考下文 3.1自定义事件接口

第二个参数：为事件属性，在创建自定义事件时自己创建的，和事件id一起创建的，具体参考下文 3.1自定义事件接口

第三个参数：为客户端ip，用于统计客户端位置信息

第四个参数：tp为平台参数，用来区分平台（ WEB,H5,IOS,ANDROID,WEIXIN）

如果您不关系位置和平台您可以传空或者使用  postEvent(String eventType, HashMap<String, String> eventAttMap) 方法，此时tp默认为1，全部归为web平台



###3.自定义事件统计

3.1自定义事件接口：

在需要统计事件的位置加入以下代码。

    //tp : 为区分平台之用，现支持五大平台 WEB,H5,IOS,ANDROID,WEIXIN
    sjkAgent.postEvent("view", eventAttMap, "1.2.3.4", TpType.IOS);

3.2自定义事件id获得：

使用自定义事件功能请先登陆数极客官网(<http://www.shujike.com>)， “自定义设置->自定义事件” 页面中添加相应的事件id，然后服务器才会对相应的事件请求进行处理。
请在数极客SDK初始化（SjkAgent.init(this)）之后调用。

例：

    //设置自定义事件
    HashMap<String, String> eventAttMap = new HashMap<String, String>();
    eventAttMap.put("m_Q1", "1");
    eventAttMap.put("m_Q2", "2");
    eventAttMap.put("d_Q3", "3");
    eventAttMap.put("ea_Q3", "4");
    sjkAgent.postEvent("view", eventAttMap, "1.2.3.4", TpType.IOS);



特别提醒：value 为自定义内容，根据统计需求填写，values 是用来做运算的，一定要设定为数字。
例如您的事件属性是“点击次数” 那么您的value 就应该传 “1”，如果您传的是“2” 在统计事件点击次数时我们会根据value做sum，导致最终统计出的数据是真实数据的2倍。
例如您的事件属性定义为“商品价格”  你的商品价格可能是 1元，3元，10.1元，那么value 应该传 1，3，10.1

![](http://www.shujike.com/docsimg/android_guide_event1.png)

![](http://www.shujike.com/docsimg/android_guide_event3.png)

![](http://www.shujike.com/docsimg/android_guide_event2.png)

3.3事件统计结果可在数极客后台查看。

###4.自定义属性统计

4.1自定义属性接口：

设置单个属性：

    //设置自定义属性
    sjkAgent.setAttribute("attributeId", "2");

设置多个属性：

    HashMap<String, String> attributeMap = new HashMap<>();
    attributeMap.put("attributeId1", "100");
    attributeMap.put("attributeId2", "101");
    attributeMap.put("attributeId3", "102");
    sjkAgent.setAttribute(attributeMap);


您可以通过添加自定义属性,进行细分分析

4.2自定义属性id获得：

使用自定义属性功能请先登陆数极客官网 （www.shujike.com）， “自定义设置->自定义属性” 页面中添加相应的事件id，然后服务器才会对相应的事件请求进行处理。
请在数极客SDK初始化（SjkAgent.init(this)）之后调用。

例：

    sjkAgent.setAttribute("attributeId", "2");

![](http://www.shujike.com/docsimg/android_guide_arg.png)
![](http://www.shujike.com/docsimg/android_guide_attribute.png)


###5.绑定用户信息

例：

 
        UserBean userBean = new UserBean();
        userBean.setUserId("123456");
        userBean.setUserRegisterChannel("shujike");
        userBean.setUserSex("男");
        userBean.setUserAge("25");
        userBean.setUserType("管理");
        userBean.setUserLevel("5级");
        userBean.setUserProvince("天津");
        userBean.setUserCity("东丽区");
        sjkAgent.bindUserInfo(userBean);
  
    

###6.技术支持  

发现问题可联系我公司客服或技术人员进行解答。



