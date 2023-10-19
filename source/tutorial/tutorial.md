# 服务准备

此处使用Flask构建一个简易后端服务，应对采集所需，生产环境可以搭建更加复杂的后端服务接口。

+ __采集目标接口__

```python
import uuid
from flask import Flask, request, views

app = Flask(__name__)


class ListViews(views.MethodView):
    def get(self):
        return {
            'status': 1,
            'data': ['./detail?id=1', './detail?id=2', './detail?id=3', ],
            'message': 'success'
        }


class DetailViews(views.MethodView):
    def get(self):
        _id = request.args.get('id') or '1'
        return {
            'status': 1,
            'data': {
                'id': _id,
                'url': './detail?id=%s' % _id,
                'title': 'title: %s' % _id,
                'content': 'content: %s' % _id,
            }
        }


app.add_url_rule(
    '/crawler/crawl_dst/list',
    view_func=ListViews.as_view('crawl_dst_list'))
app.add_url_rule(
    '/crawler/crawl_dst/detail',
    view_func=DetailViews.as_view('crawl_dst_detail'))
if __name__ == '__main__':
    app.run(host='0.0.0.0', port=5555)
```

+ __任务获取接口__

```python


class TasksView(views.MethodView):
    def get(self):
        spider_name = request.args.get('spider_name') or 'test'
        count = request.args.get('count') or 1
        return {
            'status': 1,
            'data': [
                {
                    'id': uuid.uuid4(),
                    'spiderName': spider_name,
                    'feedbackEnabled': True,  # 需要反馈
                    'seed': {
                        'startUrl': 'http://127.0.0.1:5555/crawler/crawl_dst/list',
                        'persists': {
                            'file': {'path': './'}  # 本地持久化,
                            'interface': {'url': 'http://127.0.0.1:5555/crawler/data/persist'} # 接口持久化
                        }
                    }
                }
            ]
        }


app.add_url_rule('/crawler/tasks', view_func=TasksView.as_view('tasks'))

```

+ __任务反馈接口__

```python
class TaskStats(views.MethodView):
    def put(self):
        stats = request.json
        for stat in stats:
            print(stat)
        return {
            'status': 1,
            'data': None,
            'message': 'success'
        }


app.add_url_rule(
    '/crawler/task/stats', view_func=TaskStats.as_view('task_stats'))

```

+ __数据推送接口__

```python
class DataPersist(views.MethodView):
    def post(self):
        items = request.json()
        print(items)
        return {
            'status': 1,
            'data': None,
            'message': 'success'
        }

```

# 项目准备

+ __构建项目__

```
scrapy startproject test
cd test
scrapy genspider test test.com
```

+ __设置settings__

```
ROBOTSTXT_OBEY = False
SPIDER_LOADER_CLASS = 'gggspider.spiderloader.SpiderLoader'
```

# 请求解析

+ __设计Item__

```python
# items.py


import scrapy

from gggspider.items import DataItem
from gggifcheck import fields


class PostItem(DataItem):
    id = scrapy.Field(check_filed=fields.StringCheckField())
    title = scrapy.Field(check_filed=fields.StringCheckField())
    url = scrapy.Field(check_filed=fields.StringCheckField())
    content = scrapy.Field(check_field=fields.StringCheckField())
```

+ __编写Spider__

```python
# test.py


import json
import urllib.parse

import scrapy
from gggspider.spiders import Spider
from gggspider.task import attach_task
from test.items import PostItem


class TestSpider(Spider):
    name = 'test'

    @attach_task
    def start_request(self, task):
        yield scrapy.Request(
            url=task['seed']['startUrl'],
            callback=self.parse_list,
        )

    @attach_task
    def parse_list(self, response):
        detail_urls = json.loads(response.text)['data']
        for url in detail_urls:
            yield scrapy.Request(
                url=urllib.parse.urljoin(response.url, url),
                callback=self.parse_detail
            )

    @attach_task
    def parse_detail(self, response):
        data = json.loads(response.text)['data']
        item = PostItem()
        item['id'] = data['id']
        item['title'] = data['title']
        item['url'] = data['url']
        item['content'] = data['content']
        yield item

```

# 数据持久化

+ __本地持久化__ 

根据task中的persists里的file字段进行配置保存本地储存的路径。

+ __接口推送持久化__

根据task中的persists里的interface字段进行配置保存推送接口储存的地址。

+ __配置__
```python
ITEM_PIPELINES = {
    'gggspider.pipelines.persists.datas.file.DatasFilePipeline': 900,
    'gggspider.pipelines.persists.datas.interface.DatasInterfacePersistPipeline': 901,
}
```

# 任务反馈

+ __配置__

根据task中的feedbackEnabled字段来控制是否进行反馈。
```python
# settings.py
TASKS_STATS_SERVICE_URL = 'http://127.0.0.1:5555/crawler/task/stats'
ITEM_PIPELINES = {
    'gggspider.pipelines.tasks.TaskStatsPipeline': 999,  # 收尾操作进行反馈
}
```

# 程序启动

+ __编写启动脚本__

```python
# start_task.py


from gggspider.commands import run

if __name__ == '__main__':
    run.run()

```

+ __启动__

```
python3 start_task.py
```