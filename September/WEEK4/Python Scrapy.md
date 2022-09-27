# Web Scraping 

* Extracting Data from a website to our specific folder is called web scraping.
* python program used in this regard is called Spider.
* Also known as web crawling.
* Our python program takes data from website and coverts it to .json file
* ```python import scrapy ```

### How it works:
Spider goes into the source code of website, then it searches for h2 tag in inspect elemts  and finds out the data and stores in database.

### Robot.txt:
* Rules of scraping
* URL/robots.txt
* Scarpy follows these rules
* if you dont want to then go to settsing file and set to false


# Spider proj
www.quotes.toscrape.com

keep scraping speed at 16-32 
bot=automates internet processes

```python

import scrapy
class Quote_spider(scrapy.Spider):
    name = 'quotes' # dont chnage name, start url variables
    start_urls = [
        "https://quotes.toscrape.com/"
    ]

    def parse(self, response):
        title = response.css('title::text').extract() #get title of 
        yield {"Titletext" : title } #dictionary , yield takes you to virtual environment
```
To run type in terminal *Scrapy crawl 'name'*
if it says win32api not found go to avaliable packgaes and download package  or pip install win32

### Xpath
XPath is a language for selecting nodes in XML documents, which can also be used with HTML(not much common)
 
 start with: scarot shell 'url'
```python 
    response.xpath("//title/text()').extract()
    response.xpath("//span[@class='text']/text()')[1].extract()
    response.xpath("//span[@class='text']/text()')[1].extract()
 
```
### CSS
CSS used for syling webiste

in panel write Scarpy Shell 'url'
*Some things seen from HTML Inspect Elemnt*
```python
    response.css("title").extract() # test+tag
    response.css("title::text)[0].extract()   # text only+ 0th element
    response.css("title::text).extract()_first # same thing but better
    response.css("span.text::text).extract()  # got from inspect element , gives all quotes on page 
    response.css("span.text::text)[1].extract() # get only 2nd quote
    
    # download chrome extension selectror generator which gives us a class to see in which class does your obj lie in (.author)
    # after selecting sometimes it shows too extra text so you can click again which will show red box to deselct
    
    response.css(".author::text).extract()
    
    rsponse.css9("li.next a").xpath("@href").extract()
```


# Extracting data, quotes and author
```python
import scrapy
class Quotes_to_scrape(scrapy.Spider):
    name = 'quotes'
    start_urls = [
        "https://quotes.toscrape.com/"
    ]
    def parse(self, response):
            all_div_quotes = response.css('div.quote')
            for quota in all_div_quotes:
                title = quota.css('span.text::text').extract()
                author = quota.css('.author::text').extract()
                tag = quota.css(".tag::text").extract()

                yield {
                    'title' : title,
                    'author' : author,
                    'tag' : tag
                }
```
# Ithem Container
Items are containers used to store data. We can put extracted data directly into our databases but there are some problems. These are temporary locations.

### quotes_spider.py:
```python
import scrapy
from ..items import QuotetItem


class Quotes_to_scrape(scrapy.Spider):
    name = 'quotes'
    start_urls = [
        "https://quotes.toscrape.com/"
    ]
    def parse(self, response):
            items = QuotetItem()
            all_div_quotes = response.css('div.quote')
            for quotes in all_div_quotes:
                title = quotes.css('span.text::text').extract()
                author = quotes.css('.author::text').extract()
                tag = quotes.css(".tag::text").extract()

                items['title'] = title
                items['author'] = author
                items['tag'] = tag

                yield items
```

### items.py
```python
# Define here the models for your scraped items
#
# See documentation in:
# https://docs.scrapy.org/en/latest/topics/items.html

import scrapy


class QuotetItem(scrapy.Item):
    # define the fields for your item here like:
    title = scrapy.Field()
    author = scrapy.Field()
    tag = scrapy.Field()
```

