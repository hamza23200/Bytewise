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
        yield {"Titletext" : title } #dictionary
        ```
