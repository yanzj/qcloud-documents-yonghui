## 1. 接口描述
本接口(ModifyUserCvmOverview)用于更新开发商各地域cvm的概览信息列表。
接口请求域名：<font style='color:red'>cvm.api.qcloud.com </font>



## 2. 输入参数
以下请求参数列表仅列出了接口请求参数，正式调用时需要加上公共请求参数，见<a href='/doc/api/372/4153' title='公共请求参数'>公共请求参数</a>页面。其中，此接口的Action字段为ModifyUserCvmOverview。

| 参数名称 | 是否必选  | 类型 | 描述 |
|---------|---------|---------|---------|
| cvmOverviews.n (cvmOverviews 为数组，此处入参需要填写数组元素 ) | 是 | String | 更新列表|


## 3. 输出参数
| 参数名称 | 类型 | 描述 |
|---------|---------|---------|
| code | Int | 公共错误码, 0表示成功，其他值表示失败。详见错误码页面的<a href='/document/api/377/4173' title='公共错误码'>公共错误码</a>。|
| message | String | 模块错误信息描述，与接口相关。|
| codeDesc | String | 描述（待补充） |
| data | Array | 描述（待补充） |


## 4. 示例
输入
```
http://cvm.api.qcloud.com/v2/index.php?Action=ModifyUserCvmOverview
&<公共请求参数>
&cvmOverviews.0.regionId=1
&cvmOverviews.0.newFlag=1
&cvmOverviews.0.validCvmNum=100
&cvmOverviews.1.regionId=2
&cvmOverviews.1.newFlag=0
&cvmOverviews.1.validCvmNum=50
```
输出
```
{
    "code":"0",
    "message":"",
    "codeDesc":"Success",
    "data":[
        
    ]
}
```

