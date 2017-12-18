##安装微信小程序 SDK
微信小程序监测，只需在utils引入2个js文件并在首页添加一行js代码，即可完成安装。
###1. 安装应用 获取微信小程序 SDK   
进入数极客后台，点击顶部的平台管理下拉框，点击添加应用，填写基本信息，就可获取数极客appkey，下载微信小程序SDK。
###2. 引入微信小程序 SDK  
将压缩包解压放到微信小程序的utils目录下,复制代码:

var dgt = require('./utils/dgt.js');

添加到项目首页对应的js文件的头部。

**a.** requeire中的目录位置仅做参考，具体位置请根据您的项目结构。  
 
如果无法安装代码，请联系您的技术部门同事安装  

###3. 微信小程序的自定义事件
在数极客后台生成代码后，添加到具体触发事件的位置即可，代码例子如下：

var app = getApp();

app.dgt.trackEvent("事件名","参数名","参数值");

app.dgt.trackEvent("事件名",["参数1名","参数2名"......],["参数1值","参数2值"......]);

###4. 微信小程序的自定义用户属性
在数极客后台生成代码后，添加到具体触发属性的位置即可，代码例子如下：

var app = getApp();

app.dgt.trackAttr("属性名","属性值");