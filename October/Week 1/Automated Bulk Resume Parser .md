# Automated Bulk Resume Parser 


## Purpose: 
* Go through multiple resumes
* Extracts relevant information from resume
* Convert them into structured tabular format 
* Build up one click command level tool

Dealing with resume's of PDF type only

# Packages
* import pdfminer.six(newer version) - pdf to text
* import spacy - NLP(natural language processing)
* import re - regex(Pattern Matching)
* import os os file path(for operating system and iterating multiple files)
* import pandas as pd - output CSV

To install spacy: python -m spacy download en_core_web_sm
To load: nlp= spacy.load('en_core_web_sm')

re and os are already installed 

### Essentials: 
Name, Email, Phone 
Extract skills for the relevant field  

# Basics od Regular Expression(Regex)
Sequence of characters that define a search pattern(characters and Meta characters)
Meta Characters: ^ $ .| {} [] () * + \

![image](https://user-images.githubusercontent.com/102249128/193427905-b9cfd383-f360-4776-85f3-4fd3ffa2ed85.png)

## Funnctions:
* re.match() # search word
* re.search()
* re.findall()
* re.split()
* re.sub()
* re.compile() # to create and comile and then used all other expressions

re.match('word|word2',variable)
finall will show both words

# Spacy


