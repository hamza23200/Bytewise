# TED Talk Downloader 
# Packages
* Requests (HTML)
* beautifulsoup4 (web scarpping)

To check if package is installed:
python3
import bs4
from bs4 import beautifulsoup4

```python 
import requests #TED PAge
from bs4 import BeautifulSoup #web scarpe
import re #regular expression pattern matching 
import sys #argument parsing (generalize code for using multiple URL)

#exception handling (unexpected error)
if len(sys.argv) > 1: #arg passed with code execution
  url = sys.argv[1]
else:
  sys.exit("Error: Please enter the TED Talk URL")

r = requests.get(url) #send req
print("Download about to start") 

soup = BeautifulSoup(r.content, features='lxml') #we interested only in content

for val in soup.find_all("script"):
  if(re.search("talkpage.init",str(val))) is not None: #talk page init has mp4 files
      result = str(val)

result_mp4 = re.search("(?P<url>https?:[^\s]+)(mp4)", result).group("url")
mp4_url = result_mp4.split('"')[0]

print("Downloading video from ....." + mp4_url)
file_name = mp4_url.split("/")[len(mp4_url.split("/"))-1].split('?')[0] #assign name to file
print("Storing video in ..... " + file_name)

r = requests.get(mp4_url)
with open(file_name,'wb') as f:
  f.write(r.content)

print("Download process finished")
# ted_talk_downloader.py
#CLA tool= package as 1 line and get ouptut w/o ediing

# For running code put python3 filename URLofTED
```
