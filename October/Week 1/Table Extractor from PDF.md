# Table Extractor from PDF

PDF= PORTABLE DOCUMENT FORMAT
its purpose is to work on any machine and is independent of software
#### PDF Structure
* Header
* Body
* Xref table
* Trailer
![image](https://user-images.githubusercontent.com/102249128/193403483-bbfd894b-a620-472d-a1c9-3ba075242c2b.png)

# Packages
* Jupyter Notebook (IDE)
* Camelot for extracting data/tables from PDF
* Seaborn for visualization of Data

To install camelot do *pip3 instal camelot-py*

## Why choose Camelot
* Give you power to play with hyper parameters
* ![image](https://user-images.githubusercontent.com/102249128/193404810-dc9abb91-55ee-4dc4-92d4-6c49e9cc142d.png)

This is all part of Pandas
Its a Data Manipulation package that is widely used with python
Helps:
* Read/write CSV
* Reformatting 
* Data Analysis
* Data Pre processing

## Table to Extract 
![image](https://user-images.githubusercontent.com/102249128/193404933-0722d9d1-09df-4857-8791-5901d359fdf5.png)

# Code
Type *ls* to see the avaliable files in environmnet 

```python 
import camelot as cm

#To get data from Web 
input_pdf=cm.read_pdf(URL)

#To get from local machine
input_pdf=cm.read_pdf("NAME",flavor='lattice',pages='1,2')

for n in input_pdf:
 print(n) #will show table sizes
 
 #for example if we want 3rd table
 input_pdf[2].df
 ```
 ![image](https://user-images.githubusercontent.com/102249128/193405677-d70e137a-9528-41e1-b1b1-136179cbc465.png)
 ```python
#from this we want line 11,12,13
df=input_pdf[2].df.loc[11:14,1:3]
```
 ![image](https://user-images.githubusercontent.com/102249128/193405818-b9a5d482-ed85-428c-a225-9df919719f84.png)

 ```python
#from this we want Headings
df.columns =["KPI","2001","2011"]
```
![image](https://user-images.githubusercontent.com/102249128/193406043-b28a39d1-3a6c-4fbc-8aae-aa15a6e0b60e.png)

```python
#Now Data Analysis (changing string to no.)
df.loc[:,["2001","2011"]]=df.loc[:,["2001","2011"]].astype[float]

#change format to csv
df.to_csv("packt_output.csv")

df.to_excel("packt_output.xlsx")

import pandas as pd
df2 = pd.read_csv("packt_output.csv")
df2

#Visulaization Libarry 
import seaborn as sns
df_melted = df.melt('KPI', var_name='year', value_name='percentage')
```
#wide to long format 
![image](https://user-images.githubusercontent.com/102249128/193406309-36a8d8cb-d01e-48e5-9e98-8cb1dd4bf06b.png)

```python
#Plot
sns.barplot(x = "KPI", y = "percentage", hue = "year", data = df_melted);
```
![image](https://user-images.githubusercontent.com/102249128/193406361-404e6475-6df7-4ebb-987e-5ab2efc03004.png)



