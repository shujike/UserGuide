##集成IOS SDK  
###1.集成整备  
####1.1获取AppKey  
集成数极客SDK之前，您首先需要到数极客官网注册并且添加新应用，获得Appkey。  
####1.2下载和集成SDK  
1.官网直接下载SDK;  
2.进行安装文档的第1.3步;  
####1.3导入SDK  
按照 以下步骤将SDK导入到您的项目中。  
1.解压 iOS SDK 压缩文件;  
2.添加 SjkAgent.h 和 libshujike-sdk-1.0.a 添加到您的 iOS 工程中;  
提醒: 记得勾选 "Copy items if needed"  
####1.4添加依赖库  
在您的工程项目中添加依赖  
|库名称|说明|  
|:---:|:---:|  
|libz.tbd|用于 zip压缩解压缩的库|  
提醒:添加项目依赖库的位置在 项目设置target -> 选项卡General -> Linked Frameworks and Libraries  
####1.5添加编译参数  
在您的工程项目中添加编译参数  
1.找到 Linking 设置  
2.在 Other Linker Flags 中添加 -ObjC 参数，请注意大小写  
提醒：Linking 设置位于 项目设置 target -> 选项卡 Build Settings，左上角选择 All。  




