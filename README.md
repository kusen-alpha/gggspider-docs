# 在线文档

[在线文档]<https://gggspider.readthedocs.io/zh_CN/latest/index.html>

# 项目背景
在爬虫开发中，您会发现，一个简单的采集脚本就能快速完成我们的采集需求，但是当您身处一个采集团队中，您会发现，由于采集目标站点的增加，越来越难以管理和部署，难免会重复造轮子和写重复代码，同时在和其他小伙伴开发时，不同的代码规范实现过程，很难进行协同开发和发挥各自的特长，把更多的时间投入到一些场景的攻坚克难中来，并提升整个团队的开发效率和提升整个采集团队每个人的技术能力。

无论我们使用哪种爬虫开发语言，都有一些前人的源码框架来实现，他们把握了整个采集的流程或单独解决某一个问题而提供高效整洁的实现方案，我们不得不佩服他们的架构和代码能力。但是大部分框架都是通用且偏向底层的实现，并不是面向项目和应用层面的，因此我们也需要面向项目和应用层的框架，来提高我们的开发效率。

# 项目概述

gggspider（General General General Spider）通用采集框架，是基于scrapy开源框架为基础，针对日常采集需求提供的一种可行的统一开发规范，尽可能满足日常的采集需求场景，并提供一些公共组件来搭建一个采集生态，让采集开发人员更加简单、规范地开发。

该框架的实现流程和框架设计可用性已经在线上得到了验证，当然还有很多的采集场景需要适配和需要不断地升级迭代来达到尽可能理想的成熟框架。

这里文档说明的技术实现大部分都是基于该框架，但是gggspider只是采集平台的采集框架核心部分，当然它需要一些其他服务的支撑，因此后端能力也需要一定的基础。

如果您对这个框架感兴趣的话，不妨进行下一步学习之旅吧！
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


# 技术交流&商业合作
邮箱：1194542196@qq.com

微信: hu1194542196

github: <https://github.com/kusen-alpha/>