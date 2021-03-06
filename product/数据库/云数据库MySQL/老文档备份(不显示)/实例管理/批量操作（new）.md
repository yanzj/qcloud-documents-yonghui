## 1 批量续费
### 1.1 使用控制台批量续费

Step1.选中一个或多个需要续费的实例，点击“批量续费”操作

![](http://imgcache.tcecqpoc.fsphere.cn/image/mccdn.qcloud.com/img56825d68b83d4.png)

Step2.选择需要续费的时长，确定后进入下一步

![](http://imgcache.tcecqpoc.fsphere.cn/image/mccdn.qcloud.com/img56825d6f7b8c5.png)

Step3.确定订单信息后，点击“确认支付”。

![](http://imgcache.tcecqpoc.fsphere.cn/image/mccdn.qcloud.com/img56825d763f318.png)

Step4.订单支付成功，可继续查看订单，或跳转到管理中心

![](http://imgcache.tcecqpoc.fsphere.cn/image/mccdn.qcloud.com/img56825d7c5d5ea.png)

## 2批量回档

### 2.1 通用说明

用户可以对云平台中的数据库或表进行回档操作。

回档是基于冷备+binlog，可进行实时数据回档。

云数据库回档工具通过定期镜像和实时流水重建，将云数据库或表回档到指定时间，且可以保证所有数据的时间切片一致。

期间原有数据库或表的访问不受影响，回档操作会产生新的数据库或表。回档完后，用户可以看到原来的数据库或表，以及新建的数据库或表。

>注：云数据库不会改动用户的任何数据，因用户个人原因造成的数据损毁可自行回档修复。
>
### 2.2 通过控制台批量回档

Step1.选中一个或多个需要回档的实例，点击”批量回档”

![](http://imgcache.tcecqpoc.fsphere.cn/image/mccdn.qcloud.com/img56825d2d97ec4.png)

Step2.为每个实例指定需要回档的库表

![](http://imgcache.tcecqpoc.fsphere.cn/image/mccdn.qcloud.com/img56825d1ff334a.png)


Step3.指定回档后名称和回档时间，点击”执行回档”。提交成功后会显示云数据库任务列表，可查看回档进度。

![](http://imgcache.tcecqpoc.fsphere.cn/image/mccdn.qcloud.com/img56825d17d8e14.png)

![](http://imgcache.tcecqpoc.fsphere.cn/image/mccdn.qcloud.com/img56825d12ea040.png)

Step4.找到回档实例，点击操作中的”管理”。进入实例页面后，点击“操作日志”，选择“回档日志”，可查看历史回档记录和当前回档进度。

![](http://imgcache.tcecqpoc.fsphere.cn/image/mccdn.qcloud.com/img56825d075c08a.png)

## 3 批量SQL操作

### 3.1 通用说明

本功能可以在选择的多个实例或数据库上执行SQL语句，您可以利用此功能批量创建数据库/表、更改表结构来完成对多个实例的初始化或者变更，使用此功能需要您保证选择的实例的用户名/密码一致。

3.1.1 生成待执行的SQL文件

待执行的SQL文件可以通过下面两种方法生成：
<span style = "color:#F00"> 注：不建议用户手工构造SQL文件，因为手工构造的SQL文件容易有语法、数据等各种错误，从而导致执行操作失败。 </span>
方法一： 使用云数据库数据控制台导出功能（详见：[冷备数据提取](/doc/product/236/冷备数据提取)）导出的文件；

方法二：通过MySQL工具mysqldump导出的数据文件：

（1）使用mysqldump导出的数据文件必须兼容所购买的云数据库MySQL版本的SQL规范，可登录云数据库通过select version();获取相应的MySQL版本信息。

（2）mysqldump导出数据的方式如下：

shell> mysqldump [options] db_name [tbl_name ...]
其中，options为导出选项，db_name为数据库名称，tbl_name为表名称。
更多mysqldump导出数据说明，请参考[MySQL官方手册](http://dev.mysql.com/doc/refman/5.1/en/mysqldump.html)。

3.1.2 待执行SQL文件限制

执行SQL语句的文件总大小不能超过2MB。SQL文件只支持在同一地域内进行复用，在新地域使用时请重新上传文件。

3.1.3 待执行SQL文件数据文件字符集编码问题

1. 云数据库执行SQL文件如果没有指定字符集编码，以云数据库设置的字符集编码执行。
2. 如果执行SQL文件中有指定的字符集编码，则以指定的字符集编码执行。
3. 如果执行SQL文件的字符集编码与云数据库当前字符集编码不同，会造成乱码。
更多字符集编码问题，请参考使用限制#6. 字符集说明。

3.2 使用控制台批量SQL操作

Step1. 选中一个或多个需要SQL操作的实例，点击“批量SQL操作”

![](http://imgcache.tcecqpoc.fsphere.cn/image/mccdn.qcloud.com/img56825e5e779b7.png)

Step2. 选择需要操作的实例或数据库，点击进入下一步

![](http://imgcache.tcecqpoc.fsphere.cn/image/mccdn.qcloud.com/img56825e584c1cb.png)

Step3. 选择SQL文件，若未找到需要的SQL文件，请点击“新增文件”上传。

![](http://imgcache.tcecqpoc.fsphere.cn/image/mccdn.qcloud.com/img56825e4c63c6a.png)

Step4. 确认需要操作的实例或数据库以及SQL文件，确定无误后输入用户名和密码进入下一步

![](http://imgcache.tcecqpoc.fsphere.cn/image/mccdn.qcloud.com/img56825e4227d88.png)

Step5. 操作提交后可查看任务信息，若需要查看任务执行进度。任务完成之前可“取消任务”。

![](http://imgcache.tcecqpoc.fsphere.cn/image/mccdn.qcloud.com/img56825e3723afa.png)


