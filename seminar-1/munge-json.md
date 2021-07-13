---
layout: default
title: Data cleaning
nav_order: 6
parent: Seminar 1
permalink: /seminar-1/munge-json
---

# Data Cleaning

The most important (and least glamorous) part of working with data is creating
a data pipeline. This data pipeline implements a cleaning process where you transform
the data you find in the wild into a dataset that you can use to answer your
research question. Data cleaning includes...

* Joining multiple datasets together.
* Updating values to adhere to a standard. 
    * e.g. survey data may ask for class year and you'll get "2024", "rising sophomore", "senior", etc., 
        and your goal would be to translate them all into four categories: 2022, 2023, 2024, 2025
* Manually splitting up data into categories or sorting data.
* Removing unnecessary data.
* Changing file formats to fit technical requirements.

This is also called "data munging", and is often the longest
part of the research process. When drawing data from an API, however, 
we can expect data to follow strict guidelines. We'll be focusing on removing 
unnecessary data and changing Twitter data from the JSON we receive to a CSV
that we can open in Excel or Google Sheets. Shifting Twitter data from JSON to
CSV can turn a gigabyte of data into a megabyte of useful data, a 1000-fold 
difference.

## Turn JSON into CSV

```python
# import relevant dictionaries
import json
import requests
import pandas as pd

# load JSON from website
r = requests.get('https://raw.githubusercontent.com/kmcelwee/fsi-web-scraping-seminar/main/data/dog_feelings-tweets.json')
all_tweets = json.loads(r.text)

# Cycle through the tweets in that JSON and collect the information we care about
csv_dict = []
for tweet in all_tweets:
  csv_dict.append({
      'timestamp': tweet['created_at'],
      'id': tweet['id'],
      'text': tweet['full_text'],
      'favorite_count': tweet['favorite_count'],
      'retweet_count': tweet['retweet_count'],
      'hashtags': ';'.join([h['text'] for h in tweet['entities']['hashtags']])
  })

# Turn that list of dictionaries into a dataframe and save as a CSV
df = pd.DataFrame(csv_dict)
df.to_csv('dog_feelings-tweets.csv', index=False)
```

Here is a script that turns the JSON gathered from `@dog_feelings` tweets and turns it 
into a CSV with the most basic features like `timestamp` and `favorite_count`. A
good way to build a CSV is to create a list of dictionaries, as shown above. This
would look something like:

```
[
    {
      'timestamp': 'Wed May 10 03:16:19 +0000 2017',
      'id': 862144241782444038,
      'text': "good. night. don't let. the bed bugs. bamboozle",
      'favorite_count': 1856,
      'retweet_count': 376,
      'hashtags': ''
    },
    {
      'timestamp': 'Wed May 10 00:44:59 +0000 2017',  
      'id': 862106154519977984,
      'text': 'a thing. to remember: good things. are good. BUT. bad things. are not good. i think',
      'favorite_count': 1562,
      'retweet_count': 291,
      'hashtags': ''
    }
    ...
]
```

This would create the following data frame:

|timestamp                     |id                |text                                                                               |favorite_count|retweet_count|hashtags|
|------------------------------|------------------|-----------------------------------------------------------------------------------|--------------|-------------|--------|
|Wed May 10 03:16:19 +0000 2017|862144241782444038|good. night. don't let. the bed bugs. bamboozle                                    |1856          |376          |        |
|Wed May 10 00:44:59 +0000 2017|862106154519977984|a thing. to remember: good things. are good. BUT. bad things. are not good. i think|1562          |291          |        |

Notice that each dictionary has the same keys. These are the column names. And
then the associated value with each key is that column's value for the given row.
Getting your head around this structure is fundamental, so if you don't fully 
understand, make sure to not just skim over this.

The code above can be readily reused, as long as you can properly find the path
to the tweet information that you need.

## Data validation

Data validation is an important part of data cleaning, but it can get complicated.
Fundamentally, you want to make sure that the assumptions that you have about your
data set are actually true. The Twitter API is very consistent, so you shouldn't
encounter too many problems, but consider using 
[python's `assert` statement](https://stackoverflow.com/questions/5142418/what-is-the-use-of-assert-in-python))
to double check your assumptions about how the data is structured.

[I've outlined some hurdles](https://cdh.princeton.edu/updates/2021/03/19/mistakes-avoid-when-using-twitter-data-first-time/)
I encountered when working with Twitter data and how I checked for them, but 
chances are, you won't encounter most of them if you keep to small data sets.

## Case Study 1: MTV Internship

You're an intern at MTV and your boss wants to know if
musicians active on Twitter get paid more money than those who aren't active on
Twitter.

🎤 **What are some questions we should ask before pursuing this project?**

<details>
    <summary><a class="btn btn-green">View examples</a></summary>
<ul>
<li>How will we consider artists that aren't on Twitter?</li>
<li>What list of musicians should we consider?</li>
<li>How will I get financial data for all the artists?</li>
<li>Are different genders equally likely to be on Twitter? And what are the gender pay
    disparities in the music industry?</li>
<li>How do we define "active on Twitter"? One tweet a week? A month?</li>
<li>We'll have to manually tie artists to their Twitter accounts. How long will
    that take?</li>
<li>How might outliers distort our calculation? The entertainment industry follows
    the power law, meaning a small number of people make a majority of the money.
    If Beyonce, who doesn't tweet as much, commands 10x the money of Cardi B who 
    tweets a lot, how that one data point skew our numbers?</li>
</ul>
</details>

## Tips

* Data work is both unfulfilling and time consuming. Have a clear research question
    in mind before pursuing any kind of data cleaning process.
* Manually sorting data takes up more time than you think! Always run the calculations
    and weigh whether the research question you want to answer is worth the 
    time that you expect to invest.
