# 项目背景

# 项目概述

# 环境搭建

环境安装：

```
pip3 install gggspider
```

# 快速开始

1. 创建一个scrapy项目

```
scrapy startproject test
cd test
scrapy genspider test test.com
```

2. 创建一个Spider

```python

from gggspider.spiders import Spider


class TestSpider(Spider):
    name = 'test'

    def parse(self, response):
        print('response', response)

```

3. 创建启动脚本

```python
# start_task.py


from gggspider.commands import run


def get_task(spider_name, count):
    return [{
        'id': '1',
        'spiderName': 'test',
        'seed': {
            'startUrl': 'https://www.baidu.com'
        }
    }]


run.run(get_tasks_func=get_task)
```

4. 启动

```
python3 start_task.py
```