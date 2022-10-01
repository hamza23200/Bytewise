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

now = datetime.datetime.now() #current date time

content='' #empty string 

# Extracting hackernews stories
def extract_news(url):
    print('Extracting Hacker News Stories...')
    cnt = ''  #tmp plcae holder and assign value to content
    cnt += ("<b>HN Top Stories:</b>\n"+'<br>'+'-'*50 +'<br>') #<b>= bold text
    response = requests.get(url) #http response
    content = response.content
    soup = BeautifulSoup(content,'html.parser') 
    for i, tag in enumerate(soup.find_all('td',attrs={'class': 'title', 'valign':''})):
        cnt += ((str(i+1)+ '::' +tag.text + "\n" + '<br>') if tag.text != 'More' else '')
        #enumerated to get values
    return (cnt)

cnt = extract_news('https://news.ycombinator.com/')
content += cnt
content += ('<br>------<br>') #email finish 
content += ('<br><br>End of Message')
```

# Composing Email

```python 

import requests       # http requests
from  bs4 import BeautifulSoup       # web scraping
import smtplib     # send the mail

# email body
from email.mime.multipart import MIMEMultipart
from email.mime.text import MIMEText

import datetime

now = datetime.datetime.now()

# Extracting Hacker News Stories

content = ''

def extract_news(url):
    print('Extracting Hacker News Stories...')
    cnt = ''
    cnt += ("<b>HN Top Stories:</b>\n"+'<br>'+'-'*50 +'<br>')
    response = requests.get(url)
    content = response.content
    soup = BeautifulSoup(content,'html.parser')
    for i, tag in enumerate(soup.find_all('td',attrs={'class': 'title', 'valign':''})):
        cnt += ((str(i+1)+ '::' +tag.text + "\n" + '<br>') if tag.text != 'More' else '')
    return (cnt)

cnt = extract_news('https://news.ycombinator.com/')
content += cnt
content += ('<br>------<br>')
content += ('<br><br>End of Message')
```
```python
# Lets send the email
print("Composing Email...")

# update your email details
SERVER = 'hamzafaizi86@gmail.com' #smtp.gmail.com
PORT = 587 #for gmail
FROM = 'hamzafaizi86@gmail.com'
TO = 'hamzafaizi86@gmail.com'
PASS = '********'

msg = MIMEMultipart() #msg body

msg['Subject'] = 'Top News Stories HN [Automated Email]' + '' + str(now.day) + '-' + str(
now.year) #dynamic email 
msg['From'] = FROM
msg['To'] = TO

msg.attach(MIMEText(content,'html'))

print('Intitiating Server...')

server = smtplib.SMTP(SERVER,PORT)
server.set_debuglevel(1) #to see erroe msgs
server.ehlo()
server.starttls() #transaction email
server.login(FROM,PASS)
server.sendmail(FROM,TO,msg.as_string())

print('Email Sent...')

server.quit()

#go to google security settings and set less secure access apps on 
```
