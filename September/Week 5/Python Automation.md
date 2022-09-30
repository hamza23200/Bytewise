# Automation using Python

# Web Scraping 
## Overview: 
* Get HN website front page
* Scrape required content
* Build Email body/content
* Email Authentication
* Email sent

Extracting material from Web, then use the required components 
and use email body in the email that we compose and then we send it to required users.

## Setting up Python Environment
### Packages:
* requests: HTTP requests   
* bs4: Beautiful Soup used for web scraping
* smttplib(default): Email authentication and transaction
* email.mime(default): Creating email body
* datetime(default): Accessing and Manipulating date and time

When you are running the program import these all in your terminal.
To install a pacakge do *pip3 install ___*
To install Requests, beautifulsoup4

```python 
import requests       # http requests
from  bs4 import BeautifulSoup       # web scraping
import smtplib     # send the mail

# email body
from email.mime.multipart import MIMEMultipart
from email.mime.text import MIMEText

import datetime

now = datetime.datetime.now()
```
