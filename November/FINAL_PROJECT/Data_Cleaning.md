Data Colection code 

```python
import glassdoor_scrapper as gs
import pandas as pd

path= ""

df=gs.get_jobs('Data Scientist',1000,False,path,15)
df.to_csv('glassdoor_jpbs.csv',index=False)
```
then upload to github
