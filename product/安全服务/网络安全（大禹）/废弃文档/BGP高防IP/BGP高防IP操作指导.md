## BGP高防IP快速接入（转发目标为非云平台）

登录“大禹网络安全”控制台，在“BGP高防IP”控制页中找到您已经开通的高防IP实例，点击实例ID，进入配置页面
![](http://imgcache.tcecqpoc.fsphere.cn/image/mc.qcloudimg.com/static/img/fd9063bdf1f69cb2f4c5bd73d1764787/image.png)

在“转发规则”配置栏中点击“新建”按钮，新建转发规则。按下图所示，首先选择转发规则（目前支持TCP协议），再填写转发端口（最终想通过高防IP的哪个端口来访问，一般来说跟源站端口是相同的），然后填写源站端口（源站提供服务的真实端口）和源站IP

![](http://imgcache.tcecqpoc.fsphere.cn/image/mc.qcloudimg.com/static/img/86a466a99e39b3a04685644e00d105b7/image.png)

注意：

- 如果一个域名对应多个源站IP，可以都写进去，最多支持20个。不同的源站IP之间英文分号";"分隔；
- 用多个源站之间会以轮询方式做负载均衡；
- 一个高防IP支持配置60条转发规则；

点击“确定”后会生成一条转发规则。

高防IP暂不支持配置七层转发，敬请期待。



