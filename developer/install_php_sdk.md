##集成php SDK 
###1.集成SDK的准备工作

1.1获取AppKey

集成数极客SDK之前，您首先需要到数极客官网(<http://www.shujike.com>)注册并且添加新应用，获得Appkey。

1.2 下载相关lib

[点击下载SDK](http://www.shujike.com/download/SjkAgent-php-SDK.zip)。

###2.php安装c扩展步骤

2.1 解压sdk包,获得shujike.so 文件，将该文件放入PHP的扩展目录下

例如：
    
    mv shujike.so /usr/local/lib/php/extensions/no-debug-non-zts-20131226/

2.2 配置php.ini

    //add the following statement into your php.ini
    extension=shujike.so

2.3 检查c扩展安装情况

    //testify if shujike extension works, if you get the following information, it is done.
    php -i | grep shujike
    
    shujike
    shujike support => enabled




2.4 使用Demo

创建array 传入需要统计的key和value

    $a = array(
        'appKey'=>'aabbccddeeff1122',
        'appChannel'=>'channelId',
        'sessionId'=>'101',
        'visitType'=>'1',
        'eventType'=>'click',
            .
            .
            .
        'utm'=>'');
        
    postEvent($a,"8.8.8.8",4);

您可以随时通过以下方法进行key value 的替换和删除

    $a['utm'] = 'abc'; 
    unset($a['utm']);


以下为详细的key value 对照表
            
    sessionId = "";//会话id
    eventType = "";//事件类型
    currentUrl = "";//当前页面（当前页面url）
    onlineTimes = "";//页面停留时间 （单位毫秒 如 29088）
    visitorType = "";//1-新用户，0-老用户
    appChannel = "";//渠道id（如 baidu，yingyongbao）
    deviceType = "";//设备类型 （如 Phone，Tablet）
    deviceName = "";//设备型号名称（如 小米 红米4）
    deviceBrand = "";//设备厂商 （小米）
    appVersion = "";//app 版本（如 v1.0.1）
    ua = "";//ua信息
    resolution = "";//屏幕分辨率 （如1920x1080）
    networkType = "";//网络类型（1：2g，2：3g，3：4g，4：wifi，5：未知）
    cookiePlugin = "";//是否支持cookie（1：支持，0：不支持）
    directorPlugin = "";//是否支持director插件（1：支持，0：不支持）
    flashPlugin = "";//是否支持flash插件（1：支持，0：不支持）
    gearsPlugin = "";//是否支持gears插件（1：支持，0：不支持）
    javaPlugin = "";//是否支持javaPlugin插件（1：支持，0：不支持）
    pdfPlugin = "";//是否支持pdfPlugin插件（1：支持，0：不支持）
    quicktimePlugin = "";//是否支持quicktimePlugin插件（1：支持，0：不支持）
    realplayerPlugin = "";//是否支持realplayerPlugin插件（1：支持，0：不支持）
    silverlightPlugin = "";//是否支持silverlightPlugin插件（1：支持，0：不支持）
    windowsmediaPlugin = "";//是否支持windowsmediaPlugin插件（1：支持，0：不支持）
    loadTime = "";//页面加载时间
    longitude = "";//经度（如 127.386848）
    latitude = "";//纬度（如 49.159826）
    frequency = "";//session浏览次数（如 1，2）
    browserEngine = "";//浏览器引擎
    browserName = "";//浏览器名称
    browserVersion = "";//浏览器版本
    registerTime = "";//注册时间
    registerRegion = "";//注册地点
    innerReferUrl = "";//站内跳转的refer_url
    firstReferUrl = "";//最早一次referurl
    firstAccessTime = "";//	首次访问时间（如 2017-08-17）
    utm = "";//utm信息




事件发送：

    postEvent($a,"8.8.8.8",4)

第一个参数：为事件的所有统计信息的array

第二个参数：为客户端ip，用于统计客户端位置信息

第三个参数：tp为平台参数，用来区分平台（ 1-WEB,2-H5,3-IOS,4-ANDROID,5-WEIXIN）



###3.自定义事件统计

3.1 自定义事件id获得：

使用自定义事件功能请先登陆数极客官网(<http://www.shujike.com>)， “自定义设置->自定义事件” 页面中添加相应的事件id，然后服务器才会对相应的事件请求进行处理。

例：

    $a = array(
        'appKey'=>'aabbccddeeff1122',
        'appChannel'=>'channelId',
        'sessionId'=>'101',
        'visitType'=>'1',
        'eventType'=>'yyq',
            .
            .
            .
        'm_Q1'=>'1',
        'm_Q2'=>'2',
        'm_Q3'=>'3',
        'utm'=>'');
        
        postEvent($a,"8.8.8.8",4);


特别提醒：value 为自定义内容，根据统计需求填写，values 是用来做运算的，一定要设定为数字。
例如您的事件属性是“点击次数” 那么您的value 就应该传 “1”，如果您传的是“2” 在统计事件点击次数时我们会根据value做sum，导致最终统计出的数据是真实数据的2倍。
例如您的事件属性定义为“商品价格”  你的商品价格可能是 1元，3元，10.1元，那么value 应该传 1，3，10.1

![](http://www.shujike.com/docsimg/android_guide_event1.png)

![](http://www.shujike.com/docsimg/android_guide_event3.png)

![](http://www.shujike.com/docsimg/android_guide_event2.png)

3.2 事件统计结果可在数极客后台查看。

###4.自定义属性统计

4.1 自定义属性id获得：

使用自定义属性功能请先登陆数极客官网 （www.shujike.com）， “自定义设置->自定义属性” 页面中添加相应的事件id，然后服务器才会对相应的事件请求进行处理。

例：

    $a = array(
        'appKey'=>'aabbccddeeff1122',
        'appChannel'=>'channelId',
        'sessionId'=>'101',
        'visitType'=>'1',
        'eventType'=>'click',
            .
            .
            .
        'attributeId1'=>'100',
        'attributeId2'=>'101',
        'attributeId3'=>'102',
        'utm'=>'');

        postEvent($a,"8.8.8.8",4);
        

属性被定义以后所有的事件都会带上相关属性，当属性值发生改变时请重新设置属性值。

![](http://www.shujike.com/docsimg/android_guide_arg.png)
![](http://www.shujike.com/docsimg/android_guide_attribute.png)


###5.绑定用户信息

例：

    $a = array(
        'appKey'=>'aabbccddeeff1122',
        'appChannel'=>'channelId',
        'sessionId'=>'101',
        'visitType'=>'1',
        'eventType'=>'click',
            .
            .
            .
        'userId'=>'123456',
        'userRegisterUrl'=>'shujike',
        'userGender'=>'男',
        'userAge'=>'25',
        'userType'=>'管理',
        'userLevel'=>'5级',
        'userProvince'=>'天津',
        'userCity'=>'东丽区',
            .
            .
            .
        'utm'=>'');
        
        postEvent($a,"8.8.8.8",4);

    

###6.技术支持  

发现问题可联系我公司客服或技术人员进行解答。



