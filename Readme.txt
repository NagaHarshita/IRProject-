Implemented a cosine similarity ranking for the github issues document collection(100k docs).

Corpus-QWERT-Part2.zip - contains all the documents 

## Overview
The code performs the following functions for document retrieval on the GitHub issues documents collection. 
1. Preprocesses the data in the text collection (stop words removal, stemming, removing punctuations etc.)
2. Creates an inverted index for looking up relevant documents for each word in the vocabulary of the document collection
3. Assigns weights to each word in the documents/queries by using TF-IDF weighting scheme
4. Performs cosine similarity 

## Running the code  
*Python 3 and nltk are required to run the code*

### From the command line/ terminal
source venv/bin/activate (activate the virtual environment)
python3 code.py (run the code)
Enter the query 

### Files 
* code.py - contains the code for the data 
* PostingList.txt - the inverted index is stored in this file 
* stopwords.txt - common stop words collected 
* Corpus - contains all the 100k docs 


## Detailed List of Functionalities Implemented

Class DataPreProcessing: 
- Has variables tokens, df 
- Abstracts all the functions which does preprocessing 

    #### 1. tokenize_and_remove_punctuations:
    The function accepts the text data as a parameter and does the following operations:
    a. Removes the punctuations from the text data
    b. Removes numbers from the data
    c. Converts the data to lower case
    d. Tokenizes the words from the text 

    #### 2. get_stopwords: 
    The function reads the common English stop words from the file stopwords.txt and then returns them as a list

    #### 3. remove_stop_words: 
    The function takes in tokenized words and removes stop words from it and the words which are smaller than 2 characters in length

    #### 4. get_vocabulary: 
    This function parses all the words from the document collection and returns a vocabulary of all the unique words from the collection

    #### 5. stem_words: 
    The function takes in a list of tokens and returns a list of stemmed words using NLTKs PorterStemmer

    #### 6. dataExtraction:
    The function takes a list of tuples generated by read_data and then performs the following functions:
        Extracting the data 
        -Reads the data from the corpus files, stores it in a dataframe 
        -Modifies the column data 

        Preprocessing 
        a. tokenizes and removes puntuations
        b. removes stop words
        c. stems words
        d. removes stop words after stemming and words shorter than 2 characters

Class InvertedIndex:

    ####1.updateTokensData:
    - Calculates the total no. of docs, tokens 

    ####2.InvIndex:
    - Calculates the inverted index with the dict and stores in the posting list 
    - Merges after every 50 docs 

    ####3. TermFrequency
    - Calculates the doc frequency for each word 
    - format in storing the inverted index in posting 
    word(doc frequency): [docname(term freq), docname(term freq), ---]
 
Class Query:

    ####1. preProcess
    Preprocessing 
        a. tokenizes and removes puntuations
        b. removes stop words
        c. stems words
        d. removes stop words after stemming and words shorter than 2 characters

    ####2. Scores
    - Computes the scores for the tokens present in the query after preprocessing 
    - This uses tf-idf to compute the scores 
    - Performs cosine similarity 

    ####3. printScores
    - Prints the top 10 docs with their score 
    - Gives the url of the github issue matching the query 
