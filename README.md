# Voices-in-the-Wilderness-Wolves-in-the-USA
# Project Description: 
This project applies semantic analysis using Python, PyPDF2, and NLTK to examine the way humans report conditions of wolf populations across the United States. Using reports from the Yellowstone and Oregon wolf populations, which were selected for their contrasting patterns of success and decline, the project situates these regional cases within the broader context of national wolf population data. I was able to use these PDFs in Python by utilizing the **PyPDF2 pdfreader**, something that I know will be employed in my future projects. 

Using the **Natural Language Toolkit (NLTK)**, this analysis incorporates concordances, word similarities, and text‑generation techniques to identify linguistic patterns within each report. The findings reveal notable variation between the datasets, with the Oregon report exhibiting the greatest degree of linguistic difference, offering insight into the distinct ecological and management conditions shaping these populations, as well as how these various institutions view interacting with their existing wolves. 

When analyzing the generated texts; Yellowstone showed the most emphasis on wolf birth and various success, Oregon showed the most emphasis on lethal removal, and the United States as a whole showed prominence with mortality and population control. Oregon's language surronding their reports was the most concerning to me, as the results there were very detached and clinical, with very little respect to animaal lives in these results. Now that I have familiarity with **NLTK** and **PyPDF2**, my ultimate hope is to gain mastery of these libraries and explore these conclusions further through the lens of the media attention these wolf populations tend to get. 

# Rationale Statement: 
As the current administration seeks to defund conservation efforts and National Parks, it’s important now more than ever to examine the reality of endangered animals within the United States. My goal is to stress that our National Parks, such as Yellowstone, create a safe haven for the reintroduction efforts of various species, such as the gray wolf. Wolf populations have been the focus of conservation efforts across many US national parks. These locations are essential for our ecological longevity. As this administration focuses on twisting words to suit their needs, it seemed only fitting to explore how we differentiate these populations linguistically, and how these reports view their various groups and their current state. You can tell a lot about what a community values in regards to a topic based on the information they focus on and how they choose to present it. It also touches on my own personal interests and questions, as the wolves of Yellowstone are a notorious success, one that we are struggling to replicate in other places. 


As humans, we have the greatest power to both help and harm these animals, and it is our responsibility to hold these institutions accountable and read between the lines. I believe my findings regarding this project confirm that. These national parks belong to all of us, and we should be invested in their health and longevity. What is happening now will have effects that will cascade through generations, and if we don't do something about it and make our voices heard through our vote and our dollar, those effects will be resoundingly negative. We get one Earth and one chance to love and care for the creatures upon it. Animals don't even know the fight they're involved in.

# Workflow:

