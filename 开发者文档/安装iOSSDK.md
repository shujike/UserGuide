##集成IOS SDK  
###1. 集成整备  

####1.1 获取AppKey  

集成数极客SDK之前，您首先需要到数极客官网注册并且添加新应用，获得Appkey。  

####1.2 下载和集成SDK  

1. 官网直接下载SDK;  

2. 进行安装文档的第1.3步;  

####1.3 导入SDK  

按照 以下步骤将SDK导入到您的项目中。  

1. 解压 iOS SDK 压缩文件;  

2. 添加 SjkAgent.h 和 libshujike-sdk-1.0.a 添加到您的 iOS 工程中;  

提醒:  
- 记得勾选 "Copy items if needed"  

####1.4 添加依赖库  

在您的工程项目中添加依赖  

|库名称|说明|  
|:---:|:---:|  
|libz.tbd|用于 zip压缩解压缩的库|  

提醒:  
- 添加项目依赖库的位置在 项目设置target -> 选项卡General -> Linked Frameworks and Libraries  

####1.5 添加编译参数  

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

    //开启SjkAgent调试日志 可以开启日志
    [SjkAgent shareInstance].isLogEnabled = YES;
    //启动SjkAgent
    [SjkAgent startWithAppKey:@"d3deb0f9d3bdded2" appChannel:@"pppp"];
    return YES;
}  
```

###3. 自定义事件统计  

####3.1 自定义事件接口  

在需要统计事件的位置加入以下代码。  

`[SjkAgent postEventevent:@"自定义事件id" dict:“事件属性的Map”];`  

####3.2 自定义事件id获得  

使用自定义事件功能请先登陆数极客官网([http://www.shujike.com](http://www.shujike.com))， “自定义设置->自定义事件” 页面中添加相应的事件id，然后服务器才会对相应的事件请求进行处理。 请在数极客SDK启动之后调用。 

例:  

```
NSDictionary *eventAttMap = @{@"m_Q1":@"1",@"2":@"15",@"d_Q3":@"3"};
[SjkAgent postEventevent:@"yyq" dict:eventAttMap];
```

特别提醒：value 为自定义内容，根据统计需求填写，values 是用来做运算的，一定要设定为数字。 例如您的事件属性是“点击次数” 那么您的value 就应该传 “1”，如果您传的是“2” 在统计事件点击次数时我们会根据value做sum，导致最终统计出的数据是真实数据的2倍。  

例如您的事件属性定义为“商品价格” 你的商品价格可能是 1元，3元，10.1元，那么value 应该传 1，3，10.1  

![](http://www.shujike.com/images/android_guide_event1.png)  

![](http://www.shujike.com/images/android_guide_event3.png)  

![](http://www.shujike.com/images/android_guide_event2.png)  

事件统计结果可在数极客后台查看。  

###4. 自定义属性统计  

####4.1 自定义属性接口  

设置单个属性:  

`[SjkAgent setAttributeValue:@"自定义的属性id" key:@"2"];`  

设置多个属性： 

```
NSDictionary *attributeMap = @{@"自定义的属性id":@"100",@"自定义的属性id":@"101",@"自定义的属性id":@"102"};
[SjkAgent setAttributeDict:attributeMap];
```  

您可以通过添加自定义属性,进行细分分析  

####4.2 自定义属性id获得  

使用自定义属性功能请先登陆数极客官网 （[www.shujike.com](www.shujike.com)）， “自定义设置->自定义属性” 页面中添加相应的事件id，然后服务器才会对相应的事件请求进行处理。 请在数极客SDK初始化（SjkAgent.init(this)）之后调用。  
例:  

`[SjkAgent setAttributeValue:@"vip" key:@"2"];`  

![](http://www.shujike.com/images/android_guide_arg.png)  

![](http://www.shujike.com/images/android_guide_attribute.png)  










