
# scrapy爬虫笔记

-------


## 1.Scrapy的安装已跳过
-----------
## 2.创建你的第一个爬虫项目

 在创建每一个项目时，你都应该想好你的项目应该放在哪里，即在哪个文件下创建项目，做到文件归档是一个很好的习惯
 创建一个新的爬虫项目命令：```scrapy startproject projectname```

 创建好项目后，你应该了解这个项目都有哪些文件以及struct：```tree projectname```

## 3.编写爬虫的第一步“调试”
在编写爬虫之前，你一定需要知道你想要爬取的网页的URL（网址）和你想要爬取的信息，这是前提。
 创建一个爬虫：```scrapy genspider spidername web```;当然你也可以到项目的spider文件夹下新建一个spidername.py文件，但没必要也没用命令方便，使用命令创建一个爬虫，他会为你初始化一些东西，具体有什么差别大家可以自己实践去体会。
<!--（解释以下创建爬虫项目和创建一个爬虫有什么区别：项目是由Item和若干爬虫构成的，这一点不理解也不重要）-->

这时候再用：```tree projectname```命令你会发现，spider文件夹下多了一个spidername.py文件了。

打开你的spidername.py文件，可以看到如下代码：这是一个爬虫最基本的框架。import语句可以让我们使用scrapy框架中已有的类。然后我们可以看到一些爬虫的参数，比如它的名字和我们允许其爬取的域名。最后是一个空函数parse（）的定义。

![](E:\markdown笔记\scrapy笔记\scrapy笔记图片\spider框架.png)






 在开始编写爬虫之前，我们还需要学会使用response shell 进行调试，这一定会让你事半功倍的。
（1）终端执行命令：```scrapy shell web （web即为你想爬取的网页）```，下面以爬取豆瓣电影top250为例。
（2）输入命令```scrapy shell https://movie.douban.com/top250```
（3）若返回结果中response=200，表明响应成功。

![](E:\markdown笔记\scrapy笔记\scrapy笔记图片\response.png)




（4）接下来我们调试我们想要爬取的信息的位置，例如每部电影的名称所在的位置。
   可通过浏览器的审查元素功能定位到电影名称的Xpath路径（右键copy xpath）。

![copyxpath](E:\markdown笔记\scrapy笔记\scrapy笔记图片\\copyxpath.png)



（5）然后输入命令```response.xpath(”你copy的xpath“)```（直接粘贴）
    回车之后的结果如图：

![xapth调试](E:\markdown笔记\scrapy笔记\scrapy笔记图片\xapth调试.png)

​    如果没出错的话，你已经看到了这部电影的名字已经被我们调试出来了。（说明这个xpath路径是对的）
​    
（6）接下来我们再试试找到每部电影的导演信息的xpath路径。和步骤(4)一样，我们使用审查元素和copyXpath功能来定位到导演信息的xpath路径。

![](E:\markdown笔记\scrapy笔记\scrapy笔记图片\xpath导演.png)

然后输入命令``` response.xpath("你copy的xpath").extract()```回车之后可以看到下面的结果:

![](E:\markdown笔记\scrapy笔记\scrapy笔记图片\xpath导演结果.png)
可见我们已经把导演的信息也提取出来了。这里解释以下```extract()```函数的作用：```extract()```函数是

## 我们需要提取哪些项目（item）
我们需要编辑```items.py```来定义我们需要爬取的项目名:
首先需要导入我们的scrapy库：
```import scrapy```
然后调用scrapy中的Field方法，"Item = scrapy.Field()",具体的item定义如下：
   ``` FilmName = scrapy.Field()```
   ```Director = scrapy.Field()```
   ```Score = scrapy.Field()```
其中FilmName为电影名称，Director为导演，Score为评分。

完整的items.py文件的代码：

```
# -*- coding: utf-8 -*-

# Define here the models for your scraped items

# See documentation in:

# https://doc.scrapy.org/en/latest/topics/items.html

import scrapy
from scrapy.item import Item,Field

class FilmdataItem(scrapy.Item):

    # 电影名

​    FilmName = Field()

    # 导演

​   Director = Field()

    # Score

​    Score = Field()
```




## 正式开始编写爬虫
(1)首先，我们需要给这个爬虫取一个名字作为唯一标识，所以所以我们把```name```属性修改为：
​```name='你的爬虫名字'```

(2)```allowed_domains```属性描述的是允许爬虫爬取的域名，这里我们爬取的域名为 
[movie.douban.com]()，所以修改```allowed_domains```属性为：
​```allowed_domains='movie.douban.com'```

(3)```start_urls```表示你开始爬取的起始网址，所以我们需要设置起始网页为：
​```start_urls='https://movie.douban.com/top250'```

(4)实现页面解析函数，即```parse()```函数,实现parse()函数的过程可以理解为，把我们之前用```response.xpath().extract()```进行调试的结果返回(return)给我的Item。既然要在parse()函数中返回item，那么我们就需要从刚才定义的items.py文件中导入FilmdataItem类：```from ..items import FilmdataItem```。然后将FilmdataItem类实例化为一个Item对象：```Item = FilmdataItem()```。这就是定义parse函数的基本思路了。
完整的spider.py文件的代码：
```
import scrapy
from scrapy import Request
from filmdata.items import FilmdataItem


class FilmsSpider(scrapy.Spider):
    name = 'films'
    allowed_domains = ['douban.com']
    start_urls = ['https://book.douban.com/tag/小说?start=0&type=T']
    def parse(self, response):
        item = FilmdataItem()
         # 电影名
        item['FilmName'] = response.xpath()
            
        # 导演
        item['Director'] = response.xpath()

        # 评分
        item['Score'] = response.xpath()
        yield item
```















```

```