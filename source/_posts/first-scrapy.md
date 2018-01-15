title: Scrapy爬虫工具入门尝试
date: 2013-05-27 01:08:20
tags: [scrapy, python, coding]
---
[Scrapy](http://scrapy.org/)是一款纯Python爬虫框架，安装使用据说都很方便。作为一个编程白痴，一边看官方文档上手，一边恶补基础概念，遇到问题就用stackoverflow搜索，经过3天折腾终于基本实现了初步的抓取目标：抓取外交部某栏目下的某一篇新闻的所有正文文字，保存到本地。

<!-- more -->

### 目标网页
http://www.fmprc.gov.cn/mfa_chn/wjdt_611265/fyrbt_611275/t1040553.shtml

### 分析xpath

需要抓取的是文章标题、发表日期和正文，对应的xpath是:

**title：**<acronym>//div[@id='title']/h2</acronym>
**date：**<acronym>//div[@class='data']</acronym>
**content：**<acronym>//div[@id='doccontent']</acronym>

（chrome里选择的xpath是<acronym>//[@id="title"]</acronym>，实际上还需要加上**h2**，导致我一开始抓不到标题）

### 爬虫编写

*	首先新建一个项目`$ scrapy startproject fmprc`


*	进入下一层fmprc_crawl目录里编辑items.py，定义需要抓取的内容，新建一个FmprcItem，包含三个目标：

```
from scrapy.item import Item, Field

class FmprcItem(Item):
    title = Field()
    date = Field()
    content = Field()
    pass
```

*	然后打开spiders文件夹，新建一个爬虫文件fmprc_spider.py，编辑：

```
#一开始声明用utf-8好像没用
#-- coding: utf-8 --#

from scrapy.spider import BaseSpider
from scrapy.selector import HtmlXPathSelector
from fmprc_crawl.items import FmprcItem
#最后用了这段指定encoding为utf-8的方法，搜了半天才找到
import sys
reload(sys)
sys.setdefaultencoding('utf-8')

class FmprcSpider(BaseSpider):
    name = "fmprc"
    allowed_domains = ["fmprc.gov.cn"]
    start_urls = ["http://www.fmprc.gov.cn/mfa_chn/wjdt_611265/
fyrbt_611275/t1040553.shtml"]

	def parse(self, response):
    hxs = HtmlXPathSelector(response)
    items = []
    item = FmprcItem()
    item['title'] = hxs.select('//div[@class='view']/h2/text()').extract()
    item['date'] = hxs.select('//div[@id='time']/text()').extract()
    item['content'] = hxs.select('//div[@id='doccontent']//text()').extract()
    #注意这里是'//text'双斜杠才能抓完所有的文本，否则selector会忽视内层tag里的文本
    items.append(item)
    return items 
```

*	最后执行爬虫 `$ scrapy crawl fmprc`

没有错误的话，会返回unicode形式的抓取结果，这不是我想要的，于是需要输出为csv：

`$ scrapy crawl -o 2013515.csv -t csv fmprc`

*参数：`-o` 输出的文件名 `-t` 输出的格式*

虽然输出的结果格式很简陋，至此算是完成了爬虫的第一次尝试。
