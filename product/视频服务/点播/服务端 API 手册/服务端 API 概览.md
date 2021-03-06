### 视频上传
|功能名称|API 名称|描述|
|-|-|-|
|发起上传| [ApplyUpload](/document/product/266/9756)|发起视频文件的上传，获取文件上传到云平台对象存储 COS 的元信息|
|上传文件||将视频（和封面）文件上传|
|确认上传| [CommitUpload](/document/product/266/9757)|确认视频文件（和视频封面文件）的上传，获取文件的播放地址和文件 ID|
|URL 拉取视频上传| [MultiPullVodFile](/document/product/266/7817)|通过用户传递的 URL，从已有的资源库批量拉取视频文件到云平台|
### 视频处理
|功能名称|API 名称|描述|
|-|-|-|
|使用任务流处理视频|	[RunProcedure](/document/product/266/11030)|依照指定的流程参数对视频文件进行处理。目前，具体流程参数需要与云平台点播商定|
|对视频文件进行处理|	[ProcessFile](/document/product/266/9642)|开发者可以通过该接口对单个视频发起多种处理任务|
|视频转码|	[ConvertVodFile](/document/product/266/7822)|依照控制台中的转码配置，对视频文件进行转码|
|视频剪辑|	[ClipVideo](/document/product/266/10156)|将源视频文件按指定偏移时间进行掐头去尾剪切|
|视频拼接|	[ConcatVideo](/document/product/266/7821)|将多个视频拼接成新视频文件，并添加到点播系统中|
|指定时间点截图|	[CreateSnapshotByTimeOffset](/document/product/266/8102)|获取视频文件在一组时间点的截图|
|截取雪碧图|	[CreateImageSprite](/document/product/266/8101)|对视频文件进行截图，生成雪碧图|
### 媒资管理
|功能名称|API 名称|描述|
|-|-|-|
|获取视频信息|	[GetVideoInfo](/document/product/266/8586)|可以获取单个视频的多种信息，也可以指定回包只返回部分信息|
|依照视频名称前缀获取视频信息|	[DescribeVodPlayInfo](/document/product/266/7825)|根据视频名称前缀搜索视频，并返回其播放信息列表|
|依照 VID 查询视频信息|	[DescribeRecordPlayInfo](/document/product/266/8227)|云平台直播、互动直播录制文件会进入点播系统，每个录制文件会有唯一的 video_id（简称 vid）|
|增加视频标签|	[CreateVodTags](/document/product/266/7826)|为视频增加标签|
|删除视频标签|	[DeleteVodTags](/document/product/266/7827)|删除视频的标签|
|删除视频|	[DeleteVodFile](/document/product/266/7838)|删除视频文件|
|修改视频属性|	[ModifyVodInfo](/document/product/266/7828)|修改视频文件的描述信息（包括分类、名称、描述、过期时间等）|
|增加打点信息|	[AddKeyFrameDesc](/document/product/266/14190)|为视频增加打点信息，每个文件最多支持 100 个打点信息。|
|删除打点信息|	[DeleteKeyFrameDesc](/document/product/266/13442)|删除视频的打点信息；支持一次删除单个视频的多个打点信息|
### 视频分类管理
|功能名称|API 名称|描述|
|-|-|-|
|创建视频分类|	[CreateClass](/document/product/266/7812)|用于管理视频文件，增加分类|
|获取视频分类层次信息|	[DescribeAllClass](/document/product/266/7813)|获得当前用户所有的分类层级关系|
|获取视频分类信息|	[DescribeClass](/document/product/266/7814)|获取全局分类列表，以及每个分类的具体信息|
|修改视频分类|	[ModifyClass](/document/product/266/7815)|修改视频分类的属性（包括名称）|
|删除视频分类|	[DeleteClass](/document/product/266/7816)|删除视频分类|
### 事件通知与任务管理
|功能名称|API 名称|描述|
|-|-|-|
|拉取事件通知|	[PullEvent](/document/product/266/7818)|用于从点播服务端获取事件通知|
|确认事件通知|	[ConfirmEvent](/document/product/266/7819)|开发者调用拉取事件通知，获取到事件之后，必须调用该接口来确认消息已经收到|
|查询任务列表|	[GetTaskList](/document/product/266/11722)|查询任务列表，能查询到三天（72小时）内的任务|
|查询任务信息|	[GetTaskInfo](/document/product/266/11724)|用于获取任务的执行情况，只能查询到三天（72小时）内的任务|
|重试任务|	[RedoTask](/document/product/266/11725)|只能重试已结束的三天（72小时）内的任务，执行之后任务ID不会改变，重试成功后会覆盖之前的数据|
### 参数模版管理
|功能名称|API 名称|描述|
|-|-|-|
|创建转码模板|	[CreateTranscodeTemplate](/document/product/266/9910)|创建新的转码模板|
|查询转码模板列表|	[QueryTranscodeTemplateList](/document/product/266/9913)|查询转码模板列表|
|查询转码模板|	[QueryTranscodeTemplate](/document/product/266/9912)|查询转码模板详细信息|
|更新转码模板|	[UpdateTranscodeTemplate](/document/product/266/9911)|更新转码模板|
|删除转码模板|	[DeleteTranscodeTemplate](/document/product/266/9914)|删除转码模板|
### 水印模板管理
|功能名称|API 名称|描述|
|-|-|-|
|申请上传水印文件|	[ApplyUploadWatermark](/document/product/266/11607)|在创建水印模板时，通过该接口获取水印文件的上传 URL|
|创建水印模板|	[CreateWatermarkTemplate](/document/product/266/11599)|创建新的水印模板|
|查询水印模板列表|	[QueryWatermarkTemplateList](/document/product/266/11608)|查询水印模板列表|
|查询水印模板|  [QueryWatermarkTemplate](/document/product/266/11606)|根据水印模板ID，查询水印模板详细信息|
|更新水印模板|	[UpdateWatermarkTemplate](/document/product/266/11605)|更新水印模板|
|删除水印模板|	[DeleteWatermarkTemplate](/document/product/266/11604)|删除水印截图模板|
### 密钥管理
|功能名称|API 名称|描述|
|-|-|-|
|获取视频解密密钥|	[DescribeDrmDataKey](/document/product/266/9643)|用户在视频加密任务处理成功后调用该接口获取视频加密的数据密钥，用户需要自己保存该数据密钥|
### 数据统计
|功能名称|API 名称|描述|
|-|-|-|
|获取存储量|	[DescribeVodStorage](/document/product/266/10012)|获取截止到昨天 23:59:59 的点播计费存储总量|
|获取播放统计数据文件下载地址|	[GetPlayStatLogList](/document/product/266/12624)|查询每天的播放统计文件下载地址|
## 附录
以下接口是已废弃的服务端 API 接口，具体废弃原因请参见对应文档。

|功能名称|API 名称|描述|
|-|-|-|
|获取视频信息|	[DescribeVodPlayUrls](/document/product/266/7824)|获取当前视频的播放信息（包括播放地址、格式、码率、高度、宽度信息）|
|批量获取视频信息|	[DescribeVodInfo](/document/product/266/7823)|根据 FileID 获取视频属性信息（包括名称、标签、创建时间等）|
|依照指定流程处理视频|	[ProcessFileByProcedure](/document/product/266/9045)|依照指定的流程参数对视频文件进行处理，可以指定的处理流程主要有：转码、创建雪碧图截图等。目前，具体流程参数需要与云平台点播商定|
|HLS 视频简单剪切|	[SimpleClipHls](/document/product/266/8859)|将源视频文件按指定偏移时间进行掐头去尾剪切，新生成的视频文件（目标文件）将拥有新的 FileID|
|截图地址设为视频封面|	[DescribeVodCover](/document/product/266/8814)|-|
















