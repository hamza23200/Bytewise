# Automated Bulk Resume Parser 


## Purpose: 
* Go through multiple resumes
* Extracts relevant information from resume
* Convert them into structured tabular format 
* Build up one click command level tool

Dealing with resume's of PDF type only
NLP used allot in DS/ML/AI

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
```python
import spacy
nlp = spacy.load("en_core_web_sm") #load language model

text="xyz a asd safasf fasf asfasf sfsf"
doc = nlp(text)

#Tokenization =splitting text based on token
for token in doc:
    print(token)
    
#Only Noun
for token in doc:
    if token.pos_ == "NOUN":
        print(token)

#Named Entity Recognition= identify entity 
for entity in doc.ents:
        print(entity.text, entity.label_)      
```
![image](https://user-images.githubusercontent.com/102249128/193442922-43de146b-67dc-4df7-8f3f-1f281db2aa09.png)
Text | Label

# Code
```python

import spacy
import pdfminer
import re
import os #file manipulation
import pandas as pd

import pdf2txt

def convert_pdf(f):

    output_filename = os.path.basename(os.path.splitext(f)[0]) + '.txt' #Name.pdf->Name.txt
    #os.path.join('..', 'data', 'output', output_filename)
    output_filepath = os.path.join('output/txt/', output_filename)
    pdf2txt.main(args=[f, '--outfile', output_filepath]) #text file to be saved in given location
    print(output_filepath + " saved successfully!!!")
    return open(output_filepath).read()


nlp = spacy.load("en_core_web_sm")


result_dict = {'name': [], 'phone': [], 'email': [], 'skills': []}
names = []
phones = []
emails = []
skills = []


def parse_content(text): #extract content
    skillset = re.compile('python|java|sql|hadoop|tableau') # we want these skills
    phone_num = re.compile('(\d{3}[-\.\s]??\d{3}[-\.\s]??\d{4}|\(\d{3}\)\s*\d{3}[-\.\s]??\d{4}|\d{3}[-\.\s]??\d{4})')
    #phone_num credit https://stackoverflow.com/a/3868861
    
    
    doc = nlp(text)
    name = [entity.text for entity in doc.ents if entity.label_ is 'PERSON'][0] #nlp
    print(name)
    email = [word for word in doc if word.like_email == True][0] #nlp
    print(email)
    phone = str(re.findall(phone_num,text.lower())) 
    skills_list = re.findall(skillset,text.lower())
    unique_skills_list = str(set(skills_list)) 
    names.append(name)
    emails.append(email)
    phones.append(phone)
    skills.append(unique_skills_list)
    print("Extraction completed successfully!!!")


for file in os.listdir('resumes/'):
    if file.endswith('.pdf'):
        print('Reading.....' + file)
        txt = convert_pdf(os.path.join('resumes/',file))
        parse_content(txt)


result_dict['name'] = names
result_dict['phone'] = phones
result_dict['email'] = emails
result_dict['skills'] = skills
#print(result_dict)


result_df = pd.DataFrame(result_dict)
result_df
# You get a table

result_df.to_csv('output/csv/parsed_resumes.csv')
#saves as CSV
```


