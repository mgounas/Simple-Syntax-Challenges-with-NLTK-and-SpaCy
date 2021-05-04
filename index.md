# Simple-Syntax-Tasks-with-NLTK

The Natural Language Toolkit, abbreviated as NLTK, is very useful for beginners to Natural Language Processing (NLP). NLTK can be installed following the steps here: https://www.nltk.org/install.html. 

It includes several features that help you prepare your data quickly and efficiently while programming in Python which is available to download here: https://www.python.org/downloads/.

In your preferred text editor, you can test if your installation of NLTK was successful with:

      import nltk
      
In order to use all of the features available to you through NLTK, download **all-nltk** after running the following:

      nltk.download()
      
   

# Tokenization

*Tokenization* is the process by which data is divided into subparyts to be more easily analyzed. These parts are called *tokens* in NLP. While tokens often map to the words of sentences directly, tokens can also represent whole sentences within a larger body of text. Tokens are useful for identifying patterns in your data and are an important first step for many projects; rarely can we reach conclusions about a sentence, paragraph, or paper as a whole if we cannot make conclusions about its parts. Tokens are our building blocks for text classfication, sentiment analysis, and more.

Tokenization is simplified with NLTK's **tokenize** module, which includes two sub-modules *sent_tokenize()* and *word_tokenize()*.

## sent_tokenize()

The *sent_tokenize()* sub-module is used to divide a body of text larger than a single sentence into individual sentences. In this case, each of the resulting tokens will be a whole sentence.

Let's take as a simple example the famous line said by Carrie Fisher as Princess Leia Organa in *Star Wars: Episode IV - A New Hope*:

      'Help me, Obi-Wan Kenobi. You're my only hope.'
      
In tokenizing this quote into sentences, we should expect to find two sentences as a result:

      (1) 'Help me, Obi-Wan Kenobi.'
      
      (2) 'You're my only hope.'

As speakers, we can easily identify where the natural sentence break is, but a computer needs to be taught the nuances that we take for granted. 

If we were to describe the intuition we have in identifying the end of one sentence and the start of the next, we might say that in written text: 
  
      the first sentence must end with sentential punctuation,
      it must also be followed a space,
      and the second sentence must start with an uppercase letter. 

We could include a regular expression to account for these conditions, so why would it be better to use NLTK instead?

While those three pieces certainly describe the break within "Kenobi. You're" which is our desired sentence break, it also could describe "me, Obi-Wan" depending on how we define *sentential punctuation*.

We could resolve this simply by excluding commas from our category for *sentential punctuation*, but we may find that we need commas to be included in another aspect of our project. For example, while people do not intend to write run-on sentences, it's very common for them to be written with several commas, and a task may be to revise run-on sentences. In this case, we would need to consider commas, so they cannot always be excluded from our understanding of *sentential punctuation*.

It is very possible to end up with several of these exceptions, which, when handled manually, can get confusing and can require a lot of effort to remedy. Instead, we can use NLTK for sentence tokenization, since it is already optimized for this purpose.

In your preferred text editor, we can use NLTK to tokenize Princess Leia's line for us:
      
      from nltk import sent_tokenize
      
      line      = "Help me, Obi-Wan Kenobi. You're my only hope."
      sentences = nltk.sent_tokenize(line)
      
      print("sentences: ", sentences)

