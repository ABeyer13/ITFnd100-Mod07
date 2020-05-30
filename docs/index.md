# Pickling and Error Handling
**Name**: *ABeyer*

**Date**: *5/28/2020*

## Introduction
This week we went over the meaning and use of pickling and error handling in Python. In the first topic I discuss articles on the web that give great examples and descriptions about both pickling and error handling. In the second topic I discuss the script I created to demonstrate how each of these ideas work in Python. Lastly, in the conclusion I will summarize the topics discussed in this paper. 

## Topic 1: Research
### Pickling
There are two articles I found that were helpful to me in gaining a greater understanding of pickling in Python. The first article is a simple explanation of pickling, but what it helped to clarify for me was the purpose of pickling. I was at first confused why on earth we needed to use pickling if we could use open and close for txt files. But in the initial article, it describes how pickling can help serialize and deserialize an object (like a list) so that it can be used in multiple scripts easily. The second article goes into even greater detail about serialization, which was helpful to me since this was the first time I had heard of the term, and it was not thoroughly reviewed in the Module 07 video. 

https://pythontips.com/2013/08/02/what-is-pickle-in-python/

https://realpython.com/python-pickle-module/

### Error Handling
The first article is from the same website as one of the articles I used for pickling. I think this website does an excellent job explaining new concepts and ideas in a way that even beginners can understand. They break down each idea separately and then tie it all together at the end, using lots of great examples. Additionally, I included the resource we’ve used in class (w3schools) because it was helpful for me to get basic practice after reading through everything, watching all the videos, and having not yet actually coded except for the one Lab assignment.

https://realpython.com/python-exceptions/

https://www.w3schools.com/python/python_try_except.asp

## Topic 2: Creating My Script

