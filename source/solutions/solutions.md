# 任务标准
## task标准
```
{
    'id': '',  # 任务id
    'parentId': '',  # 父任务id
    'type': '',  # 任务类型,普通任务/多媒体下载任务
    'executeType': '',  # 一次性任务/常态化任务
    'status': '',  # 任务状态
    'sourceTasks': [],  # 来源任务
    'spiderId': '',  # 采集器id
    'spiderType': 'test',  # 采集器类别
    'platformName': '',  # 平台名
    'spiderName': 'test',  # 采集器名，spiderType+'/'+platformName
    'spiderManagerName': '',  # 管理者采集器名
    'spiderVersion': '',  # web/pc/api/app
    'duplicateEnabled': True,  # 是否去重
    'feedbackEnabled': False, # 是否需要反馈
    'distributeCount': 3,  # 下发次数
    'currentDistributeCount': 1, # 当前下发次数
    'seed': {},  # 采集种子/信源
    'createTs': '',  # 创建时间
    'updateTs': '',  # 修改时间
    'creator': '',  # 创建者
    'updater': ''  # 修改者
}


```
## seed层标准
```
{
    'channel': '',
    'siteId': '',
    'siteName': '',
    'boardType': '',
    'boardId': '',
    'customBoardId': '',
    'boardName': '',
    'subBoardName': '',
    'boardUrl': '',
    'startUrl': 'https://www.baidu.com',
    "requestKwargs": {
        "className": "",
        "url": "",
        "method": "",
        "headers": {},
        "cookies": {},
        "body": {}
    },
    "fileUrls": [],  # 文件url列表
    "filePaths": [],  # 文件url对应的本地路径列表
    'appends': {},
    'encoding': '',
    'language': '',
    'priority': '',
    'location': '',
    'domain': 'xxx.com',
    'customDomain': '',
    'allowDomains': '',
    'timeFormats': '',
    'crawlTypes': '',
    'crawlPageNum': '',
    'crawlCount': '',
    'crawlDepth': '',  #爬取深度/多级传播深度
    'retryCount': '',
    'delay': '',
    'timeout': '',
    'resources': {},
    'resourceServiceConfigs': {},
    'crawlStartTs': '',
    'crawlEndTs': '',
    'multimediaMarkup': False,  # 文本是否进行多媒体标记
    'multimediaDownloadUnified': True, # 是否使用统一下载（子任务进行spiderName替换为父类）
    'multimediaDownload': {  # 多媒体下载细分控制
        "image": True,
        "video": True,
        "file": True,
        "audio": True,
    },
    'parseConfigOrRules': { },
    },
    'persistConfigs': {
    },
    'spreadEabled':True # 开启多级传播
    'spreadBasis':['user' ] # 多级传播基准
    'spreadBasisSourceTypes':['follow','follower']  # 多级传播基准来源类别
    'spreadCrawlTypes':['user', 'post', 'comment']  # 多级传播采集的类型
}
```
# 多场景启动

# 任务生命周期

# Manager模式

# 多版本共存

# 请求前置/后置处理

# 统一去重

# 资源附加回收

# 第三方请求库插件

# 多媒体下载

# 简单数据治理

# 数据透传

# 数据备份/续传

# 子任务应用

# 数据量统计

# 任务操作

# 种子操作

# 预警操作