First, I needed to install **PyPDF2 pdfreader** to read the provided PDFs. I only did one PDF at a time, as it kept everything more organized. 
```
pip install PyPDF2 pdfreader
```
Then I ran this code to extract text from the first page of the PDF. Make sure the PDF file is in the same folder. The code loads the PDF using PdfReader, selects the first page, and prints whatever text it contains into the kernel. 
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
I then went to check the number of pages that I loaded in. I needed to make sure I loaded them all in correctly, so I knew exactly how many I can loop through.
```
len(reader.pages)
```
I then attempted to check how many lines of text were on the first PDF page. 
```
len(reader.pages[0])
```
I then wanted to check what type of object the first PDF page is so that I know what it would return. 
```
type(reader.pages[0])
```
Then I needed to write a loop that goes through every page in the PDF one by one. For each page, it extracts the text and prints it so that you are able to extract all of the text from the PDF three.
```
for page in reader.pages:
    print(page.extract_text())
```
This line goes straight to page 9 of the PDF and extracts the text from that page. It’s a direct way to pull text from one page without looping through the whole document, to make sure that everything would print alright. 
```
reader.pages[8].extract_text()
```
I then created an empty list **text** and then had a loop go through each page in the PDF. For every page, it extracts the text and adds it to the **list**. When the loop is done, the text contains the extracted text from every page in order.
```
for page in reader.pages:
    print(page.extract_text())
```
I wanted to check that this was successful, so I did the following code to confirm it. 
```
reader.pages[8].extract_text()
```
I then had to take all the **tex**t pieces stored in the **list** and join them together into one long **string** so I could use the **NLTK library**. 
```
joined_text = ' '.join(text)
```
Then I made a new file and name it **yellowstone.txt**, using the first PDF I worked with as an example, which will put all of the text into it. When this is done, you’ll see the new text file appear in your python library. 
```
with open('yellowstone.txt', 'w', encoding='utf-8') as f:
    f.write(joined_text)
```
I then needed to load the nltk library and download two tools it needs: **punkt_tab**, which helps Python split text into words and sentences, and **stopwords**, which gives a list of common words to ignore. It also imports Text so you can work with the text in NLTK.
```
import nltk
nltk.download('punkt_tab')
from nltk.text import Text
nltk.download('stopwords')
```
I then had to take the text string **(joined_text)** and break it into individual words. **nltk.word_tokenize()** turns the text into a list of **tokens** that you can analyze using the NLTK library.
```
tokenized = nltk.word_tokenize(joined_text)
```
I wanted to confim that I had done this step correctly, so I checked the first ten words. 
```
tokenized[:10]
```
Then I created a new **NLTK Text object** from the list of words, which I called **new_text**.
```
new_text = Text(tokenized)
```
I wanted to check that the first ten words had been tokenized correctly with the following code.
```
new_text[:10]
```
After that came back correct, I wanted to confirm that the type of the **new_text** object we'd created matched my expectations. 
```
type(new_text)
```
Now I am ready to begin my semantic analysis of this PDF by using the options provided by the NLTK library (mostly the _similar_ and _collocations_ functions). I've included the the opporations that I used below. However, I had to edit my collocation terms when I encounter the Oregon report, as it became clear to me that they used different terminology compared to the Yellowstone and USA data, those terms are not included but can be found in my _GreyWolfOregon.ipynb_ (the notebook). 
```
- new_text.similar('wolves')
- new_text.collocations()
- new_text.concordance('wolves')
- new_text.concordance('died')
- new_text.concordance('endangered')
- new_text.concordance('mortality')
- new_text.concordance('killed')
- new_text.concordance('death')
```
Once I compared those results, I then had NLTK generate a text portion from the PDF, which was my main point of anaysis and visualization of the PDF data. I used this as my main point of analysis as it removed my own bias and stopped me from hunting for specific terms in the reports. 
```
new_text.generate(length=100, text_seed=None, random_seed=42)
```
**I repeated these steps for the other two PDFs.** 

# Further Uses:

The further uses of this project would be to run further semantic analysis using Python on reports from states that weren't considered. While Colorado is currently witnessing a rapid decline in their recently reintroduced wolf population, they have yet to publish an offical report detailing the exact data. Having mentioned Colorado, there's an angle that can be taken regarding the media's documentation of the wolf populations, as a great portion of that media appears to be negative surrounding the recently reintroduced wolves. Another way to further use this project would be to apply this analysis to other endangered and controversial species, especially in regards to further providing them with territory, such as our National Parks, in order for them to thrive. Given more time, I would've been interested in exploring the exact language used around human and wildlife conflict, as Oregon showed interesting differences regarding the terminology used to express lethal operations towards their wolf population. Essentially, this project is just the beginning! As my skills advance, and my knowledge of NLTK becomes less mediocre, I hope to return to these datasets and explore related materials. I see an abundance of further uses that can spring from this starting point _(with more time and expertise)_. 

# Files Included: 

All the files used for the creation and execution of this project can be found in the repository. 
1. *The PDF Reports*
- 2024_Wolf Yellowstone.pdf (Yellowstone Data)
- GreyWolfOregon.pdf (Oregon Data)
- Gray Wolf Pop.pdf (USA Data)
3. *The Text Files*
- graywolf.txt (USA text)
- oregon.txt (Oregon text)
- yellowstone.txt (Yellowstone text)
4. *My Python Notebooks showing the work and outcomes, confirming my process and conclusions.*
- GreyWolfOregon.ipynb (Oregon Notebook)
- GrayWolfYellowstone.ipynb (Yellowstone Notebook)
- GrayWolfUSA.ipynb (USA Notebook)
