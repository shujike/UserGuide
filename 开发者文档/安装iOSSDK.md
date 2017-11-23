##集成IOS SDK  
###1. 集成整备  

####1.1 获取AppKey  

集成数极客SDK之前，您首先需要到数极客官网(<http://www.shujike.com>)注册并且添加新应用，获得Appkey  

####1.2 选择SDK安装方式  

#####1. 使用CocoaPods安装  

1. 添加 `pod 'SjkAgent'` 到 Podfile 文件中   

2. 执行 `pod update`   

3. 然后进行安装文档的1.4步  

注：如出现`[!] Unable to find a pod with name, author, summary, or description matching 'SjkAgent'` 警告。
先`pod setup` 然后 `rm ~/Library/Caches/CocoaPods/search_index.json`

#####2. 手动安装
1. [<font color=#dc143f size=16>点击下载SDK</font>](http://www.shujike.com/download/SjkAgent-IOS-SDK.zip) <font color=#dc143f size=18>(最新版本 V2.3.6)</font>   

####1.3 导入SDK  

按照 以下步骤将SDK导入到您的项目中。  

1. 解压 iOS SDK 压缩文件;  

2. 添加 SjkAgent.h 和 libSjkAgent.a、SjkBundle.bundle 添加到您的 iOS 工程中;  

提醒:  
- 记得勾选 "Copy items if needed"   

####1.4 添加编译参数  

在您的工程项目中添加编译参数  

1. 找到 Linking 设置  
2. 在 Other Linker Flags 中添加 -ObjC 参数，请注意大小写  

提醒：  
- Linking 设置位于 项目设置 target -> 选项卡 Build Settings，左上角选择 All。  

###2. 基础功能集成  

####2.1 添加初始化函数  

在 AppDelegate 中引入#import "SjkAgent.h"并添加启动方法  

```
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions { 

    //启动SjkAgent
    [SjkAgent startWithAppKey:@"d3deb0f9d3bdded2" appChannel:@"App Store"];
    //开启SjkAgent调试日志 可以开启日志
    [SjkAgent sharAgent].isLogEnabled = YES;
    return YES;
}  
```
###3. 添加URL Scheme  

把 URL Scheme 添加到您的项目，以便我们唤醒您的程序，进行圈选。

URL Scheme 的格式是 sjk.xxxxxxxxxxxxxxxx(sjk.appkey)。  

1. 添加您的 URL Scheme（sjk.xxxxxxxxxxxxxxxx）到项目中，URL Scheme 位于项目设置 target -> 选项卡 Info -> URL Types。  

2. 在 AppDelegate 中调用函数 [SjkAgent handleUrl:] 来接收 URL。  

```
- (BOOL)application:(UIApplication *)application openURL:(NSURL *)url sourceApplication:(NSString *)sourceApplication annotation:(id)annotation
{
    if ([SjkAgent handleUrl:url])
    {
        return YES;
    }
    ...
    return NO;
}
```  
提醒：  

* 如果您的 AppDelegate 中，实现了其中一个或者多个方法，请在已实现的函数中，调用 [SjkAgent handleUrl:]。  

```
- (BOOL)application:(UIApplication *)application openURL:(NSURL *)url sourceApplication:(nullable NSString *)sourceApplication annotation:(id)annotation
- (BOOL)application:(UIApplication *)application handleOpenURL:(NSURL *)url
- (BOOL)application:(UIApplication *)app openURL:(NSURL *)url options:(NSDictionary<NSString*, id> *)options

```  
* 如果以上所有函数都未实现，则请实现以下方法并调用 [SjkAgent handleUrl:]。  

`- (BOOL)application:(UIApplication *)application openURL:(NSURL *)url sourceApplication:(nullable NSString *)sourceApplication annotation:(id)annotation`  

* 实际情况可能很复杂，请在调试时确保函数 [SjkAgent handleUrl:] 会被执行到。

###4. 自定义事件统计  

####4.1 自定义事件接口  

在需要统计事件的位置加入以下代码。 

设置单个参数:  

`[SjkAgent postEventevent:@"自定义事件id" value:@"m_Q1" key:@"1"];`  

设置多个属性:  

```
NSDictionary *eventAttMap = @{@"m_Q1":@"1",
                              @"m_Q2":@"2",
                              @"d_Q3":@"3"};
[SjkAgent postEventevent:@"自定义事件id" dict:eventAttMap];
```

####4.2 自定义事件id获得  

使用自定义事件功能请先登陆数极客官网([http://www.shujike.com](http://www.shujike.com))， “自定义设置->自定义事件” 页面中添加相应的事件id，然后服务器才会对相应的事件请求进行处理。 请在数极客SDK初始化之后调用。 

例:  

```
NSDictionary *eventAttMap = @{@"m_Q1":@"1",
                              @"m_Q2":@"2",
                              @"d_Q3":@"3"};
[SjkAgent postEventevent:@"yyq" dict:eventAttMap];
```

特别提醒：value 为自定义内容，根据统计需求填写，values 是用来做运算的，一定要设定为数字。 例如您的事件属性是“点击次数” 那么您的value 就应该传 “1”，如果您传的是“2” 在统计事件点击次数时我们会根据value做sum，导致最终统计出的数据是真实数据的2倍。  

例如您的事件属性定义为“商品价格” 你的商品价格可能是 1元，3元，10.1元，那么value 应该传 1，3，10.1  

![](http://www.shujike.com/docsimg/android_guide_event1.png)  

![](http://www.shujike.com/docsimg/android_guide_event3.png)  

![](http://www.shujike.com/docsimg/android_guide_event2.png)  

事件统计结果可在数极客后台查看。  

###5. 自定义属性统计  

####5.1 自定义属性接口  

设置单个属性:  

`[SjkAgent setAttributeValue:@"自定义的属性id" key:@"2"];`  

设置多个属性： 

```
NSDictionary *attributeMap = @{@"自定义的属性id":@"100",
                               @"自定义的属性id":@"101",
                               @"自定义的属性id":@"102"};
[SjkAgent setAttributeDict:attributeMap];
```  

您可以通过添加自定义属性,进行细分分析  

####5.2 自定义属性id获得  

使用自定义属性功能请先登陆数极客官网 （[www.shujike.com](www.shujike.com)）， “自定义设置->自定义属性” 页面中添加相应的事件id，然后服务器才会对相应的事件请求进行处理。 请在数极客SDK初始化之后调用。  
例:  

`[SjkAgent setAttributeValue:@"vip" key:@"2"];`  

![](http://www.shujike.com/docsimg/android_guide_arg.png)  

![](http://www.shujike.com/docsimg/android_guide_attribute.png)  

###6. 自定义用户信息统计  

设置用户信息:  

```
//设置用户信息
UserBean *userBean = [[UserBean alloc]init];
userBean.userId = @"788";
userBean.userRegesterChannel = @"微信";
userBean.userSex = @"男";
....
[SjkAgent bindUserInfo:userBean];  
```
###7. 采集Error数据  

1.自动采集奔溃日志，无需特殊配置。 

登录数极客官网后台查看  
例如：  
![](http://www.shujike.com/docsimg/ErrorIos.png)  

###8.实现APP与H5页面数据打通。  

8.1 为什么要实现APP与H5页面数据打通  
APP嵌套H5混合开发在互联网APP中非常多见。但对有h5嵌套的APP端用户行为分析时，传统用户行为分析平台经常会出现“断档”的情况：  
1.当用户通过APP端跳转到h5页面，APP端采集的用户属性数据不能迁移到h5，导致数据缺失，原生APP只起到了一个浏览器的作用。  
2.APP端贡献给h5的流量，因数据未与APP打通共享，导致APP数据源从根本上出现缺失，造成一定程度上分析决策偏差。  
为了更好的解决APP与h5贯通的问题，数极客研发出APP与h5完全贯通的移动端SDK，顺利解决该问题。  
8.2 场景  
某产品首页上线活动，有多少用户点击跳转到h5页面，有多少用户参加活动，有多少用户真正完成目标事件。在APP与h5贯通的情况下即可以按照用户的设备类型，下载渠道等APP端的用户属性细分进行多维度的细分，研究不同维度活动转化路径的效果的关键影响因素，复盘活动效果，提升活动转化率。  
8.3 使用数极客自动采集H5页面的数据，无需特殊配置。

###9. 注意事项  

* 为了不影响圈选，请设置允许 HTTP 协议请求。  

###10. 技术支持  

如有任何问题可联系我们公司客服或技术人员进行解答。








