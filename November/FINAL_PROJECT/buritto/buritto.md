```python
#import relevant libraries 
import pandas as pd 
import numpy as np 
import atoti as tt 
import re 
```
```python
#load in data 
df = pd.read_csv('burritos_01022018.csv')     

#explore column headers
df.columns

#look at first 5 rows of data
df.head()

#explore shape and central tendency 
df.describe()
```
```python
df.columns = [re.sub("([\(\[]).*?([\)\]])", "", x).strip() for x in df.columns]
df.columns = [x.replace(':','_').strip() for x in df.columns]
df.columns
```
```python
#check if there are nulls in column
df.isnull().any()
#check the % of the column that is null
df.isnull().sum() / df.shape[0]
```
```python
#create an atoti session and store dashboard files in ./content
session = tt.Session() 
```
```python
# scale circumference, volume, fillings, length, mass, and cost data
from sklearn.preprocessing import MinMaxScaler
scaler = MinMaxScaler()
burrito_vars_norm = df.loc[:,['Circum','Volume','Length','Mass','Cost']]

#change 0-1 scaline to 0-10 scale for readability 
bnorms = scaler.fit_transform(burrito_vars_norm)*10


#create new columns for normalized values in our datframe (df)
df[['Circum_norm','Volume_norm','Length_norm','Mass_norm','Cost_norm']] = bnorms 
```
```python
#upload dataframe to atoti session 
burrito_table = session.read_pandas(df,table_name = 'burritos')

burrito_table.head()
```
```python
#create data cube 
cube = session.create_cube(burrito_table)

#create hierarchies, levels, and measures 
h = cube.hierarchies
l = cube.levels
m = cube.measures

#create new measures (examples)
m['five'] = 5
m['lenXwrap'] = m['Length.MEAN'] * m['Wrap.MEAN']

#create pivot table visual / example
session.visualize('exploration 1')

burrito_variables = pd.melt(df.reset_index(), id_vars = ['Location','Burrito'], value_vars = ['Circum_norm','Volume_norm','Length_norm','Mass_norm','Cost_norm'],)
burrito_variables
```
```python
#create scatterplot visual /example
session.visualize('scatter plot neighborhood yelp google')
```
```python
#add reformatted data to table to visualize 
burrito_var_table = session.read_pandas(burrito_variables, table_name = 'burrito_variables', keys=['Location','Burrito','variable'])

#join main dataframe with new burrito_var_table
burrito_table.join(burrito_var_table)

# create value measure in atoti with values for each of the burrito variables that we made above (mass, circum, cost, etc.)
m['value'] = tt.agg.mean(burrito_var_table["value"])
m['aggvalue'] = tt.agg.mean(m['value'], scope = tt.scope.origin(l['Location'],l['Burrito'],l['variable']))
```
```python
#create radar chart 
session.visualize('radar chart final')  
```


     
