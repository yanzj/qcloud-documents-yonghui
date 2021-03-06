## 1. 接口描述

功能： 直拨 PSTN 获取虚拟中间号（App 使用方发起）    
接口地址： `http://HOST/201511v3/getVirtualNum?id=xxx` 
请求方式：POST  

>**注意：**
>上述接口地址的 id 值测试时由腾讯统一分配

## 2. 参数说明
| 参数名 | 要求 | 备注 | 
|---------|---------|------------|
| appId | 必选 | xxx | 
| requestId | 可选 | session buffer，字符串最大长度不超过 48 字节，该 requestId 在后面回拨请求响应和回调中都会原样返回 | 
| src | 可选 | 主叫号码 | 
| dst | 必选 | 被叫号码 | 
| accreditList | 可选 | {“accreditList”:[“008613631686024”,”008612345678910”]}，主要用于 N-1 场景，号码绑定非共享是独占型，指定了 dst 独占中间号绑定，accreditList 表示这个列表成员可以拨打 dst 绑定的中间号，默认值为空，表示所有号码都可以拨打独占型中间号绑定，最大集合不允许超过 30 个 | 
| assignVirtualNum | 可选 | 指定中间号，如果该中间号已被使用返回绑定失败，如果不带该字段由腾讯侧从号码池里自动分配 | 
| calleeDisplayNum | 可选 | 被叫显号，如果指定了该字段，被叫透传强显该号码，如果该字段为空，被叫默认显虚拟中间号 | 
| record | 可选 | 是否录音，0 表示不录音，1 表示录音。默认为不录音 | 
| cityId | 可选 | 主被叫号码归属地，详见[《腾讯-中间号-城市id.xlsx》](http://imgcache.tcecqpoc.fsphere.cn/image/mc.qcloudimg.com/static/archive/445a5ee035950ed3a5e71068cf972e70/archive.xlsx) | 
| bizId | 可选 | 应用二级业务 ID，bizId 需保证在该 appId 下全局唯一，最大长度不超过 16 个字节。 | 
| maxAllowTime | 可选 | 允许最大通话时间，不填默认为 30 分钟，单位分钟 | 
| maxAssignTime | 可选 | 号码最大绑定时间，不填默认为 24 小时，单位秒 | 
| statusFlag | 可选 | 主叫发起呼叫状态：1 <br/> 被叫发起呼叫状态：256 <br/> 主叫响铃状态：2<br/>  被叫响铃状态：512<br/> 主叫接听状态：4 <br/> 被叫接听状态：1024 <br/>主叫拒绝接听状态：8<br/>  被叫拒绝接听状态：2048 <br/>主叫正常挂机状态：16<br/> 被叫正常挂机状态：4096<br/> 主叫呼叫异常：32<br/>  被叫呼叫异常：8192<br/><br/> 例如：<br/>值为 0：表示所有状态不需要推送 <br/>值为 4：表示只要推送主叫接听状态 <br/>值为 16191：表示所有状态都需要推送（上面所有值和） | 
| statusUrl | 可选 | 状态回调通知地址，正式环境可以配置默认推送地址 | 
| hangupUrl | 可选 | 话单回调通知地址，正式环境可以配置默认推送地址 | 
| recordUrl | 可选 | 录单 URL 回调通知地址，正式环境可以配置默认推送地址 | 


## 3. 返回结果
| 参考值 | 描述 | 
|---------|---------|------------|
| 0 | 成功 | 
| -1 | 版本不支持 | 
| -2 | 参数异常 | 
| -101 | 参数 src 或 dst 号码不符合规则 | 
| -102 | 参数 displayNum 号码不符合规则 | 
| -103 | 参数 statusUrl 或 hangupUrl 或 recordUrl 不符合 URL 规范 | 
| -106 | 指定中间号已绑定，指定绑定失败 | 
| -107 | 分配中间号失败，中间号号码资源不足 | 
| -108 | 复用 bindId 及中间号绑定超过最大允许绑定次数 | 
| -109 | 分配中间号失败，主被叫号码绑定太频繁，如 1 小时内号码绑定超过 30 次 | 
| -111 | accreditList 错误 | 
| -401 | appId 非法 | 
| -402 | uri 不匹配 | 
| -403 | ip 不在白名单 | 
| -423 | 服务器屏蔽此调用（调用方被入侵或者异常操作） | 
| -501 | 平台处理请求异常（业务做容灾处理） | 

| 变量名 | 类型 | 说明 | 
|---------|---------|------------|
| virtualNum | String | 分配的虚拟号 | 
| bindId | String | 双方号码 + 中间号绑定 ID，该 ID 全局唯一 | 
| refNum | String | 分配绑定中间号引用计数 | 
| requestId | String | requestId 原样返回 | 

## 4. 示例
请求示例
```
{
    "appId":"65500", 
    "requestId":"requessstid",
    "src":"0086135xxxxxxxx",
    "dst":"0086135yyyyyyyy",
    "record":"1",
    "maxAllowTime":"31",
    "statusFlag":"16191",
    "statusUrl":"http://test1111111",
    "hangupUrl":"http://test2222222",
    "recordUrl":"http://test3333333",
    "cityId":"0086"
}
```

成功： 
```
{
	"errorCode":"0",
	"virtualNum":"01012345678",
	"requestId":"vultureli123456",
	"bindId":"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
}
```


失败： 
```
{"errorCode":"-1","msg":"version not supported"}
```