### json file 
```python
[
{"title": ["\u201cThe world as we have created it is a process of our thinking. It cannot be changed without changing our thinking.\u201d"], "author": ["Albert Einstein"], "tag": ["change", "deep-thoughts", "thinking", "world"]},
{"title": ["\u201cIt is our choices, Harry, that show what we truly are, far more than our abilities.\u201d"], "author": ["J.K. Rowling"], "tag": ["abilities", "choices"]},
{"title": ["\u201cThere are only two ways to live your life. One is as though nothing is a miracle. The other is as though everything is a miracle.\u201d"], "author": ["Albert Einstein"], "tag": ["inspirational", "life", "live", "miracle", "miracles"]},
{"title": ["\u201cThe person, be it gentleman or lady, who has not pleasure in a good novel, must be intolerably stupid.\u201d"], "author": ["Jane Austen"], "tag": ["aliteracy", "books", "classic", "humor"]},
{"title": ["\u201cImperfection is beauty, madness is genius and it's better to be absolutely ridiculous than absolutely boring.\u201d"], "author": ["Marilyn Monroe"], "tag": ["be-yourself", "inspirational"]},
{"title": ["\u201cTry not to become a man of success. Rather become a man of value.\u201d"], "author": ["Albert Einstein"], "tag": ["adulthood", "success", "value"]},
{"title": ["\u201cIt is better to be hated for what you are than to be loved for what you are not.\u201d"], "author": ["Andr\u00e9 Gide"], "tag": ["life", "love"]},
{"title": ["\u201cI have not failed. I've just found 10,000 ways that won't work.\u201d"], "author": ["Thomas A. Edison"], "tag": ["edison", "failure", "inspirational", "paraphrased"]},
{"title": ["\u201cA woman is like a tea bag; you never know how strong it is until it's in hot water.\u201d"], "author": ["Eleanor Roosevelt"], "tag": ["misattributed-eleanor-roosevelt"]},
{"title": ["\u201cA day without sunshine is like, you know, night.\u201d"], "author": ["Steve Martin"], "tag": ["humor", "obvious", "simile"]}
]
```

### CSV file
```python
author,tag,title
Albert Einstein,"change,deep-thoughts,thinking,world",“The world as we have created it is a process of our thinking. It cannot be changed without changing our thinking.”
J.K. Rowling,"abilities,choices","“It is our choices, Harry, that show what we truly are, far more than our abilities.”"
Albert Einstein,"inspirational,life,live,miracle,miracles",“There are only two ways to live your life. One is as though nothing is a miracle. The other is as though everything is a miracle.”
Jane Austen,"aliteracy,books,classic,humor","“The person, be it gentleman or lady, who has not pleasure in a good novel, must be intolerably stupid.”"
Marilyn Monroe,"be-yourself,inspirational","“Imperfection is beauty, madness is genius and it's better to be absolutely ridiculous than absolutely boring.”"
Albert Einstein,"adulthood,success,value",“Try not to become a man of success. Rather become a man of value.”
André Gide,"life,love",“It is better to be hated for what you are than to be loved for what you are not.”
Thomas A. Edison,"edison,failure,inspirational,paraphrased","“I have not failed. I've just found 10,000 ways that won't work.”"
Eleanor Roosevelt,misattributed-eleanor-roosevelt,“A woman is like a tea bag; you never know how strong it is until it's in hot water.”
Steve Martin,"humor,obvious,simile","“A day without sunshine is like, you know, night.”"
```

### XML File
```python
<?xml version="1.0" encoding="utf-8"?>
<items>
<item><title><value>“The world as we have created it is a process of our thinking. It cannot be changed without changing our thinking.”</value></title><author><value>Albert Einstein</value></author><tag><value>change</value><value>deep-thoughts</value><value>thinking</value><value>world</value></tag></item>
<item><title><value>“It is our choices, Harry, that show what we truly are, far more than our abilities.”</value></title><author><value>J.K. Rowling</value></author><tag><value>abilities</value><value>choices</value></tag></item>
<item><title><value>“There are only two ways to live your life. One is as though nothing is a miracle. The other is as though everything is a miracle.”</value></title><author><value>Albert Einstein</value></author><tag><value>inspirational</value><value>life</value><value>live</value><value>miracle</value><value>miracles</value></tag></item>
<item><title><value>“The person, be it gentleman or lady, who has not pleasure in a good novel, must be intolerably stupid.”</value></title><author><value>Jane Austen</value></author><tag><value>aliteracy</value><value>books</value><value>classic</value><value>humor</value></tag></item>
<item><title><value>“Imperfection is beauty, madness is genius and it's better to be absolutely ridiculous than absolutely boring.”</value></title><author><value>Marilyn Monroe</value></author><tag><value>be-yourself</value><value>inspirational</value></tag></item>
<item><title><value>“Try not to become a man of success. Rather become a man of value.”</value></title><author><value>Albert Einstein</value></author><tag><value>adulthood</value><value>success</value><value>value</value></tag></item>
<item><title><value>“It is better to be hated for what you are than to be loved for what you are not.”</value></title><author><value>André Gide</value></author><tag><value>life</value><value>love</value></tag></item>
<item><title><value>“I have not failed. I've just found 10,000 ways that won't work.”</value></title><author><value>Thomas A. Edison</value></author><tag><value>edison</value><value>failure</value><value>inspirational</value><value>paraphrased</value></tag></item>
<item><title><value>“A woman is like a tea bag; you never know how strong it is until it's in hot water.”</value></title><author><value>Eleanor Roosevelt</value></author><tag><value>misattributed-eleanor-roosevelt</value></tag></item>
<item><title><value>“A day without sunshine is like, you know, night.”</value></title><author><value>Steve Martin</value></author><tag><value>humor</value><value>obvious</value><value>simile</value></tag></item>
</items>
```

