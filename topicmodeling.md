# Goals/Questions for Topic Modeling with Mallet

Adapted from a workshop by Peter Leonard,
Digital Humanities Library, Yale University

## Figure out why we would use Mallet: 
- What is Topic Modeling?
- Why would you use it?
- Pros/Possibilities and Cons/Limitations?
- What humanities questions can we ask?

## Example

## Installing Mallet

## Data:
- What are the charachteristics of data that is amenable to topic modeling?
- What kinds of corpora are not ideal?
- How does the data need to be structured?


## Using Mallet  
- Downloading Mallet
- Topic modeling with Mallet
 
--------

--------



## Figure out why we would use Mallet: 

[Text vs Topic Models Assignment](https://github.com/introdh2016/other/blob/master/textvstopic.md)

Using our readings from last week fro Blevins, Brett, Goldstone and Underwood:

- What is Topic Modeling?
- Why would you use it? 
- Pros/Possibilities and Cons/Limitations?
- What humanities questions can we ask? Provide a few examples.

Let's take a look at Mining the Dispatch.

-------------

## Example

Let's topic model American Quarterly in Mallet. 

Now, it's your turn...

-------------
## Installing Mallet

Mac:

Java Download and Setup:
Mallet is written in Java, a cross-platform language maintained by Oracle. Although named similarly, it has nothing to with Javascript in your web browser.
Depending on your version of Mac OS X and what you’ve installed previously, you may already have Java installed. But most probably will need to install Java before you are able to use Mallet.

How to check
1. Go to Apple -> System Preferences -> You should see Java on the bottom left. 
2. Command Line
- Java version
```sh
java -version  
```
- Java Compiler version
```sh
javac -version
```

Go to this [page](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).
Accept the License Agreement
Download the “Mac OS X x64” version of Java.


Mallet Download and Setup:
Download this file: http://mallet.cs.umass.edu/dist/mallet-2.0.7.tar.gz
Open the Downloads folder in the Finder (usually in the Dock next to the trash)
Open the downloaded file so that it uncompresses into folder called mallet-2.0.7.
Leave the Downloads folder open for right now.
Launch Terminal
The icon is in the Utilities folder, inside the Applications folder
Or search for “Terminal” using Spotlight, the magnifying glass icon in the top righthand corner of the screen
Within Terminal, type cd (with a space). Don’t hit return yet.
Drag the icon of mallet-2.0.7 into the Terminal window. The full “path” to the folder should appear, so that the line reads:
 cd /Users/yourname/Downloads/mallet-2.0.7
Hit return. Your command-line terminal will now be “inside” the mallet folder.
Type ls to get a list of all the files and folders inside the mallet folder.
Back in the Finder, double-click the mallet-2.0.7 folder.  You can now see all the files and folders inside the mallet folder.

PC:
Mallet is written in Java, a cross-platform language maintained by Oracle. Although named similarly, it has nothing to with Javascript in your web browser.
You will most probably need to install Java on your PC. Note that Oracle has stopped supporting Java on Windows XP. 
The Programming Historian has a comprehensive tutorial on how to install the required Java files for use with Mallet. Follow the instructions here:
http://programminghistorian.org/lessons/topic-modeling-and-mallet

----------

## Data 
- What are the charachteristics of data that is amenable to topic modeling?
- What kinds of corpora are not ideal?
- How does the data need to be structured?


Mallet can read in files in many formats, but most people use the program one plain-text file per ‘unit of text’. 
So if I wanted to work with 10,000 newspaper articles, I would have 10,000 plain-text files with one article in each file, 
all in one big directory.

----

### Granular Units of Text

Due to some intricacies of the algorithm, it works best to split up longer texts into “chunks” that approximate semantic units.  For shorter texts (articles, poems, etc), it’s fine to leave them as one unit. But novels probably need to be split up into smaller divisions than chapters. Matt Jockers (University of Nebraska, Lincoln) has done more work with topic-modeling literature than most: “For the books in this corpus, I found through experimentation that 1,000-word chunking was effective.” See his post: 
http://www.matthewjockers.net/2013/04/12/secret-recipe-for-topic-modeling-themes/
or his book:
http://books.google.com/books?id=mPOdxQgpOSUC

You can use a command on Mac OS X or most other Unix systems to split a novel up into roughly 1000-word chunks, by slicing the text into 6 kilobyte sections:

```sh
split -b 6k file.txt file_
```

Replace file.txt with the name of your file, and file_ with the name of the prefix for each smaller part.  

---

### Sample Data

Don’t have your own texts yet, or they’re not in the right format? We have a collection of journal articles from JSTOR that you can use for this workshop. Download this Zip file:

https://drive.google.com/file/d/0B1glRexbIUWoODZoaU5jb1NOcEk/edit?usp=sharing

Once you uncompress the file, you’ll see a number of folders with names such as “avian”, “bible”, etc.  These titles roughly correspond with the subjects of the journals they were pulled from.

If you happen to inspect any of these individual text files, you’ll notice they’re not readable by a human because they’re just lists of word counts. This is how JSTOR can grant access to in-copyright material for text mining purposes. Even though we can’t read them easily, Mallet can still find patterns in word co-occurrence.

----

## Using Mallet

Three basic steps to using Mallet:

1. Make sure you and your data are in the right directory. The data should be in the mallet-2.0.7 folder.  Open your terminal and move into that folder. Use the [command line tutorial](https://github.com/introdh2016/labs/blob/master/commandline.md).

2. The second step is to Import all your text files. The result will be a combined binary file that isn’t much use to you, but that is optimized for further work in Mallet. The token-regex should be modified (or removed) for PC users.

```sh
bin/mallet import-dir --input NAMEOFFOLDERWITHTEXTS/ --output texts.mallet  --token-regex '\p{L}[\p{L}\p{P}]*\p{L}' --keep-sequence --remove-stopwords
```



Example:
```sh
bin/mallet import-dir --input amstudiestxt/ --output texts.mallet  --token-regex '\p{L}[\p{L}\p{P}]*\p{L}' --keep-sequence --remove-stopwords
```

For PC:
```sh
bin\mallet import-dir --input amstudiestxt\ --output texts.mallet --keep-sequence --remove-stopwords
```

3.The third step is to “Train topics” on file you created during the import process. The result will be a list of unlabeled topics, expressed by their significant, or characteristic, words

If you’re using your own data:

```sh
bin/mallet train-topics --input texts.mallet --num-topics 30  --output-topic-keys topic30keys.txt --xml-topic-phrase-report phrase30report.xml --output-doc-topics doc30topics.txt --optimize-interval 10 --inferencer-filename 30inferencer.mallet --random-seed 1 --num-threads 8 
```

If you’re using the JSTOR sample data:

```sh

bin/mallet train-topics --input texts.mallet --num-topics 30  --output-topic-keys topic30keys.txt --xml-topic-report  phrase30report.xml --output-doc-topics doc30topics.txt --optimize-interval 10 --inferencer-filename 30inferencer.mallet --random-seed 1 --num-threads 8 

```

If you’re using the JSTOR sample data with a PC:

```sh

bin\mallet train-topics --input texts.mallet --num-topics 30  --output-topic-keys topic30keys.txt --xml-topic-report  phrase30report.xml --output-doc-topics doc30topics.txt --optimize-interval 10 --inferencer-filename 30inferencer.mallet --random-seed 1 --num-threads 8 

```


Shorter command to change number of topics:

```sh
bin/mallet train-topics --input texts.mallet --num-topics 10 --optimize-interval 10 --random-seed 1 --num-threads 8 
```

Shorter command to change number of topics with a PC:

```sh
bin\mallet train-topics --input texts.mallet --num-topics 10 --optimize-interval 10 --random-seed 1 --num-threads 8 
```

(the difference between these two is that the JSTOR sample data can’t provide multiple-word phrases for each topic, due to the way the data is provided.)

Adding custom stop words:

Create a file (NAMEOFFILE.txt) with your stop words and put it directly in the mallet folder (in our case mallet-2.0.7).

```sh
bin/mallet import-dir --input NAMEOFFOLDERWITHTEXTS/ --output texts.mallet  --token-regex '\p{L}[\p{L}\p{P}]*\p{L}' --keep-sequence --stopword-file NAMEOFFILE.txt 
```


-----

# Next Steps

1. Go to the [assignment information](https://github.com/introdh2016/response1_textanalysis/blob/master/assignment.md). 
2. Make sure to send me your data this weekend!
