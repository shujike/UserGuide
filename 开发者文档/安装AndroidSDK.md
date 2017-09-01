##集成Android 无埋点SDK 
###1.集成SDK的准备工作

1.1获取AppKey

集成数极客SDK之前，您首先需要到数极客官网(<http://www.shujike.com>)注册并且添加新应用，获得Appkey。

1.2 下载相关SDK

[点击下载SDK](http://www.shujike.com/download/SjkAgent-Android-SDK.zip)。

###2.集成SDK

####2.1 集成所需的jar包

    shujike-android-sdk-2.0.1.aar
    shujike-agent-2.0.0.jar
    ShujikeGradlePlugin-2.0.0.jar

####2.2 集成步骤

![](http://www.shujike.com/docsimg/android_sdk_init.png)


###2.2.1 导入shujike-android-sdk-2.0.0.aar

将下载好的shujike-android-sdk-2.0.0.aar包拷贝到app目录下的libs目录中。

###2.2.2 导入 shujike-agent-2.0.0.jar 和 ShujikeGradlePlugin-2.0.0.jar

在项目下新建一个名为plugin文件夹（名字可以自定义，但是要修改相应的build.gradle文件），将这个两个jar包拷贝进去。

###2.2.3 修改项目目录下的build.gradle文件

为shujike-agent-2.0.0.jar 和 ShujikeGradlePlugin-2.0.0.jar两个jar包添加依赖。

    buildscript {
        repositories {
            jcenter()
        }
        dependencies {
            classpath 'com.android.tools.build:gradle:2.2.2'
            //添加依赖
            classpath fileTree(dir: 'plugin', include: '*.jar')
        }
    }

    allprojects {
        repositories {
            jcenter()
        }
    }

###2.2.4 修改app目录下的build.gradle文件

启动shujikegradleplugin 插件，导入shujike-android-sdk-2.0.1.aar包

    apply plugin: 'com.android.application'
    //启用插件
    apply plugin: 'shujikegradleplugin'

    android {
        compileSdkVersion 23
        buildToolsVersion '23.0.2'
        defaultConfig {
            applicationId "com.shujike.sample"
            minSdkVersion 9
            targetSdkVersion 22
        }
        ......
        ......

    }

    repositories{
        flatDir {
            dirs 'libs'
        }
    }
    dependencies {
        //导入sdk包  (注意修改aar文件名称)
        compile(name: 'shujike-android-sdk-2.0.1', ext: 'aar')
    }


###2.2.5 修改app目录下的build.gradle文件

![](http://www.shujike.com/docsimg/android_sdk_appManifest.png)


scheme内信息为 “sjk.”+appKey
参考以下代码：


    //启动圈选功能需要的
    <intent-filter>
        <data android:scheme="sjk.1c7be246d5a051fb" />
        <action android:name="android.intent.action.VIEW" />
        
        <category android:name="android.intent.category.DEFAULT" />
        <category android:name="android.intent.category.BROWSABLE" />
    </intent-filter>
    
    
    <meta-data
        android:name="SHUJIKE_APPKEY"
        android:value="应用的appKey" />
    
    
    <meta-data
        android:name="SHUJIKE_CHANNEL"
        android:value="应用的渠道ID" />
    


###2.2.6 在app的Application中初始化SDK

    public class MyApplication extends Application {
        @Override
        public void onCreate() {
            SjkAgent.init(this);
            super.onCreate();
        }
    }
    
到此SDK已经初步集成完毕。（如最终测试无法收到数据，请查看 8.注意事项）



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

![](http://www.shujike.com/docsimg/android_guide_event1.png)

![](http://www.shujike.com/docsimg/android_guide_event3.png)

![](http://www.shujike.com/docsimg/android_guide_event2.png)

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
        SjkAgent.bindUserInfo(SampleActivity.this, userBean);
  
    


###6.调试模式

在SDK初始化时可以设置debug模式，此模式下可查看SDK log 。代码如下

SjkAgent.setDebugEnabled(true);
SjkAgent.init(this);  

###7.采集Error数据  

7.1 自动采集奔溃日志，无需特殊配置。 

登录数极客官网后台查看  
例如： 
![](http://www.shujike.com/docsimg/ErrorAndroid.png)  

###8.注意事项

8.1 如果您启用了代码混淆，请在您的 proguard-rules.pro 中添加以下代码：

        -keep class com.shujike.analysis.** {
            *;
        }
        -dontwarn com.shujike.analysis.**

8.2 如果您成功集成SDK后事件发送不成功请尝试在 project 级别的 gradle.properties 中添加如下配置：
        
        android.enableBuildCache=false


8.3 如遇无法启动圈选功能，请确保应用已允许悬浮窗权限。在设置页面允许悬浮窗权限。

8.4 无埋点SDK不支持 Android Studio 的 instant run 特性，使用前需要关闭该特性。

###9.技术支持  

发现问题可联系我公司客服或技术人员进行解答。