# Using pipelines to store scrapped data:
 
Main path will be scraped data -> Item containers -> pipelines -> SQL/Mongo databases
```python 
# Define your item pipelines here
#
# Don't forget to add your pipeline to the ITEM_PIPELINES setting
# See: https://docs.scrapy.org/en/latest/topics/item-pipeline.html


# useful for handling different item types with a single interface
from itemadapter import ItemAdapter


class QuotetPipeline:
    def process_item(self, item, spider):
        print("Pipelines: "+ item['title'][0])
        return item
```

# Basics of SQLITE
```python
import sqlite3

conn = sqlite3.connect("myquotes.db")
curr = conn.cursor()
# curr.execute("""create table quotes_tb(
#             title text,
#             author text,
#             tag text
#             )""")

curr.execute("""insert into quotes_tb values('Python is awesome','buildwithpython','python')""")
conn.commit()
conn.close()
```

# Storing data in sqlites

### Pipelines.py
```python 
# Define your item pipelines here
#
# Don't forget to add your pipeline to the ITEM_PIPELINES setting
# See: https://docs.scrapy.org/en/latest/topics/item-pipeline.html


# useful for handling different item types with a single interface
from itemadapter import ItemAdapter

import sqlite3
class QuotetPipeline:

    def __init__(self):
        self.create_connection()
        self.create_table()
    def create_connection(self):
        self.conn = sqlite3.connect("my_quotes.db")
        self.curr = self.conn.cursor()
    def create_table(self):
        self.curr.execute("""DROP TABLE IF EXISTS quotes_tb""")
        self.curr.execute("""create table quotes_tb(
                            title text,
                            author text,
                            tag text
                            )""")

    def process_item(self, item, spider):
        print("Pipelines: "+ item['title'][0])
        return item

    def store_db(self,item):
        self.curr.execute("""insert into quotes_tb values (?,?,?)""",(
            item['title'][0],
            item['author'][0],
            item['tag'][0]
        ))
        self.conn.commit()
```

# Data storage in MYSQL
```python 
# Define your item pipelines here
#
# Don't forget to add your pipeline to the ITEM_PIPELINES setting
# See: https://docs.scrapy.org/en/latest/topics/item-pipeline.html


# useful for handling different item types with a single interface
from itemadapter import ItemAdapter

import mysql.connector


class QuotetPipeline(object):

    def __init__(self):
        self.create_connection()
        self.create_table()

    def create_connection(self):
        self.conn = mysql.connector.connect(
            host='localhost',
            user='root',
            passwd='1helloworld',
            database='myquotes'
        )
        self.curr = self.conn.cursor()

    def create_table(self):
        self.curr.execute("""DROP TABLE IF EXISTS quotes_tb""")
        self.curr.execute("""create table quotes_tb(
                            title text,
                            author text,
                            tag text
                            )""")

    def process_item(self, item, spider):
        print("Pipelines: " + item['title'][0])
        return item

    def store_db(self, item):
        self.curr.execute(""" insert into table quotes_tb """, (
            item['title'][0],
            item['author'][0],
            item['tag'][0]
        ))
        self.conn.commit()
```

# Crawling and Following links
```python
import scrapy
from ..items import QuotetItem


class Quotes_to_scrape(scrapy.Spider):
    name = 'quotes'
    start_urls = [
        "https://quotes.toscrape.com/"
    ]
    def parse(self, response):
            items = QuotetItem()
            all_div_quotes = response.css('div.quote')
            for quotes in all_div_quotes:
                title = quotes.css('span.text::text').extract()
                author = quotes.css('.author::text').extract()
                tag = quotes.css(".tag::text").extract()

                items['title'] = title
                items['author'] = author
                items['tag'] = tag

                yield items

            next_page = response.css('li.next a::attr(href)').get()
            if next_page is not None:
                yield response.follow(next_page, callback = self.parse)
```

