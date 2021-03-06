## 容器镜像服务权限介绍

容器镜像的描述格式是: `ccr.ccs.tencentyun.com/${namespace}/${name}:${tag}`。
镜像仓库的权限围绕以下两个字段进行设置：
* `${namespace}`: 镜像所属命名空间；
* `${name}`: 镜像名字；

>**注意：**
>命名空间 `${namespace}` 及镜像名字 `${name}` 中不能包含斜杠 “ / ”；  
>`${tag}` 字段目前只实现了删除操作鉴权，请参考 [镜像Tag权限](#镜像Tag权限)；

通过`${namespace}`，`${name}`两个字段，开发商可以为协作者制定详细的权限方案，实现灵活的权限管理。  
例如：
* 允许协作者A拉取镜像
* 禁止协作者A删除镜像
* 禁止协作者B拉取命名空间ns1中的镜像
* ...


如果您不需要详细管理镜像仓库权限，可以使用[预设策略授权](#预设策略授权)。  

如果您需要细致地管理协作者权限，请使用[自定义策略授权](#自定义策略授权)。

容器镜像服务权限基于云平台CAM进行管理，您可以详细了解CAM的使用方法：
[用户管理](/document/product/598/10598)，  
[策略管理](/document/product/598/10601)，  
[授权管理](/document/product/598/10602)  

## 预设策略授权

为了简化容器镜像服务权限管理，容器镜像服务内置了两个预设策略:  

* [镜像仓库（CCR）全读写访问权限](http://console.tcecqpoc.fsphere.cn/cam/policy/detail/419082&QcloudCCRFullAccess&2)  

    该预设策略配置了容器镜像服务所有权限，如果协作者关联该预设策略后，将与开发商拥有相同的镜像仓库权限。 详情请查看[权限列表](#权限列表)。  

* [镜像仓库（CCR）只读访问权限](http://console.tcecqpoc.fsphere.cn/cam/policy/detail/419084&QcloudCCRReadOnlyAccess&2)  

    该预设策略包含了容器镜像服务只读操作的权限，如果协作者在容器镜像服务中 **只** 关联了该预设策略，则以下操作将被禁止：  
    * `docker push` 推送镜像
    * 新建镜像仓库命名空间
    * 删除镜像仓库命名空间
    * 创建镜像仓库
    * 删除镜像仓库
    * 删除镜像Tag

如果您不了解如何为协作者关联预设策略，请参考CAM文档： [预设策略介绍](/document/product/598/10601#.E9.A2.84.E8.AE.BE.E7.AD.96.E7.95.A5)、[预设策略关联用户](/document/product/598/10602#.E9.A2.84.E8.AE.BE.E7.AD.96.E7.95.A5.E5.85.B3.E8.81.94.E7.94.A8.E6.88.B7)  

## 自定义策略授权

通过自定义策略，开发商可以为不同的协作者关联不同的权限。  

当您分配权限时，考虑这些要素：  

* **资源(resource)**： 该权限策略关联哪些镜像，例如所有镜像仓库描述为 `qcs::ccr:::repo/*`，详见[CAM资源描述方式](/document/product/598/10606)；  
* **动作(action)**： 该权限策略对 **资源(resource)** 有哪些操作，如删除、新建等，通常使用接口进行描述；
* **效力(effect)** ： 该权限策略对协作者表现出的效果(允许/拒绝)；  

一旦您规划好权限设置，就可以开始进行权限分配。下面我们以“允许协作者创建镜像仓库”为例进行说明：  

1. 创建自定义策略（[CAM文档](/document/product/598/10601#.E8.87.AA.E5.AE.9A.E4.B9.89.E7.AD.96.E7.95.A5))，  

    * 使用开发商账号登录控制台  
    * 进入[CAM自定义策略管理页面](http://console.tcecqpoc.fsphere.cn/cam/policy/custom)，点击“新建自定义策略”按钮打开“选择策略创建方式”对话框  

        ![选择创建策略方式][6]  

    * 选择“按策略语法创建”选项 >> 选择“空白模板”  

        ![选择模板][7]  

    * 点击页面下方“下一步”按钮，进入“按策略语法创建” - “编辑策略” 页面  
    * 在“编辑策略内容”编辑框中填入以下内容，在“策略名称”中填入一个有意义的名字，如 `ccr-policy-demo`  

        ```
        {
            "version": "2.0",
            "statement": [{
                "action": "ccr:CreateRepository",
                "resource": "qcs::ccr:::repo/*",
                "effect": "allow"
            }]
        }
        ```

        ![编辑策略][8]  

        _注: resource **末尾** 使用 \* 表示可以在任意命名空间下创建镜像仓库_  

    * 点击页面底部“创建策略”按钮，结束策略创建过程。  

        ![编辑策略][9]  

2. 关联自定义策略。步骤1中的策略(`ccr-policy-demo` )创建完成以后，您可以将其关联到任意协作者，详见[CAM文档](/document/product/598/10602#.E7.94.A8.E6.88.B7.E5.85.B3.E8.81.94.E8.87.AA.E5.AE.9A.E4.B9.89.E7.AD.96.E7.95.A5)。策略关联完成后协作者即拥有 **在任意命名空间下创建镜像仓库权限**。  


_resource `qcs::ccr:::repo/*` 格式说明_:  

* `qcs::ccr:::` 为固定格式，表示开发商的容器镜像仓库服务；  
* `repo` 为固定前缀，代表资源类型，这里是镜像仓库；  
* 斜杠(`/`)后面的 `*` 表示匹配所有镜像仓库。  

关于resource更详细的描述，请参考[CAM资源描述方式](/document/product/598/10606)  

#### 按资源进行授权

您可以同时为多个资源进行授权。例如：“允许删除命名空间foo, bar中的镜像仓库”，可以创建下面的自定义策略：  

```
{
    "version": "2.0",
    "statement": [{
        "action": [
            "ccr:BatchDeleteRepository",
            "ccr:DeleteRepository"
        ],
        "resource": [
            "qcs::ccr:::repo/foo/*",
            "qcs::ccr:::repo/bar/*"
        ]
        "effect": "allow"
    }]
}
```

_ 注: _
* `qcs::ccr:::repo/foo/*` 中 `foo/*` 表示镜像仓库命名空间 `foo` 下的所有镜像  
* `qcs::ccr:::repo/bar/*` 中 `bar/*` 表示镜像仓库命名空间 `bar` 下的所有镜像  

#### 按动作(接口)进行授权  

您可以对一个资源配置多个`action`，实现资源权限的统一管理。例如：“允许创建、删除、push命名空间foo中的镜像仓库”，可以创建下面的自定义策略：  

```
{
    "version": "2.0",
    "statement": [{
        "action": [
            "ccr:CreateRepository",
            "ccr:BatchDeleteRepository",
            "ccr:DeleteRepository",
            "ccr:push"
        ],
        "resource": "qcs::ccr:::repo/foo/*",
        "effect": "allow"
    }]
}
```

## 权限列表  

#### docker client 权限  

resource： `qcs::ccr:::repo/${namespace}/${name}`    
action：
* `ccr:pull`    使用docker命令行pull镜像  
* `ccr:push`    使用docker命令行push镜像  

#### 命名空间权限

resource： `qcs::ccr:::repo/${namespace}`  
action:
* `ccr:CreateCCRNamespace`     新建镜像仓库命名空间  
* `ccr:DeleteUserNamespace`    删除镜像仓库命名空间  

功能指引: **容器服务** >> 左侧导航栏 **镜像仓库**  >> **我的镜像** >> **命名空间**  
![新建|删除 镜像仓库命名空间权限][1]  


#### 镜像仓库权限

resurce： `qcs::ccr:::repo/${namespace}/${name}`    
action：
* `ccr:CreateRepository`        创建镜像仓库  
* `ccr:DeleteRepository`        删除镜像仓库  
* `ccr:BatchDeleteRepository`   批量删除镜像仓库  
* `ccr:GetUserRepositoryList`  查看镜像仓库列表  

功能指引: **容器服务** >> 左侧导航栏 **镜像仓库**  >> **我的镜像** >> **我的创建**  
![镜像仓库权限][4]  

>**注意：**
>要阻止协作者删除某些镜像，请配置多个 action 来实现。  
例如：禁止删除任何镜像仓库：  
```
{
    "version": "2.0",
    "statement": [{
        "action": [
            "ccr:BatchDeleteRepository",
            "ccr:DeleteRepository"
        ],
        "resource": "qcs::ccr:::repo/*",
        "effect": "deny"
    }]
}
```

#### 镜像Tag权限

resource： `qcs::ccr:::repo/${namespace}/${name}:${tag}`  
action:
* `ccr:DeleteTag`           删除镜像Tag权限

功能指引: **容器服务** >> 左侧导航栏 **镜像仓库**  >> **我的镜像** >> **我的创建** >> 点击某个镜像名称 >> **镜像版本** 页面  
![镜像仓库权限][5]  



[1]:http://imgcache.tcecqpoc.fsphere.cn/image/mc.qcloudimg.com/static/img/1be5647f80dcc50db26cf13ef0e29ce5/1.png
[2]:http://imgcache.tcecqpoc.fsphere.cn/image/mc.qcloudimg.com/static/img/aec6771c2595210d3e4319e6188aafa9/2.png
[3]:http://imgcache.tcecqpoc.fsphere.cn/image/mc.qcloudimg.com/static/img/1d7f13366192079ea3c64d70e46f5215/3.png
[4]:http://imgcache.tcecqpoc.fsphere.cn/image/mc.qcloudimg.com/static/img/99a097e254a9e0e13839d8eaff7b26a8/4.png
[5]:http://imgcache.tcecqpoc.fsphere.cn/image/mc.qcloudimg.com/static/img/3efec02b8ade10fa5c7778820ebdfec3/6.png
[6]:http://imgcache.tcecqpoc.fsphere.cn/image/mc.qcloudimg.com/static/img/224dd2cc5dc809c3220d50ba6497a36e/5.png
[7]:http://imgcache.tcecqpoc.fsphere.cn/image/mc.qcloudimg.com/static/img/daf81fe58cac20aa2c27c65a776288fa/7.png
[8]:http://imgcache.tcecqpoc.fsphere.cn/image/mc.qcloudimg.com/static/img/fb69dccc77754060b713361034acac18/8.png
[9]:http://imgcache.tcecqpoc.fsphere.cn/image/mc.qcloudimg.com/static/img/1492b89bdb394490ab5613a1e06b8987/9.png

