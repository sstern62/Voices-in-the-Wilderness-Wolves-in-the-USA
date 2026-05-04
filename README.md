# Voices-in-the-Wilderness-Wolves-in-the-USA
# Project Description: 
This project applies semantic analysis using Python to examine the conditions of wolf populations across the United States. Using reports from the Yellowstone and Oregon wolf populations, which were selected for their contrasting patterns of success and decline, the project situates these regional cases within the broader context of national wolf population data.

Using the Natural Language Toolkit (NLTK), this analysis incorporates concordances, word similarities, and text‑generation techniques to identify linguistic patterns within each report. The findings reveal notable variation between the datasets, with the Oregon report exhibiting the greatest degree of linguistic difference, offering insight into the distinct ecological and management conditions shaping these populations, as well as how these various institutions view interacting with their existing wolves. 

When analyzing the generated texts; Yellowstone showed the most emphasis on wolf birth and various succes, Oregon showed the most emphasis on lethal removal, and the United States as a whole showed prominence with mortality and population control.

# Rationale Statement: 
As the current administration seeks to defund conservation efforts and National Parks, it’s important now more than ever to examine the reality of endangered animals within the United States. My goal is to stress that our National Parks, such as Yellowstone, create a safe haven for the reintroduction efforts of various species, such as the gray wolf. These locations are essential for our ecological longevity. As this administration focuses on twisting words to suit their needs, it seemed only fitting to explore how we differentiate these populations linguistically, and how these reports view their various groups. It also touches on my own personal interests and questions, as the wolves of Yellowstone are a notorious success, one that we are struggling to replicate in other places. 

As humans, we have the greatest power to both help and harm these animals, and it is our responsibility to hold these institutions accountable and read between the lines. 

# Workflow:

First, you need to install PyPDF2 pdfreader to read the provided PDFs. 
```
pip install PyPDF2 pdfreader
```
Run this script to extract text from the first page of a PDF. Make sure the file 2024_Wolf Yellowstone.pdf is in the same folder. The code loads the PDF using PdfReader, selects the first page, and prints whatever text it contains to the terminal. 
```
from PyPDF2 import PdfReader
reader = PdfReader("2024_Wolf Yellowstone.pdf")
page = reader.pages[0]
print(page.extract_text())
```
I then checked the type to make sure I understand what I'm working with and how to best move forward effectively.  
```
type(reader.pages)
```
I then went to check the number if pages I loaded in, to make sure I loaded them all in correctly and so I knew exactly how many I can loop through.
```
len(reader.pages)
```
I then attempt to check how many lines of text were on the first PDF page. 
```
len(reader.pages[0])
```
I then wanted to check what type of object the first PDF page is so that I know what it returns. 
```
type(reader.pages[0])
```
Then I needed to write a loop goes through every page in the PDF one by one. For each page, it extracts the text and prints it, so that you are able to extract all of the text from the PDF.
```
for page in reader.pages:
    print(page.extract_text())
```
This line goes straight to page 9 of the PDF and extracts the text from that page. It’s a direct way to pull text from one page without looping through the whole document, to make sure that everything rpinted alright. 
```
reader.pages[8].extract_text()
```
I then created an empty list called text and then had a loop go through each page in the PDF. For every page, it extracts the text and adds it to the list. When the loop is done, the text contains the extracted text from every page in order.
```
for page in reader.pages:
    print(page.extract_text())
```
I wanted to check that this was successful, so I did the following code to confirm it. 
```
reader.pages[8].extract_text()
```
I then had to take all the text pieces stored in the list text and join them together into one long string so I could use the NLTK library. 
```
joined_text = ' '.join(text)
```
Then I made a new file and name it yellowstone.txt, which will put all of the text into it. When this is done, you’ll see the new text file appear in your python library. 
```
with open('yellowstone.txt', 'w', encoding='utf-8') as f:
    f.write(joined_text)
```
I then needed to load the nltk library and download two tools it needs: punkt_tab, which helps Python split text into words and sentences, and stopwords, which gives a list of common words to ignore. It also imports Text so you can work with the text in NLTK.
```
import nltk
nltk.download('punkt_tab')
from nltk.text import Text
nltk.download('stopwords')
```
I then had to take the text string (joined_text) and break it into individual words. nltk.word_tokenize() turns the text into a list of tokens that you can analyze using the NLTK library.
```
tokenized = nltk.word_tokenize(joined_text)
```
I wanted to confim that I had done this step correctly, so I checked the first ten words. 
```
tokenized[:10]
```
Then I created a new NLTK Text object from the list of words, which I called new_text.
```
new_text = Text(tokenized)
```
I wanted to check that the first ten words had been tokenized correctly with the following code.
```
new_text[:10]
```
After that came back correct, I wanted to confirm the type of the new_text we'd created. 
```
type(new_text)
```
Now I ready to begin my semantic analysis of this PDF by using the options provided by the NLTK library. I've included the the opporations that I used below. 
```
new_text.similar('wolves')
new_text.collocations()
new_text.concordance('wolves')
new_text.concordance('died')
new_text.concordance('endangered')
new_text.concordance('mortality')
new_text.concordance('killed')
new_text.concordance('death')
```
Once I compared those results, I then had NLTK generate a text portion from the PDF, which was my main point of anaysis and visualization of the PDF data. 
```
new_text.generate(length=100, text_seed=None, random_seed=42)
```
I repeated these steps for the other two PDFs. 

# Further Uses:

The further uses of this project could be to run further semantic analysis using Python on reports from states that weren't consider during this project. While Colorado is currently witnessing a rapid decline in their recently reintroduced wolf population, they have yet to publish an office report detailing the facts. Having mentioned Colorado, there's an angle that can be taken regarding the media's documentation of the wolf populations, as a great portion of that media appears to be negative surronding the recently reintroduced population. Another way to further use this project would be to apply this analysis to other endangered and controversial species, especially in regards to the improve of having protected territory like our National Parks in order for them to thrive. Given more time, I would've been interested in exploring the exact language used around human and wildlife conflict, as Oregon showed interesting differences regarding the terminology used to express lethal operations towards their wolf population. 
