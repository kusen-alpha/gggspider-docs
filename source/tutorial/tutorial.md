# 服务准备

此处使用Flask构建一个简易后端服务，应对采集所需，生产环境可以搭建更加复杂的后端服务接口。

1. 采集目标接口

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
    app.run(host='0.0.0.0', port=5000)
```

2. 任务获取接口

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
                    'seed': {
                        'startUrl': 'http://127.0.0.1/crawler/crawl_dst/list'
                    }
                }
            ]
        }


app.add_url_rule('/crawler/tasks', view_func=TasksView.as_view('tasks'))

```

3. 任务反馈接口

```python
class TaskFeedBack(views.MethodView):
    def put(self):
        tid = request.json.get('tid')
        stats = request.json.get('stats')
        print(tid, stats)


app.add_url_rule(
    '/crawler/task/feedback', view_func=TaskFeedBack.as_view('task_feedback'))

```

4. 数据推送接口

```python
class DataPersist(views.MethodView):
    def post(self):
        items = request.json()
        print(items)


app.add_url_rule(
    '/crawler/data/persist', view_func=TaskFeedBack.as_view('data_persist'))

```

# 项目准备

# 请求解析

# 数据持久化

# 任务反馈