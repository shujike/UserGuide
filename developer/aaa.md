##dga平台API调用示例（SaaS平台版） 
###1.生成Oauth Secret  
在 /manage_app 页面选定要查看数据所属的应用，以“数极客”为例，appKey = '8dea3eba4ea2018e' 点击“生成Oauth Secret”按钮，获取secretKey=
‘882109bca55d4e28ad8ff9c564897e63’    
*注*：    
**a.** secretKey不会保存，每次动态生成，关闭获取窗口后不会再展示，请妥善保存，如果忘记或丢失请重新生成     
**b.** 调用域名为http://a.shujike.com/    
###2.申请oauth access_token  
shell 调用接口：	
curl -d 'client_id=d3deb0f9d3bdded2&client_secret=3d66561de55ca0c7e376ef7b0a344fc3&grant_type=client_credentials&scope=basic
' http://a.shujike.com/api/oauth/clientCredentials  
clientid字段即appKey,clientsecret字段对应第一步生成的secretKey，后面的grant_type和scope参数保留默认值不变即可  
返回结果：  
{"access_token":"b86daeaec59f840bd0249e2cc0ebcd5d11c30fdc","expires_in":3600,"token_type":"Bearer","scope":"basic"}    
//获取accesstoken成功 该token有效期1小时，有效期内可以用于调用数据接口，过期后需要重新进行步骤二生成新的accesstoken  
###3.调用数据接口  
以获取 事件分析——SEM日报 的表格数据为例  
shell 调用接口：  
curl -d 'access_token=b86daeaec59f840bd0249e2cc0ebcd5d11c30fdc&events[0][name]=注册成功-后台&events[0][fe_name]=0008RegisterSu
ccess&events[0][metrics][0][name]=unique_event&events[0][metrics][0][op]=&events[1][name]=发包-审核有效-后台&events[1][fe_name
]=0007ValidPublishOrder&events[1][metrics][0][name]=m_success&events[1][metrics][0][op]=SUM&events[1][metrics][1][name]=m_or
der_price&events[1][metrics][1][op]=SUM&events[2][name]=合同签订-后台&events[2][fe_name]=0007ContractSignServer&events[2][metr
ics][0][name]=m_success&events[2][metrics][0][op]=SUM&events[2][metrics][1][name]=m_sign_price&events[2][metrics][1][op]=SUM
&dimensions[]=ak2&dimensions[]=ak9&dimensions[]=ak1&predicates[0][values][]=-&predicates[0][op]=like&predicates[0][name]=ak2
&predicates[1][values][]=3400.0&predicates[1][op]=like&predicates[1][name]=ak9&relation=or&granularity=hour&time_range[]=201
7-11-07&time_range[]=2017-11-07' http://a.shujike.com/api/source/calculate_grid  

更多参考示例(<http://api.shujike.com/v1.0/doc/>)

