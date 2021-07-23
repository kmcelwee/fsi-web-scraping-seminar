---
layout: default
title: "Analysis Tools"
nav_order: 4
parent: Seminar 2
permalink: /seminar-2/analysis-tools
---

# Analysis Tools for Natural Language Processing

Natural Language Processing (or NLP), is a broad field in data science that
incorporates text generation, parsing, and analysis. We will be largely focused
in compressing text into numbers. Put simply, numbers are easier to work with
than text. Often, our goal is to somehow strip out some of the complexity inherent to text
data in order to reveal broad trends.

## Sentiment analysis

Sentiment analysis is a process of attributing a blob of text to a value
between -1 and 1, where -1 is the most negative statement, and 1 is the most 
positive statement. For example, "I had a great day today." would be
fed into the sentiment analysis function and would probably return something
like 0.8, and "I'm not feeling well." may return -0.4.

Below, we use the python library [`nltk`](https://www.nltk.org/) (Natural Language ToolKit).
This is a free, classic library that is often used for basic analysis.

```python
import pandas as pd
from nltk.sentiment import SentimentIntensityAnalyzer
import nltk

# Download the VADER sentiment analysis model
nltk.download('vader_lexicon')

sia = SentimentIntensityAnalyzer()

def get_sentiment(text):
  return sia.polarity_scores(text)['compound']

df['sentiment'] = df['text'].apply(get_sentiment)
```

Another library you can use is [`spaCy`](https://spacy.io/). I suggest that
you read the documentation for both tools to see what seems easier to you
and what helps you better answer your research question.

**🤖 Question: Sentiment analysis algorithms are machine learning models like any other. What potential pitfalls must you consider when using this library?**

## Word frequency

"Just count the words" sounds simple, but any student of a foreign language 
knows that it can't be that simple.
our language. Computers have a tough time parsing our language, so we have
a whole bunch of systems to help us calculate word frequency. We won't go
too indepth, but here are some concepts you should be familiar with.

* **tokenization**: The process of taking a blob of text, and splitting it up, (often into words).
* **stemming**: The process of taking words and chopping off the ending, hoping to collapse
words down to their simpler parts ("boy's" -> "boy")
* **lemmatization**: The process of conjugating words to the root, "swim", "swam", and "swum" would
all be collapsed down to "swim". This is usually the better path, but harder
to implement.
* **stopwords**: Common words that don't add a lot of value to analysis, e.g. "a",
"the", "and". When performing word frequency analysis, you often want to strip
these out.
* **TF-IDF**: Term-frequency inverse document frequency. It's a normalized way
of talking about term frequency, allowing researchers to look for actually 
distinct words while stripping out common words. If comparing chapters within 
Life of Pi, "tiger" is probably equally likely to be found in all chapters, 
whereas the word "ship" occurs more often at the beginning and end.

[Voyant](https://voyant-tools.org/) is a go-to tool for performing a lot of this analysis.
(Researchers were often performing the same tasks over and over again, 
so they just made a tool to analyze and visualize everything for them.)

Just paste your text into the website, and it will create a nice dashboard
with different word frequency charts and a word cloud. Too much text, however,
will cause it to error.

These online tools are great, but once you need something just slightly outside
the scope of what they offer, there's nothing you can do. The great
thing about programming is that you're not necessarily limited by what tools
exist, but by whether the tool can be built!

## Useful links

* [Stanford explanation of stemming and lemmatization](https://nlp.stanford.edu/IR-book/html/htmledition/stemming-and-lemmatization-1.html)
* [Voyant](https://voyant-tools.org/)
