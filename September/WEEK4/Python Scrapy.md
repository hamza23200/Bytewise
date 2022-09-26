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


XPath is a language for selecting nodes in XML documents, which can also be used with HTML.
```python 
    response.xpath("//title/text()').extract()
    response.xpath("//span[@class='text']/text()')[1].extract()
    response.xpath("//span[@class='text']/text()')[1].extract()
```
CSS used for syling webiste
```python
    response.css("title").extract()
    response.xpath("title::text)[0].extract()
    response.xpath("title::text).extract()_first
    response.xpath("span.text::text).extract()
    response.xpath("span.text::text)[1].extract()
    response.xpath(".author::text).extract()
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
