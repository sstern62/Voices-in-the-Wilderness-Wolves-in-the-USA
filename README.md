# Voices-in-the-Wilderness-Wolves-in-the-USA
This project compared the language surrounding reports regarding wolf populations in the United States, with a specific lens taken comparing the population data from Yellowstone to that of the United States as a whole.

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


