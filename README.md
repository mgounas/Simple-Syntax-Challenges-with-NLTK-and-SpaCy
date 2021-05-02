# Simple-Syntax-Tasks-with-NLTK-and-SpaCy

The Natural Language Toolkit, abbreviated as NLTK, is very useful for beginners to Natural Language Processing (NLP). NLTK can be installed following the steps here: https://www.nltk.org/install.html. 

It includes several features that help you prepare your data quickly and efficiently while programming in Python which is available to download here: https://www.python.org/downloads/.

In your preferred text editor, you can test if your installation of NLTK was successful with:

      import nltk
      
In order to use all of the features available to you through NLTK, download **all-nltk** after running the following:

      nltk.download()
      
   

# Tokenization
Tokenization is the process by which data is divided into subparyts to be more easily analyzed. These parts are called *tokens* in NLP. While tokens often map to the words of sentences directly, tokens can also represent whole sentences within a larger body of text. Tokens are useful for identifying patterns in your data and are an important first step for many projects; rarely can we reach conclusions about a sentence, paragraph, or paper as a whole if we cannot make conclusions about its parts. Tokens are our building blocks for text classfication, sentiment analysis, and more.

Tokenization is simplified with NLTK's **tokenize** module, which includes two sub-modules *sentence_tokenize()* and *word_tokenize()*.

## sent_tokenize()
The *sent_tokenize()* sub-module is used to divide a paragraph or body of text larger than a single sentence into individual sentences. In this case, each of the resulting tokens will be a whole sentence.

Let's take as a simple example the famous line said by Carrie Fisher as Princess Leia Organa in *Star Wars: Episode IV - A New Hope*:

      "Help me, Obi-Wan Kenobi. You're my only hope."
      
In tokenizing this quote into sentences, we should expect to find two sentences as a result:

      (1) 'Help me, Obi-Wan Kenobi.'
      
      (2) 'You're my only hope.'

As speakers, we can easily identify where the natural sentence break, but a computer needs to be taught the nuances that we take for granted. 

If we were to describe the intuition we have in identifying the end of one sentence and the start of the next, we might say that in written text: 
  
      the first sentence must end with sentential punctuation,
      it must also be followed a space,
      and the second sentence must start with an uppercase letter. 

We could include a regular expression to account for these conditions, so why would it be better to use NLTK instead?

While those three pieces certainly describe the break within "Kenobi. You're" which is our desired sentence break, it also could describe "me, Obi-Wan" depending on how we define *sentential punctuation*.

We could resolve this simply by excluding commas from our category for *sentential punctuation*, but we may find that we need commas to be included in another aspect of our project. 

In manually dividing paragraphs into sentences, it's not usually as simple as two sentences with a clear separation. In larger data sets, there can be some aspects that we don't expect that may render our simple approach unsuccessful and insufficient.

NLTK's *sent_tokenizer()* can help with simple tasks, but more importantly, it can make dividing up much larger bodies of text simple.

In your preferred text editor, the 
      

## word_tokenize()