# Pagination 
Pagination is the art of scraping next pages
Syntax : Quotes.toscrape.com/page/1/

```python 
mport scrapy
from ..items import QuotetItem


class QuoteSpider(scrapy.Spider):
    name = 'quotes'
    page_number = 2
    start_urls = [
        "https://quotes.toscrape.com/page/1/"
    ]
    def parse(self, response):
            items = QuotetItem()
            all_div_quotes = response.css('div.quote')
            for quotes in all_div_quotes:
                title = quotes.css('span.text::text').extract()
                author = quotes.css('.author::text').extract()
                tag = quotes.css(".tag::text").extract()

                items['title'] = title
                items['author'] = author
                items['tag'] = tag

                yield items

            next_page = "https://quotes.toscrape.com/page/" + str(QuoteSpider.page_number) + '/'
            print(next_page)
            if QuoteSpider.page_number < 11:
                QuoteSpider.page_number += 1
                yield response.follow(next_page, callback = self.parse)
```

# Amazon Web Scrapper
## Login forms
We can also use python scraping inorder to login forms
It can also be used to check out username and password

## Code
```python
import scrapy
from scrapy.http import FormRequest
from scrapy.utils.response import open_in_browser
from ..items import QuotetItem


class QuoteSpider(scrapy.Spider):
    name = 'quotes'
    start_urls = [
        'https://quotes.toscrape.com/login'
    ]
    def parse(self, response):
        token = response.css('form input::attr(values)').extract()
        return FormRequest.from_response(response,formdata={
            'csrf_token' : token,
            'username' : 'fantasmaamante09@gmail.com',
            'password' : '1HelloWorld'
        }, callback = self.start_scraping)
    def start_scraping(self,response):
        open_in_browser(response)
        items = QuotetItem()
        all_div_quotes = response.css('div.quote')
        for quotes in all_div_quotes:
            title = quotes.css('span.text::text').extract()
            author = quotes.css('.author::text').extract()
            tag = quotes.css(".tag::text").extract()

            items['title'] = title
            items['author'] = author
            items['tag'] = tag

            yield items
```
After this do Inspect login 
As a result youre loged in 

## Amazon Scraping
```python
import scrapy
from ..items import AmazontutorialItem

class AmazonSpiderSpider(scrapy.Spider):
    name = 'amazon'
    start_urls = ['https://www.amazon.com/s?i=electronics-intl-ship&bbn=16225009011&rh=n%3A3248684011&dc&ds=v1%3AI91B%2BdZTSA96JFKRasp6HXQXmnwcDXjnGP3sdGiHpdM&qid=1663938140&ref=sr_ex_n_1']

    def parse(self, response):
        items = AmazontutorialItem()
        product_name = response.css('.a-size-base-plus::text').extract()
        product_price = response.css('.a-size-base-plus').css('::text').extract()
        product_image = response.css('.s-height-equalized .s-image::attr(src)').extract()

        items['product_name'] = product_name
        items['product_price'] = product_price
        items['product_image'] = product_image

        yield  items
```

