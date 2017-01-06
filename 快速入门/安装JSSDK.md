##开发者API  
为了更好的支持您的全程数据应用场景，数极客支持您对数据的自定义采集（如自定义客户、订单、购物车、事件追踪等）、数据输出及嵌入您的在线应用当中。
##安装JS采集API   
###安装应用 获取JS SDK   
进入数极客后台，点击顶部的平台管理下拉框，点击添加应用，选择需要安装采集API的网站 如下图所示： 
![](http://www.shujike.com/images/buzhou.jpg)  
###引入JS SDK
完成以上步骤后，复制我们提供的检测代码 如下所示：
    
        <script>
           var _dgt = _dgt || [];
               (function () {
                   _dgt.push(['setSiteId', '替换成您的网站ID']);
                   var d = document, g = d.createElement('script'), s = d.getElementsByTagName('script')[0];
                   g.type = 'text/javascript'; g.async = true; g.defer = true;
                   g.src = ('https:' == document.location.protocol ? 'https://' : 'http://') + 'shujike.cn/dgt.js';
                   s.parentNode.insertBefore(g, s);
               })();
         </script> 
           
 1.将以上我们给您提供的JS SDK代码COPY到您网站的 < head >与< /head >之间  
 2.为了采集全量数据，建议您将此代码放到类似于header.tpl，这种全站的页头模板当中  
 * 如果无法安装代码，请联系您的技术部门同时安装  
 
以上代码是异步加载，不会影响您的网站打开速度，您也可以放到网站的< / body >之前 成功引用JS SDK后数极客就会自动采集您网站当日的访客量、注册量以及事件量等信息。
