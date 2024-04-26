# Study-on-Project-Gutenberg-Corpus-using-NLP-AI-Applications

# Introduction 

In this study, we have examined Project Gutenberg Tool from the NLTK package using NLP (Natural Language Processing) toread text, interpret it, and determine which parts are important from the tool. Natural language processing (NLP) is a branch of artifi cial intelligence within computer science that focuses on helpingcomputers to understand the way that humans write and speak (Díaz, 2022). Over the years, we have used NLP in the form ofemail fi lters, smart assistants, search results, predictive text, language translation, digital phone calls, data analysis, and textanalytics (8 Natural Language Processing (NLP) Examples, n.d.). In the steps below we will take you through the process of examining the output, and describe each element.

# Analysis 

The analysis is divided into two parts - This section aims to take you through the process of both parts of the analysis. 1) Install, analyzing Gutenberg Corpus Tool.Analyzing two modals with the largest span of relative and their frequencies. 2) Analysis of Kennedy's speech.

Gutenberg contains some 25,000 free electronic books hosted at http://www.gutenberg.org/. We can install the NLTK package and use theGutenberg corpus. You will install it by running the following in the computer terminal:


Step 1 Downloaded and installed the Gutenberg corpus tool in the NLTK package, using the following commands

import nltk
nltk.download('gutenberg')

Step 2 load the Gutenberg corpus

from nltk.corpus import gutenberg
from collections import Counter
import pandas as pd

Step 3 The following code is used for reading all the project files that represent the gutenberg file. This lists down all the text files present in the corpus gutenberg.

nltk.corpus.gutenberg.fileids()
['austen-emma.txt', 'austen-persuasion.txt', 'austen-sense.txt', 'bible-kjv.txt', 'blake-poems.txt', 'bryant-stories.txt', 'burgess-busterbrown.txt', 'carroll-alice.txt', 'chesterton-ball.txt', 'chesterton-brown.txt', 'chesterton-thursday.txt', 'edgeworth-parents.txt', 'melville-moby_dick.txt', 'milton-paradise.txt', 'shakespeare-caesar.txt', 'shakespeare-hamlet.txt', 'shakespeare-macbeth.txt', 'whitman-leaves.txt']

Step 4 Using the texts in the corpus we create a table displaying relative frequencies with which “modals” (can, could, may,might, will, would, and should) which appear in all texts provided in the corpus

modals = [
"can","could","may","might","will","would","should"]
print
(modals)
['can', 'could', 'may', 'might', 'will', 'would', 'should']


frequency = {}
for file id in gutenberg.fileids():
  words = gutenberg.words(fileid)
  fd = nltk.FreqDist(words)
  frequency[fileid] = {modal: fd[modal]/fd.N() for modal in modals}

df = pd.DataFrame(frequency).T
df.index.name = "Text"
df.columns.name ="Modals"
print(df)

(The model displays all the values)

# Explore the words in "The Ball and The Cross"
gk = gutenberg.words('chesterton-ball.txt')
print(' '.join(gk[:100]))
[ The Ball and The Cross by G . K . Chesterton 1909 ] I . A DISCUSSION SOMEWHAT IN THE AIR The flying ship of Professor L


# Explore the words in "The Sense and Sensibility"
austen = gutenberg.words('austen-sense.txt')
print(' '.join(austen[:100]))
[ Sense and Sensibility by Jane Austen 1811 ] CHAPTER 1 The family of Dashwood had long been settled in Sussex .

Step 5 We selected two modals with the largest span of relative frequencies for which we choose "will" to be the most usedand "should" to be the least. We chose "Sense and Sensibility" by Jane Austen as the text that uses "will" the most, and "The Balland The Cross" by G . K . Chesterton 1909 as the text that uses "will" the least.

Used of the word in both texts by examining the relative frequencies of those modals.

text1 ="austen-sense.txt"
text2 ="chesterton-ball.txt"

frequency = {}
for fileid in[text1, text2]:
  words = gutenberg.words(fileid)
  fd = nltk.FreqDist(words)
  frequency[fileid] = {modal: fd[modal]/fd.N() for modal in modals}

df = pd.DataFrame(frequency).T
df.index.name ="Text"
df.columns.name ="Modals"
print(df)

# Conclusion 

It can be observed that "will" is used more frequently in "Sense and Sensibility" Sense and Sensibility by Jane Austen 1811 than in "The Ball andthe Cross is a novel by G. K. Chesterton" which can be a result of showing extreme intention or determination which is more in the context ofSense and Sensibility. Meanwhile, in the case of "The Ball and the Cross" which is also novel by G. K. Chesterton the modal verbs may beinfrequent.