# Bypassing restrictions with user agents
## Setting
```python
# Scrapy settings for amazontutorial project
#
# For simplicity, this file contains only settings considered important or
# commonly used. You can find more settings consulting the documentation:
#
#     https://docs.scrapy.org/en/latest/topics/settings.html
#     https://docs.scrapy.org/en/latest/topics/downloader-middleware.html
#     https://docs.scrapy.org/en/latest/topics/spider-middleware.html

BOT_NAME = 'amazontutorial'

SPIDER_MODULES = ['amazontutorial.spiders']
NEWSPIDER_MODULE = 'amazontutorial.spiders'


# Crawl responsibly by identifying yourself (and your website) on the user-agent
#USER_AGENT = 'amazontutorial (+http://www.yourdomain.com)'
# USER_AGENT = 'https://developers.whatismybrowser.com/useragents/parse/79-googlebot'
# Obey robots.txt rules
ROBOTSTXT_OBEY = True

# Configure maximum concurrent requests performed by Scrapy (default: 16)
#CONCURRENT_REQUESTS = 32

# Configure a delay for requests for the same website (default: 0)
# See https://docs.scrapy.org/en/latest/topics/settings.html#download-delay
# See also autothrottle settings and docs
#DOWNLOAD_DELAY = 3
# The download delay setting will honor only one of:
#CONCURRENT_REQUESTS_PER_DOMAIN = 16
#CONCURRENT_REQUESTS_PER_IP = 16

# Disable cookies (enabled by default)
#COOKIES_ENABLED = False

# Disable Telnet Console (enabled by default)
#TELNETCONSOLE_ENABLED = False

# Override the default request headers:
#DEFAULT_REQUEST_HEADERS = {
#   'Accept': 'text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8',
#   'Accept-Language': 'en',
#}

# Enable or disable spider middlewares
# See https://docs.scrapy.org/en/latest/topics/spider-middleware.html
#SPIDER_MIDDLEWARES = {
#    'amazontutorial.middlewares.AmazontutorialSpiderMiddleware': 543,
#}

# Enable or disable downloader middlewares
# See https://docs.scrapy.org/en/latest/topics/downloader-middleware.html
DOWNLOADER_MIDDLEWARES = {
    'scrapy.downloadermiddlewares.useragent.UserAgentMiddleware': None,
    'scrapy_user_agents.middlewares.RandomUserAgentMiddleware': 400,
}
#DOWNLOADER_MIDDLEWARES = {
#    'amazontutorial.middlewares.AmazontutorialDownloaderMiddleware': 543,
#}

# Enable or disable extensions
# See https://docs.scrapy.org/en/latest/topics/extensions.html
#EXTENSIONS = {
#    'scrapy.extensions.telnet.TelnetConsole': None,
#}

# Configure item pipelines
# See https://docs.scrapy.org/en/latest/topics/item-pipeline.html
#ITEM_PIPELINES = {
#    'amazontutorial.pipelines.AmazontutorialPipeline': 300,
#}

# Enable and configure the AutoThrottle extension (disabled by default)
# See https://docs.scrapy.org/en/latest/topics/autothrottle.html
#AUTOTHROTTLE_ENABLED = True
# The initial download delay
#AUTOTHROTTLE_START_DELAY = 5
# The maximum download delay to be set in case of high latencies
#AUTOTHROTTLE_MAX_DELAY = 60
# The average number of requests Scrapy should be sending in parallel to
# each remote server
#AUTOTHROTTLE_TARGET_CONCURRENCY = 1.0
# Enable showing throttling stats for every response received:
#AUTOTHROTTLE_DEBUG = False

# Enable and configure HTTP caching (disabled by default)
# See https://docs.scrapy.org/en/latest/topics/downloader-middleware.html#httpcache-middleware-settings
#HTTPCACHE_ENABLED = True
#HTTPCACHE_EXPIRATION_SECS = 0
#HTTPCACHE_DIR = 'httpcache'
#HTTPCACHE_IGNORE_HTTP_CODES = []
#HTTPCACHE_STORAGE = 'scrapy.extensions.httpcache.FilesystemCacheStorage'
```

# Scraping multiple pages in Amazon
```python
import scrapy
from ..items import AmazontutorialItem

class AmazonSpiderSpider(scrapy.Spider):
    name = 'amazon'
    page_number = 2
    start_urls = ['https://www.amazon.com/s?i=electronics-intl-ship&bbn=16225009011&rh=n%3A3248684011&dc&ds=v1%3AI91B%2BdZTSA96JFKRasp6HXQXmnwcDXjnGP3sdGiHpdM&qid=1663938140&ref=sr_ex_n_1']

    def parse(self, response):
        items = AmazontutorialItem()
        product_name = response.css('.a-size-base-plus::text').extract()
        product_price = response.css('.a-size-base-plus').css('::text').extract()
        product_image = response.css('.s-height-equalized .s-image::attr(src)').extract()

        items['product_name'] = product_name
        items['product_price'] = product_price
        items['product_image'] = product_image

        yield  items
        next_page = 'https://www.amazon.com/s?i=electronics-intl-ship&bbn=16225009011&rh=n%3A3248684011&dc&page='+ str(AmazonSpiderSpider.page_number) + '&qid=1663950585&ref=sr_pg_2'
        if AmazonSpiderSpider.page_number <= 100:
            AmazonSpiderSpider.page_number += 1
            yield response.follow(next_page,callback=self.parse)
```