The output should look like this:
      
      sentences: ['Help me, Obi-Wan Kenobi.', 'You're my only hope.']
      
Here, we can see that the *sent_tokenize()* successfully identified the two sentences and overlooked the potential issue with the comma.

NLTK's *sent_tokenize()* can help with simple tasks like this example, but more importantly, it can make dividing up much larger bodies of text a simple task because it successfully accounts for variation in text.

## word_tokenize()

Many tasks will rely on individual words from sentences. The sentences may be a result of passing a paragraph through the *sent_tokenizer()* first, or they may be the original structure of your input, but, importantly, we are interested in dividing each of these sentences into smaller parts. The tokens that result from tokenizing a whole sentence are usually words and sentential punctuation. 

We'll use another simple example to illustrate *word_tokenize()*. This one is a line spoken by Tom Holland as Spider-Man in *Avengers: Infinity War*:

      'Mr. Stark, I don't feel so good.'
      
When we tokenize a sentence into its parts, we want individual words and sentential punctuation to be individual tokens. We could simply split the sentence on the whitespaces between each word and further identify sentential punctuation like periods and commas and make those individual tokens, as well.

There are, however, two points of interest in this example that could get tricky if we approached this task manually.

First, we can look at the contraction *don't*. The standard approach for handling contractions is to separate the contracted portion *n't* from the rest of the word *do*. One reason for this is that *n't* is common among other contractions like *aren't* and *isn't*, T we can consider it as an individual token and tally how many contractions are present in a document by counting how many instances of *n't* are present. We could include a regular expression to identify the contracted portion from the rest of the word, but this is adding another condition to be cautious of as we tokenize our sentences. Each time something new appears, we would need to add another condition.

The other word that should give us pause is *Mr.* since it is typical to tokenize sentential puncutation independent of the rest of the sentence. Following that logic, we would think that *Mr* should be one token and *.* should be another, but as speakers and readers of the language, we know this isn't ideal. So, this is another potential hiccup in manually tokenizing the sentence, especially since the immediate environment of the period after *Mr* is not dramatically different from the environment for the period after *good*. Both periods are in the final position of the word, and if we had more sentences in the quote, they would be followed by a whitespace, as well. 

Both of these concerns are handled well by NLTK's *word_tokenize()*, and we can illustrate this with our example from *Avengers: Infinity War*:
      
      from nltk import word_tokenize
      
      line   = 'Mr. Stark, I don't feel so good.'
      tokens = word_tokenize(line)
      
      print("tokens: ", tokens)
      
The output of this should be:

      tokens:  ['Mr.', 'Stark', ',', 'I', 'do', "n't", 'feel', 'so', 'good', '.']
      
Here, we can see that the NLTK *word_tokenize()* was successful in tokenizing this sentence in the most natural way and accounted for the two potential issues we outlined above.

The *sent_tokenizer()* and *word_tokenizer()* from the Natural Language Toolkit make tokenization efficient and simple to use.

# Stemming and Lemmatization

*Stemming* and *lemmatization* are processes by which words are simplified. These can be helpful in identifying a consistent sentiment when an author has written several words with the same roots but different forms. 

Both *stemming* and *lemmatization* can establish relationships among words, but they behave differently. Critically, *stemming* can be faster but it risks generating stems that are not real words. While *lemmatization* can be slower, it considers context and only generates real words.

## PorterStemmer()

*Stemming* often removes the endings of words without considering what will be left over. In some cases, this is not much of a concern, and the speed with which the system can stem may be preferred. The *PorterStemmer()* is an option we can use in for stemming words.

A simple concept where stemming is useful would be removing the plural ending on plural forms of nouns.

Let's take the following pairs of singular and plural forms of nouns:
      
      supervillian ~ supervillians
      superhero ~ superheroes
      
Knowing that the plural marker in English is *-s* we can easily determine that the stemmed form of *supervillains* will be *supervillian*. We might expect the stemmer to remove only the *-s* from both plural forms above, which would result in *superheroe* which would be incorrect. Let's test it:

      from nltk.stem import PorterStemmer
      porter_stemmer = PorterStemmer()
      
      words = ["supervillain", "supervillains", "superhero", "superheroes"]

      for word in words:
          stem = porter_stemmer.stem(word)
          print("The stem for", word, "is", stem)
          
The output is:

      The stem for supervillain is supervillain
      The stem for supervillains is supervillain
      The stem for superhero is superhero
      The stem for superheroes is superhero

The stemmer got it right! It can, however, be the case that the stemmer generate stems that are not real words:

      from nltk.stem import PorterStemmer
      porter_stemmer = PorterStemmer()
      
      words = ["cry", "crying", "cries", "cried"]

      for word in words:
          stem = porter_stemmer.stem(word)
          print("The stem for", word, "is", stem)
          
The output here is:

      The stem for cry is cri
      The stem for crying is cri
      The stem for cries is cri
      The stem for cried is cri
      
So, when using the *PorterStemmer()*, you need to be aware of potential outputs like these. If this is not desirable for the project you are working on you should consider *lemmatization*.

## WordNetLemmatizer()

*Lemmatization* is similar to *stemming* but a key difference is that anything generated through *lemmatization* will be a real word. Let's take the set of examples with the output *cri* from the *PorterStemmer()* section above and apply the *WordNetLemmatizer()* instead:

      from nltk.stem import WordNetLemmatizer
      word_net_lemmatizer = WordNetLemmatizer()

      words = ["cry", "crying", "cries", "cried"]

      for word in words:
            lemma = word_net_lemmatizer.lemmatize(word)
            print("The lemma for", word, "is", lemma)

The output now is:

      The lemma for cry is cry
      The lemma for crying is cry
      The lemma for cries is cry
      The lemma for cried is cried

These may be easier to work with than the output from the *PorterStemmer()* since they are real words. 
