Data Colection code 

```python
import glassdoor_scrapper as gs
import pandas as pd

path= ""

df=gs.get_jobs('Data Scientist',1000,False,path,15)
df.to_csv('glassdoor_jpbs.csv',index=False)
```
then upload to github:

* cd document/
* ds_proj
* echo "# ds_proj" >> README.md
* git add .
* git commit -m "uploaded scraper and run code"
* git remote add origin https://github.com/hamza23200/Data-Science.git #createnew repo
* git push

After this   
* git pull #creats sort of a copy
*git checkout -b data_cleaning