# Exploring the inaugural corpus

Step 1 Download the inaugural package and explored the inaugural fi les in the data from 1789 to 2021.

nltk.download('inaugural')
from nltk.corpus import inaugural
inaugural.fileids() 

'1793-Washington.txt', '1797-Adams.txt', '1801-Jefferson.txt', '1805-Jefferson.txt', '1809-Madison.txt', '1813-Madison.txt', '1817-Monroe.txt', '1821-Monroe.txt', '1825-Adams.txt', '1829-Jackson.txt', '1833-Jackson.txt', '1837-VanBuren.txt', '1841-Harrison.txt', '1845-Polk.txt', '1849-Taylor.txt', '1853-Pierce.txt', '1857-Buchanan.txt', '1861-Lincoln.txt', '1865-Lincoln.txt', '1869-Grant.txt', '1873-Grant.txt', '1877-Hayes.txt', '1881-Garfield.txt', '1885-Cleveland.txt','1901-McKinley.txt', '1905-Roosevelt.txt', '1909-Taft.txt', '1913-Wilson.txt', '1917-Wilson.txt', '1921-Harding.txt', '1925-Coolidge.txt', '1929-Hoover.txt', '1933-Roosevelt.txt', '1937-Roosevelt.txt', '1941-Roosevelt.txt', '1945-Roosevelt.txt', '1949-Truman.txt', '1953-Eisenhower.txt', '1957-Eisenhower.txt', '1961-Kennedy.txt', '1965-Johnson.txt', '1969-Nixon.txt', '1973-Nixon.txt', '1977-Carter.txt', '1981-Reagan.txt', '1985-Reagan.txt', '1989-Bush.txt', '1993-Clinton.txt', '1997-Clinton.txt', '2001-Bush.txt', '2005-Bush.txt', '2009-Obama.txt', '2013-Obama.txt', '2017-Trump.txt','2021-Bidentxt']

nltk.corpus.inaugural.words("1961-Kennedy.txt")
['Vice', 'President', 'Johnson', ',', 'Mr', '.', ...]

file_id ='1961-Kennedy.txt'

# Get the raw text of Kennedy's speech
kennedy_speech = inaugural.raw(file_id)

# Print the first 1000 characters of the speech
print(kennedy_speech[:1000])

# we explored the 10 most frequently used long words, which are citizens, president, americans,generation, forebears, revolution, committed, powerful, supporting, themselves.


kennedy = inaugural.words('1961-Kennedy.txt')
long_words = [word for word in kennedy if len (word) >7]
freq_dist = nltk.FreqDist(long_words)
top10 = freq_dist.most_common(10)
print(top10)

('citizens', 5), ('President', 4), ('Americans', 4), ('generation', 3), ('forebears', 2), ('revolution', 2), ('committed',

word that has the largest number of synonyms is "supporting".

from nltk.corpus import wordnet
synonyms = {} 
for word in top10:
  syns = set()
  for synset in wordnet.synsets(word[0]):
    for syn in synset.lemmas():
      syns.add(syn.name())
synonyms[word[0]] = syns

max_synonyms = max(synonyms, key=lambda k: len(synonyms[k]))
print(max_synonyms)

We explored the 10 words frequently used and its relative hyponyms which are listed belowand the word is most hypnyms is Americans

citizens: citizen
President: President, United_States_President, prexy, Chief_Executive, chairman, chair, chairperson, president,President_of_the_United_States, chairwoman
Americans: American_English, American, American_language
generation: contemporaries, genesis, coevals, propagation, multiplication, generation
forebears: forbear, forebear
revolution: gyration, revolution, rotation
committed: intrust, perpetrate, committed, entrust, consecrate, institutionalise, invest, pull, trust, send, commit, institutionalize,devote, attached, practice, confi de, dedicate, give, put, charge, place
powerful: potent, muscular, powerful, herculean, brawny, mightily, hefty, knock-down, mighty, right, sinewy
supporting: substantiate, plump_for, plunk_for, patronize, patronage, put_up, back_up, hold_up, endorse, support, bear, abide,stomach, indorse, keep_going, confi rm, affi rm, supporting, bear_out, sustain, stand, digest, tolerate, corroborate, endure,stick_out, subscribe, suffer, encouraging, underpin, hold, brook, fend_for, patronise, load-bearing, defend, back
themselves:

# The word with most hyponyms: Americans

# Conclusion 

We can conclude from both the sections NLP focusses on extrapolating the words that are frequently used in a speech,content, passage or relative material. This helps the management team make informed decisions towards, and understandwhat part infl uences decision making.