### Pickling Example
For pickling, I decided to use a basic example to showcase how you can store complex data (lists) into a binary file (FavoritesPickles.dat). The first step was to create 3 different lists and the new binary file. Afterwards, using the function dump(), I loaded each list into the new file. Lastly, I opened the files and used the pickle function load() to load each individual list. From there I could print the lists to the user a number of different ways (simply printing, using a for loop, and by unpacking it.

```
#Create 3 lists

movies = ["Harry Potter", "Lord of the Rings", "Star Wars"]
books = ["Eragon", "Pride and Prejudice", "The Alchemist"]
shows = ["The Good Place", "Parks and Rec", "30 Rock"]

#Create a new file

f = open("FavoritesPickles.dat", "wb")

#Store (A.K.A. - Pickle) lists in new file (use - dump())
pickle.dump(movies, f)
pickle.dump(books, f)
pickle.dump(shows, f)

#Retrieve pickled lists from the new file (load())

f = open("FavoritesPickles.dat", "rb")
Movies = pickle.load(f)
Books = pickle.load(f)
Shows = pickle.load(f)

#Show the lists that have just been unpickled and assigned to variable names

print(Movies)
print(Books)
print(Shows)
print() #added a space

#Unpacking the unpickled lists
print("Favorite Movies:")
for rows in Movies:
    print(rows)
print()

print("Favorite Books:")
for lines in Books:
    print(lines)
print()

print("Favorite TV Shows:")
for items in Shows:
    print(items)
print()

#Unpacking unpickled lists in a different way:
print("Favorite Movies:")
print(Movies[0], Movies[1], Movies[2], sep= " | ")
print()
print("Favorite Books:")
print(Books[0], Books[1], Books[2], sep= " | ")
print()
print("Favorite TV Shows:")
print(Shows[0], Shows[1], Shows[2], sep= " | ")

f.close()

```

**Here is the script running on PythonCharm (Figure 1)**

*Figure 1*

![PickleLoad](https://abeyer13.github.io/ITFnd100-Mod07/PickleLoad.PNG "PickleLoad")

### Error Handling
For error handling, I started with a basic example as I did with pickling. I created two variables (A and B) and one function called C(), which when called, would perform the action A/B. 
I created try except blocks for each variable and function to demonstrate how it works when there is no error, and when there is an error. I created my won custom error messages for each, and then went to show how you can make error messages even more specific by naming them in the except block and assigning the name to a variable. 

```
A = 5+1
B = 0
def C():
    A/B # purposefully creating a function that does not work mathematically

try:
    print(A)
except:
    print("There is an error")
try:
    print(B)
except:
    print("There is an error")
try:
    C()
except:
    print("You cannot divide by 0!") # creating my own custom error message
print()

# Specific Exceptions
print("Using Specific Exceptions provided by Python")
try:
    C()
except ZeroDivisionError as z:
    print("This is my custom error message: You cannot divide by 0 silly goose!")  # my custom error message
    print()
    print("These are some of python's error messages for this specific exception:")
    print(z) # Python's error messages
    print(type(z))
    
```

**Here is an example of the script running in PyCharm (Figure 2)**

*Figure 2*
![ErrorH](https://abeyer13.github.io/ITFnd100-Mod07/ErrHan.PNG "ErrorH")


### Pickling and Error Handling
I created  a simple program where the user would create two lists. The first list would be a list of their favorite movie, book, and tv show. The second list they created would be their answers to two questions. These lists would then be pickle dumped into a file name that they created and would always be assigned with .dat, and then loaded so they could view their answers. 
I created try except blocks for each question and for the file naming portions. See Figure 6-1, 6-2, 6-3, and 6-4 for images of the program running in PyCharm, the command prompt, and in the .dat file. 

```
import pickle

#-Data

FavList1 = []
Answers = []
PickleTable = []

#-Presentation
# Create a list of favorite movie, book, and tv show and surround with try/except

try:
    fmovie = str(input("What is your favorite movie?: "))
    fbook = str(input("What is your favorite book?: "))
    fshow = str(input("What is your favorite TV show?: "))
except:
    print("Do not use characters other than letters and numbers!")

#Simple Math questions with try/exceptions
try:
    Decimal = float(input("What is 5 / 2 ?: "))
    Answer1 = 2.5
    if Decimal == Answer1:
        print("Correct!")
    else:
        print("Incorrect!")

except ValueError as v:
    print("There was an error! You must enter a number!")
    print(v)

try:
    TorF = str(input("True or False: Is the sky blue? "))
    Answer2 = "True"
    if TorF.lower() == Answer2.lower():
        print("Correct!")
    elif TorF.lower() == "t":
        print("Correct!")
    else:
        print("Incorrect, indeed, the sky IS blue!")

except ValueError as v:
    print("You must enter either 'True' or 'False':")
    print(v)


#-Processing
# Pickle the data to file with try/exceptions

FavList1 = [fmovie, fbook, fshow]
Answers = [Decimal, TorF]
PickleTable = [FavList1, Answers]

try:
    nf_name = str(input("What name would you like to give your binary file?: "))
    x = ".dat"
    nfx = nf_name + x   # ensures saved file will be binary
    nf = open(nfx, "wb")
    pickle.dump(PickleTable, nf)
    print()

except Exception as e:
    print("There was an error while pickling your answers!")

#Read back the pickled list
try:
    print("Your answers were saved to the file ", "'", nf_name,x,"' :")
    nf = open(nfx, "rb")
    PickleTable = pickle.load(nf)
    for rows in PickleTable:
        print(rows)
    print()

except FileNotFoundError as e:
    print("Could not find the saved file name.")

#-Leave program

nf.close()
input("Press [enter] to exit:")

```
*Here are more examples of the program running in PyCharm (Figure 3), the command prompt (Figure 4), and saving into a binary file (Figure 5)

**Figure 3**

![PDemo](https://abeyer13.github.io/ITFnd100-Mod07/PandEDemo.PNG "PDemo")

**Figure 4**

![CMD](https://abeyer13.github.io/ITFnd100-Mod07/CMDP.PNG "CMD")


**Figure 5**

![DAT](https://abeyer13.github.io/ITFnd100-Mod07/PandEDAT.PNG "DAT")

## Conclusion
In summary, I was able to create a basic example of pickling, error handling, and the two working together using the Module 07 lecture, the textbook chapter, and the outside resources I discovered on the internet. 

