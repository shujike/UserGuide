## 自定义属性  
在应用安装成功并且SDK成功引入到网站之后，就可以开始追踪属性，具体步骤如下： 进入数极客应用后台，点击左侧系统管理，切换到系统管理页面之后点击左侧自定义设置，选择自定义属性，点击右上角新增用户属性，按要求填写完内容点击保存，如下所示： 


<video style="width:800px;height:500px"  src="http://www.shujike.com/docsimg/自定义属性.mp4" controls="controls"></video>

<video id="example_video_1" class="video-js vjs-default-skin vjs-big-play-centered"
  controls preload="auto" width="640" height="264"
  poster="http://www.shujike.com/docsimg/自定义属性.mp4"
  data-setup='{"example_option":true}'>
  ...
</video>

自定义属性添加成功之后，在自定义列表中选择添加的属性，点击右侧[生成代码]， 复制生成的代码到触发此的位置，如:  

        _dgt.push(['trackAttr',['gender22'], ['属性的值']]);

## 自定义事件属性
在用户行为数据分析过程中，用户属性、会话属性可以对所有事件指标进行拆解多维分析。但事件属性就只能拆解所对应的事件指标。比如属性“支付方式”（属性值：支付宝、微信、银联）就只能对 “支付订单”等指标进行拆解分析，而不能拆解“注册”“加入收藏”等指标。  
对于行为数据分析中用事件属性拆解指标的需要，数极客大数据分析系统完全支持按事件属性拆解特定事件进行多维分析。  
### 如何创建事件属性
a.进入自定义设置-事件，选择“新增自定义事件属性”。  
![](http://www.shujike.com/docsimg/事件属性1.png)
b.配置自定义事件属性  
![](http://www.shujike.com/docsimg/事件属性2.png)
配置事件属性参数名：相当于变量名，英文翻译即可。  
事件属性名称：属性的名称即维度名  
事件属性值数量：对属性（维度）的值，比如：微信，微博，QQ为3个，选择“小于等于1000”  
c．配置完成即可按照事件属性对特定指标进行拆解多维分析，比如通过“登录方式”拆解登录事件，分析不同登录方式用户的分布情况。  
![](http://www.shujike.com/docsimg/事件属性3.png)
## 默认属性  
在数极客js-SDK中已提供一些默认的属性，调用时传入指定参数即可，如:  

| 属性名称 | 调用方法 |
| :-------------: |:-------------:|
|用户类型|	_dgt.push(['track_role', '参数值']);|
|用户ID|	_dgt.push(['track_userid', '参数值']);|
|用户注册URL|	_dgt.push(['track_url', '参数值']);|
|用户等级|	_dgt.push(['track_level', '参数值']);|
|性别|	_dgt.push(['track_gender', '参数值']);|
|年龄|	_dgt.push(['track_age', '参数值']);|
|注册省|	_dgt.push(['track_province', '参数值']);|
|注册市|	_dgt.push(['track_city', '参数值']);|

