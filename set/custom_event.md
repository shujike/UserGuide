##自定义事件  
在应用安装成功并且SDK成功引入到网站之后，就可以开始追踪事件，通过灵活的自定义事件采集更精准和全面的数据，实现更精准的业务分析。具体步骤如下：
进入数极客应用后台，点击左侧系统管理，切换到系统管理页面之后点击左侧自定义设置，选择自定义事件，点击右上角添加自定义事件，按要求填写完内容点击保存，如图所示：  
![](http://www.shujike.com/images/event.jpg)   
**事件方法：**调用事件的方法，只能输入字母和数字 如：login  必填  
**事件名称：**事件对应的中文名称  必填  
**事件类型：**分为浏览、交易、轻交互、重交互 必选  
添加自定义事件时，支持添加多个事件参数[参数名称，指标名称，计算方式（ sum | count-distinct ）]
自定义事件添加成功之后，在自定义列表中选择添加的事件，点击右侧[生成代码]，如：
  
          _dgt.push(['trackEvent', 'signup',['d_uid'], ['参数1的值']);  
  
复制生成的代码到触发此事件的位置，如自定义购物事件：  
生成代码：

              <script>
                      _dgt.push(['trackEvent', 'item_buy',['m_price','d_classification'], ['参数1的值','参数2的值']]);
              </script>  
          
将以上代码拷贝都触发item_buy事件的位置，点击返回首页之后点击获客分析下的渠道分析，在指标中选择添加的自定义事件名，选择好事件属性，就可以在下方直观的看到触发事件的访问渠道以及对应事件属性值。如图所示：  
 ![](http://www.shujike.com/images/h5/qudao.png)  

*您可拥有的自定义事件总数由您的版本决定。

## 默认事件
在数极客js-SDK中已提供一些默认的事件，调用时传入指定参数即可，如:  
  
| 事件名称 |	调用方法 |
| :-------------: |:-------------:|
|表单提交成功|	_dgt.push(['track_formsuccess',表单元素]); <br /> 例: _dgt.push(['track_formsuccess',document.getElementById("form")]);|
| 加入收藏|	_dgt.push(['track_favorite_add',[商品id,商品单价,商品折扣单价,spu,sku,一级类目,二级类目,三级类目]]); <br /> 例: _dgt.push(['track_favorite_add',[123456,20,19,'spu','sku','服装','男装','T恤']]);|
| 删除收藏|	_dgt.push(['track_favorite_del',[商品id,商品单价,商品折扣单价,spu,sku,一级类目,二级类目,三级类目]]); <br /> 例: _dgt.push(['track_favorite_del',[123456,20,19,'spu','sku','服装','男装','T恤']]);|
|加入购物车|	_dgt.push(['track_cart_add',[商品id,商品金额,商品折扣金额,商品折扣单价,商品件数,spu,sku,一级类目,二级类目,三级类目]]); <br /> 例: _dgt.push(['track_cart_add',[123456,20,19,8,2,'spu','sku','服装','男装','T恤']]);|
|买家主动删除|	_dgt.push(['track_cart_del',[商品id,商品金额,商品折扣金额,商品折扣单价,商品件数,spu,sku,一级类目,二级类目,三级类目]]); <br /> 例: _dgt.push(['track_cart_del',[123456,20,19,8,2,'spu','sku','服装','男装','T恤']]);|
|购物车结算|	_dgt.push(['track_cart_submit',[商品id,商品金额,商品折扣金额,商品件数,spu,sku,一级类目,二级类目,三级类目]]); <br /> 例: _dgt.push(['track_cart_submit',[123456,20,19,2,'spu','sku','服装','男装','T恤']]);|
|立即购买|	_dgt.push(['track_buy',[商品id,商品金额,商品折扣金额,商品件数,spu,sku,一级类目,二级类目,三级类目]]); <br /> 例: _dgt.push(['track_buy',[123456,20,19,2,'spu','sku','服装','男装','T恤']]);|
|提交订单|	_dgt.push(['track_order_submit',[订单id,订单金额,订单折扣金额,商品件数,运费,spu,sku,一级类目,二级类目,三级类目]]); <br /> 例: _dgt.push(['track_order_submit',[123456,20,19,2,1,'spu','sku','服装','男装','T恤']]);|
|取消订单|	_dgt.push(['track_order_cancel',[订单id,订单金额,订单折扣金额,商品件数,spu,sku,一级类目,二级类目,三级类目]]); <br /> 例: _dgt.push(['track_order_cancel',[123456,20,19,2,'spu','sku','服装','男装','T恤']]);|
|提交订单商品详情|	_dgt.push(['track_order_detail',[订单id,商品id,订单金额,商品单价,商品折扣单价,订单折扣金额,商品件数,spu,sku,一级类目,二级类目,三级类目]]); <br /> 例: _dgt.push(['track_order_detail',[123456,654321,20,19,18,2,'spu','sku','服装','男装','T恤']]);|
|取消订单商品详情|	_dgt.push(['track_order_cancel_detail',[订单id,商品id,订单金额,商品单价,商品折扣单价,订单折扣金额,商品件数,spu,sku,一级类目,二级类目,三级类目]]); <br /> 例: _dgt.push(['track_order_cancel_detail',[123456,654321,20,19,18,2,'spu','sku','服装','男装','T恤']]);|
|支付成功|	_dgt.push(['track_pay_succeed',[订单id,订单金额,订单折扣金额,商品件数,spu,sku,一级类目,二级类目,三级类目]]); <br /> 例: _dgt.push(['track_pay_succeed',[123456,20,19,2,'spu','sku','服装','男装','T恤']]);|
|支付失败|	_dgt.push(['track_pay_fail',[订单id,订单金额,订单折扣金额,商品件数,spu,sku,一级类目,二级类目,三级类目]]); <br /> 例: _dgt.push(['track_pay_fail',[123456,20,19,2,'spu','sku','服装','男装','T恤']]);|
|确认收货|	_dgt.push(['track_receipt_confirm',[订单id,订单金额,订单折扣金额,商品件数,spu,sku,一级类目,二级类目,三级类目]]); <br /> 例: _dgt.push(['track_receipt_confirm',[123456,20,19,2,'spu','sku','服装','男装','T恤']]);|
|申请退货|	_dgt.push(['track_refund_apply',[订单id,订单金额,订单折扣金额,商品件数,spu,sku,一级类目,二级类目,三级类目]]); <br /> 例: _dgt.push(['track_refund_apply',[123456,20,19,2,'spu','sku','服装','男装','T恤']]);|
|提交退货|	_dgt.push(['track_refund_submit',[订单id,订单金额,订单折扣金额,商品件数,spu,sku,一级类目,二级类目,三级类目]]); <br /> 例: _dgt.push(['track_refund_submit',[123456,20,19,2,'spu','sku','服装','男装','T恤']]);|
  
<iframe height=498 width=510 src='http://player.youku.com/embed/XMzI0OTc5NzI2NA==' frameborder=0 'allowfullscreen'></iframe>
