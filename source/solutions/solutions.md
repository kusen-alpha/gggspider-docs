# 任务标准

总结日常采集所需要的一些字段，项目中可根据实际情况进行选择相应字段和类型，这里只是做一个参考。

## task标准

|字段名|   功能    | 是否必须 |        类型        |  默认值   |             备注             |
|:---:|:-------:|:----:|:----------------:|:------:|:--------------------------:|
|id|  任务id   |  是   |    string/int    |||
|parentId|  父任务id  |  否   |    string/int    |  null  |           子任务时设置           |
|type|  任务类型   |  否   |      string      |  text  |   text(普通任务)/file(多媒体下载任务  |
|executeType| 执行任务类型  |  否   |      string      | always |  once(一次性任务)/always(常态化任务) |
|status|  任务状态   |  否   |       int        |   0    |                            |
|sourceTasks|  来源任务   |  否   |      array       |  null  |                            |
|spiderId|  采集器id  |  否   |       int        |  null  |                            |
|spiderType|  采集器类别  |  否   |      string      |  null  |                            |
|platformName|   平台名   |  否   |      string      |  null  |                            |
|spiderName|  采集器名   |  是   |      string      |        | spiderType+'/'+platformName |
|spiderManagerName| 管理者采集器名 |  否   |      string      |  null  |                            |
|spiderVersion|  采集器版本  |  否   |      string      |  null  |                            |
|duplicateEnabled|  是否去重  |  否   |     boolean      | False  |                            |
|feedbackEnabled|  是否需要反馈  |  否   |     boolean      | False  |                            |
|distributeCount|  下发次数  |  否   |       int        |   3    |                            |
|currentDistributeCount|  当前下发次数  |  否   |       int        |   1    |                            |
|createTs|  创建时间  |  否   |       int        |       |           毫秒            |
|updateTs|  修改时间  |  否   |       int        |       |           毫秒            |
|creator|  创建者  |  否   |      string      |       |                       |
|updater|  修改者  |  否   |      string      |       |                       |
|seed|  采集种子/信源  |  是   | object(map/dict) |       |                       |

## seed标准

|            字段名            |               功能               | 是否必须 |        类型        |            默认值             |             备注             |
|:-------------------------:|:------------------------------:|:----:|:----------------:|:--------------------------:|:--------------------------:|
|            id             |            信源/种子id             |  是   |    string/int    |         string/int         ||
|          channel          |              通道号               |  否   |       int        |||
|          siteId           |              网站id              |  否   |    string/int    |||
|         siteName          |              网站名称              |  否   |      string      |||
|         boardType         |              板块类别              |  否   |      string      |||
|          boardId          |              板块id              |  否   |    string/int    |||
|       customBoardId       |            自定义板块id             |  否   |    string/int    |||
|         boardName         |              板块名称              |  否   |      string      |||
|       subBoardName        |             子板块名称              |  否   |      string      |||
|         boardUrl          |             板块url              |  否   |      string      |||
|         startUrl          |             起始url              |  是   |      string      |||=
|       requestKwargs       |             起始请求参数             |  否   | object(map/dict) |||
|         fileUrls          |            文件url列表             |  否   |      array       |||
|         filePaths         |         文件url对应存储路径列表          |  否   |      array       |||
|          appends          |             透传其他参数             |  否   | object(map/dict) |||
|         encoding          |               编码               |  否   |      string      |||
|         language          |               语言               |  否   |      string      |||
|         priority          |              优先级               |  否   |       int        |||
|         location          |               地区               |  否   |      string      |||
|          domain           |               域名               |  否   |      string      |||
|       customDomain        |             自定义域名              |  否   |      string      |||
|       allowDomains        |             允许域名列表             |  否   |      array       |||
|        timeFormats        |            时间解析格式列表            |  否   |      array       |||
|        crawlTypes         |             爬取类别列表             |  否   |      array       |||
|       crawlPageNum        |              爬取页码              |  否   |       int        |||
|        crawlCount         |              爬取数量              |  否   |       int        |||
|        crawlDepth         |              爬取深度              |  否   |       int        |||
|        retryCount         |              重试次数              |  否   |       int        |||
|           delay           |              请求延迟              |  否   |       int        |||
|          timeout          |             请求超时时间             |  否   |       int        |||
|         resources         |              资源信息              |  否   | object(map/dict) |||
|      resourceConfigs      |             资源信息配置             |  否   | object(map/dict) |||
|       crawlStartTs        |            爬取范围起始时间            |  否   |       int        |||
|        crawlEndTs         |            爬取范围结束时间            |  否   |       int        |||
|     multimediaMarkup      |          文本是否进行多媒体标记           |  否   |     boolean      |||
| multimediaDownloadUnified | 是否使用统一下载 |  否   |        boolean          || 统一下载时将spiderName取为默认Spider |
|    multimediaDownload     |           多媒体是否下载配置            |  否   | object(map/dict) |||
|       parseConfigs        |             解析规则配置             |  否   | object(map/dict) |||
|       persistConfigs        |             持久化配置              |  否   | object(map/dict) |||
|       spreadEabled        |            是否开启多级传播            |  否   |     boolean      |||
|       spreadBasis        |             多级传播基准             |  否   |      array       |||
|       spreadBasisSourceTypes        |           多级传播基准来源类别           |  否   |      array       |||
|       spreadCrawlTypes        |           多级传播采集的类型            |  否   |      array       |||

+ __requestKwargs__

```
"requestKwargs": {  # 初始请求参数
        "className": "",
        "url": "",
        "method": "",
        "headers": {},
        "cookies": {},
        "body": {}
    }
```

+ __multimediaDownload__

```
    'multimediaDownload': {  # 多媒体下载细分控制
        "image": True,
        "video": True,
        "file": True,
        "audio": True,
    }
```

# 任务生命周期

## 信源存储

信源/种子，是最原始的采集目标，它们一般是不会或不需要频繁变更的数据，一般保存在结构化数据库中。

信源在表设计时，需要考虑以下几点：

+ 信源优先级，每个优先级的信源的采集周期应该是不一样的，是采集及时性和采集资源的综合考虑下确定的。
+ 信源表的分库分表，由于信源的增加，可能面临着信源表越来越大，影响查询修改效率。

## 任务封装

任务是直接面向采集的，信源和任务是一对多的关系，一个信源在一周采集周期内封装一个任务，然后放入任务队列。

在任务封装时，需要单独有脚本去生成任务，实现方案有以下几种：

+ 实时地查询信源表，将达到采集时间点的信源推送进任务队列，并根据优先级对应的周期修改该信源下一次获取的时间点。
+ 利用定时任务，达到一个时间周期时将对应的优先级所有信源查询出并推送进任务队列。

由于任务队列只是临时的任务数据，当需要一些后续业务的完整性，如统计任务采集情况，就必须将任务再持久化一份。

## 任务队列

任务队列是直接对接采集节点的，封装任务入采集队列是生产者，采集节点消费任务是消费者。

任务队列在设计的时候，需要考虑如下几点：

+ 每个采集平台需要有对应的队列。
+ 每个采集平台的队列数可根据优先级来区分（优先级太对时也需要适当缩减队列数）
+ 根据信源优先级对应的时间周期，进行任务打散,能解决部分风控问题。

## 采集消费

采集节点统一从任务队列中进行消费（可以封装一个统一任务接口），采集节点理论上消费速度要比生产任务高，才不不会导致任务队列积压。

采集消费时需要考虑如下几点：

+ 支持指定采集器任务，因为有一些采集平台特殊或需要单独部署时，需要一对一进行获取任务。
+ 支持混合任务，因为大部分采集节点都是是采集非特殊的采集平台任务。
+ 支持指定采集采集器任务且同时支持混合任务，在单独部署的采集环境里，当指定采集器任务取完后，为了避免服务器空闲，一般可获取混合任务。

## 任务反馈

在任务封装开始，就需要记录任务的状态，如：

+ 任务封装完毕
+ 采集节点获取完毕
+ 采集节点正常采集完毕
+ 采集节点异常采集完毕
+ 采集开发者指定设置任务状态

根据任务状态，为应用层做一些更高级的需求。

# 多场景启动

支持物理机单机、多机部署和容器集群部署。

支持指定采集器任务和混合任务启动。

## 任务接口设计

在生产环境中，一般采集节点是众多的，因此对获取任务的接口需要满足高并发的要求，同时需要应对多场景部署方案提供一些支持，常见的需求有：

+ 指定平台任务
+ 混合任务
+ 指定任务数量

示例：

```python
# flask

@app.route('/crawler/tasks')
def tasks():
    spider_name = request.args.get('spider_name')  # 采集器名，不指定则拿混合任务
    count = request.args.get('count')  # 数量
    spider_count = request.args.get('spider_count')  # 采集器数量
    mixed = request.args.get('mixed')  # 是否支持混合，用于指定采集器名时
    # 获取任务逻辑......
```

## 启动脚本

统一的启动脚本，不同场景启动通过参数来指定，便于生产环境命令部署。

默认提供的脚本如下：

|                   脚本                   | 功能 |说明| 
|:--------------------------------------:|:---:|:---:|
|       gggspider.commands.run.py        | 单进程方式启动 || 
|       gggspider.commands.run.sh        | 单进程方式启动 || 
| gggspider.commands.run_multiprocess.py | 多进程方式启动 || 
| gggspider.commands.run_multiprocess.sh | 多进程方式启动 ||

可选参数有：

|              参数              |    功能     |                 默认值                 |        说明        |
|:----------------------------:|:---------:|:-----------------------------------:|:----------------:|
|         service_url          |   任务接口    | http://127.0.0.1:5555/crawler/tasks ||
|         spider_name          |   采集器名    |                空字符串                 ||
|            count             |    数量     |                  1                  ||
|         spider_count         |   采集器数量   |                  1                  | 即混合任务时获取多少采集器的任务 |
|            mixed             |  是否支持混合   |                False                ||
|            memory            | 最大使用内存阈值  |                 60                  ||
|             cpu              | 最大使用cpu阈值 |                 60                  ||
|           forever            | 是否持续获取任务  |                False                ||

## 部署方案

**物理机部署**

+ 单机部署

将源码放入指定目录，指定启动脚本。

+ 多机部署

可利用批量工具（如ansible）进行批量指定启动脚本。

**容器集群部署**

+ 环境镜像+源码

打包一个环境镜像，启动前进行拉取代码。

+ 源码环境镜像

将源码和环境打包成镜像再启动。

# Manager模式

在采集过程中，有一些零散的、数据量少、任务少的采集平台需求（如小新闻网站）， 这时在采集节点拿到任务时也会整体启动一次项目，这时采集的收益是非常小的
（启动运行代价和采集数据量比例），这时针对这种情况，设计出Manager模式，
即利用Manager来管理多个采集器，也就是只启动一个Manager（本质是Spider），
然后由Manager根据进行代理分发对应Staff采集器里处理逻辑。

manager模式实现步骤：

## 项目配置

```python
STAFF_PREFIX = "staff"  # 默认为staff，文件名规范写法为：STAFF_PREFIX+_平台名.py
SPIDER_LOADER_CLASS = 'gggspider.spiderloader.SpiderLoader'

```

## 项目示例

+ 目录结构

```
├─spiders
    │  │  __init__.py
    │  │
    │  ├─test
    │  │  │  manager.py
    │  │  │  staff_spider1.py
    │  │  │  staff_spider2.py
    │  │  │  __init__.py


```

+ 代码实现

```python

# manager.py
from gggspider.spiders import manager


class ManagerSpider(manager.ManagerSpider):
    name = 'test/manager'


# staff_spider1.py
from gggspider.spiders import Spider
from gggspider.task import attach_task


class StaffSpider1(Spider):
    name = 'test/spider1'

    @attach_task
    def parse(self, response, **kwargs):
        print('response1', response)


# staff_spider2.py
from gggspider.spiders import Spider
from gggspider.task import attach_task


class StaffSpider1(Spider):
    name = 'test/spider2'

    @attach_task
    def parse(self, response, **kwargs):
        print('response2', response)
```

## 任务示例

```python
from gggspider.commands import run


def get_tasks(spider_name, count, spider_count, mixed):
    return [
        {
            "id": "1",
            "spiderName": "test/spider1",
            "spiderManagerName": "test/manager",
            "seed": {
                "startUrl": "https://www.baidu.com"
            }
        },
        {
            "id": "2",
            "spiderName": "test/spider2",
            "spiderManagerName": "test/manager",
            "seed": {
                "startUrl": "https://www.jd.com"
            }
        }
    ]


if __name__ == '__main__':
    run.run(get_tasks_func=get_tasks)


```

# 多版本共存

对于一些大的采集站点，可能有很多种采集方式，比如PC/API/APP等不同平台方式采集、
基于刷新用户/刷新板块/id等采集方式采集，这种情况下，一个采集站点就会有很多版本的采集代码，这时在
下发任务时需要明确指定用哪种采集器进行采集，并且有些时候需要多种版本采集协同完成（比如优先的采集方案不能采集，
需要用其他采集方式进行补充采集），这时就需要采集里实现多版本之间的自动切换（通过子任务或者修改任务里的 采集版本进行重新下发）。

## 配置项目

```python
VERSION_PREFIX = "version"

"""
默认为version，文件名规范写法为下列三种中其中一种：
1、VERSION_PREFIX+_平台名_+spiderVersion.py
2、平台名/VERSION_PREFIX_spiderVersion.py
3、平台名/VERSION_PREFIX_spiderVersion/平台名.py

"""

SPIDER_LOADER_CLASS = 'gggspider.spiderloader.SpiderLoader'

```

## 项目示例

+ 目录结构

```
├─spiders
│  │  test.py
│  │  version_test_v1.py
│  │  version_test_v2.py
│  │  __init__.py

```

+ 代码实现

```python
# test.py
import scrapy
from gggspider import Spider
from gggspider.task import attach_task


class TestSpider(Spider):
    name = "test"

    def parse(self, response):
        print("default", response)


# version_test_v1.py
import scrapy
from gggspider import Spider
from gggspider.task import attach_task


class TestSpider(Spider):
    name = "test"

    def parse(self, response):
        print("v1", response)


# version_test_v2.py
import scrapy
from gggspider import Spider
from gggspider.task import attach_task


class TestSpider(Spider):
    name = "test"

    def parse(self, response):
        print("v2", response)

```

## 任务示例

```python
from gggspider.commands import run


def get_tasks(spider_name, count, spider_count, mixed):
    return [

        {
            "id": "1",
            "spiderName": "test",
            "seed": {
                "startUrl": "https://www.baidu.com"
            }
        },
        {
            "id": "2",
            "spiderName": "test",
            "spiderVersion": "v1",
            "seed": {
                "startUrl": "https://www.jd.com"
            }
        },
        {
            "id": "3",
            "spiderName": "test",
            "spiderVersion": "v2",
            "seed": {
                "startUrl": "https://www.taobao.com"
            }
        }
    ]


if __name__ == '__main__':
    run.run(get_tasks_func=get_tasks)

```

## 版本切换

当一个采集平台有多个版本，面临着多版本协同完成采集目录，如果版本信息是在下发任务时就已经能明确的情况下，
直接在任务里进行指定，但是如果在采集过程中，当前版本未能达到采集目录，需要切换其他版本进行完成采集工作时，
可通过子任务的方式进行将版本名切换，这时需要用到任务相关服务进行操作，采集里进行子任务的发起即可：

```python
# 待测试......
```

# 数据处理

## 数据治理

如果业务层对采集推送的数据有一定的要求，比如字段类型校验、默认值补全、数据格式校验等有要求时， 可以在采集层面进行有些初步治理。

gggspider里利用scapy和gggifcheck能完成这些简单的治理工作，示例:

```python
# items.py
import scrapy
from gggspider.items import DataItem
from gggifcheck import fields


class TestDataItem(DataItem):
    # 治理操作可以参考gggifcheck
    id = scrapy.Field(check_filed=fields.IntegerCheckField(nullable=False))
    author = scrapy.Field(check_filed=fields.StringCheckField(default="张三"))
    content = scrapy.Field(check_filed=fields.StringCheckField())


# spider

import scrapy
from gggspider import Spider
from gggspider.task import attach_task
from xxx.items import TestDataItem


class TestSpider(Spider):
    name = "test"

    @attach_task
    def start_request(self, task):
        yield scrapy.Request(url=task['seed']['startUrl'])

    @attach_task
    def parse(self, response):
        item = TestDataItem()
        item['id'] = 1
        item['content'] = "test"
```

settings配置CheckPipeline进行治理生效:

```python
# settings.py
ITEM_PIPELINES = {
    "gggspider.pipelines.check.CheckPipeline": 100,
    # "gggspider.pipelines.show.ShowPipeline": 101, # 打印
}
```

## 数据透传

在采集数据推送时，有部分数据是通过任务里携带的，包括一些和采集平台相关的以及一些
业务变动临时附加的，这时在采集中手动指定从任务里获取或在Pipeline进行统一获取。

采集里获取示例:

```python

# 解析处示例
@attach_task
def parse(self, response):
    seed = response.meta['task']['seed']
    item = TestDataItem()
    item['site_name'] = seed.get('siteName')
```

在Pipeline里处理示例：

```python
# pipeline处处理

def process_item(self, item, spider):
    task = spider.tasks[item['_tid']]
    seed = task['seed']
    item['site_name'] = seed.get('siteName')
    return item
```

## 数据推送

在gggspider里，默认推荐使用统一数据推送服务接口，来完成批量和统一处理逻辑。

如果需要直接连接数据库等相关逻辑，可以自定义进行完成相关pipeline逻辑。

搭建示例：

```python

import scrapy
from gggspider import Spider
from gggspider.task import attach_task
from xxx.items import TestDataItem


class TestSpider(Spider):
    name = "test"

    @attach_task
    def start_request(self, task):
        yield scrapy.Request(url=task['seed']['startUrl'])

    @attach_task
    def parse(self, response):
        item = TestDataItem()
        item['id'] = 1
        item['author'] = "author"
        item['content'] = "content"
        yield item
```

推送接口服务:

```python
from flask import Flask, views, request


class DatasPersist(views.MethodView):

    def post(self):
        items = request.json
        print(items)
        # TODO 进行持久化处理
        return {
            'status': 1,
            'data': None,
            'message': 'success'
        }


app.add_url_rule('/crawler/persist/datas',
                 view_func=DatasPersist.as_view(name='persist_datas'))
```

采集配置:

```
# settings.py

ITEM_PIPELINES = {
   "gggspider.pipelines.check.CheckPipeline": 100,
   "gggspider.pipelines.persists.datas.interface.PersistPipeline": 101,
}
DATAS_INTERFACE_PERSIST_URL = "http://127.0.0.1:5555/crawler/persist/datas"
DATAS_INTERFACE_PERSIST_CLASSIFIED = True  # 是否分类推送
DATAS_INTERFACE_PERSIST_MAXSIZE = 1  # 批量推送单次最大数量
```

## 数据备份

数据备份接口服务:

```python
from flask import Flask, views, request


class BackupDatasPersist(views.MethodView):

    def get(self):
        _id = request.args.get('id')
        _type = request.args.get('type')
        # TODO 获取备份的数据进行续传
        return {
            'status': 1,
            'data': [{
                'id': '1',
                'author': 'author',
                'content': 'content'
            }],
            'message': 'success'
        }

    def post(self):
        items = request.json
        print(items)
        # TODO 进行持久化处理且生成任务到任务队列(续传也通过任务方式流转)
        return {
            'status': 1,
            'data': None,
            'message': 'success'
        }


app.add_url_rule('/crawler/persist/backup_datas',
                 view_func=BackupDatasPersist.as_view(
                     name='persist_backup_datas'))
```

采集配置:

```
# settings.py

ITEM_PIPELINES = {
   "gggspider.pipelines.persists.datas.interface.BackupPersistPipeline": 102
}
DATAS_BACKUP_INTERFACE_PERSIST_URL = "http://127.0.0.1:5555/crawler/persist/backup_datas"
DATAS_BACKUP_INTERFACE_PERSIST_MAXSIZE = True  # 是否分类推送
DATAS_BACKUP_INTERFACE_PERSIST_CLASSIFIED = 1  # 批量推送单次最大数量
```

## 数据续传

数据续传是将备份的数据重新进行推送，通过接口获取，这时可以抽象为一个采集器进行采集 通过任务的方式进行获取备份数据。

数据续传采集器：

```python
import json

import scrapy
from gggspider import Spider
from gggspider.task import attach_task
from gggspider.items import DataRetransmissionItem


class DatasRetransmissionSpider(Spider):
    name = "datas/retransmission"

    @attach_task
    def start_request(self, task):
        yield scrapy.Request(url=task['seed']['startUrl'])

    @attach_task
    def parse(self, response):
        datas = json.loads(response.text)['data']
        for data in datas:
            item = DataRetransmissionItem()
            item['data'] = data
            item['_type'] = data.get('_type', '')
            yield item
```

任务服务示例：

```python
class BackupDatasPersist(views.MethodView):

    def get(self):
        ids = request.args.get('ids')
        _type = request.args.get('type')
        return {
            'status': 1,
            'data': [{
                '_tid': '1',
                '_type': '',
                'id': '1',
                'author': 'author',
                'content': 'content'
            }],
            'message': 'success'
        }


app.add_url_rule('/crawler/persist/backup_datas',
                 view_func=BackupDatasPersist.as_view(
                     name='persist_backup_datas'))
```

任务启动示例：

```python

from gggspider.commands import run


def get_tasks(spider_name, count, spider_count, mixed):
    return [
        {
            "id": "2",
            "spiderName": "datas/retransmission",
            "seed": {
                "startUrl": "http://127.0.0.1:5555/crawler/persist/backup_datas?ids=1,2",
                "persistConfigs": {
                    "interface": {
                        'url': 'http://127.0.0.1:5555/crawler/persist/datas'}
                }
            }
        },
    ]


if __name__ == '__main__':
    run.run(get_tasks_func=get_tasks)
```

# 任务处理

## 任务操作

## 子任务应用

## 多媒体下载

## 任务反馈

# 信源种子处理

## 信源种子操作

## 信源种子优先级处理

# 预警处理

## 异常规范

## 预警服务

## 第三方组件

# 第三方请求库插件

## urllib

## requests

## 自定插件

# 请求前置/后置处理

## 实现流程

## 统一去重

## 资源附加回收

# 反爬风控处理

## 公共方法

## 频率限制

## 资源限制

## 逆向服务

## 设备绑定

## html渲染
