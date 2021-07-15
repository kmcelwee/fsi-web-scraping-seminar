---
layout: default
title: Intro to Tweepy
nav_order: 4
parent: Seminar 1
permalink: /seminar-1/tweepy
---

# Introduction to Tweepy

1. TOC
{:toc}

## Twitter Advanced Search

Before using the Twitter API, consider [Twitter Advanced Search](https://twitter.com/search-advanced?lang=en). You can often
get a lot of answers before writing a line of code! "Site-specific syntax" is
not unique to Twitter. Check out useful ways to query [Reddit](https://www.reddit.com/wiki/search/)
or [Google](https://support.google.com/websearch/answer/2466433?hl=en). Because
working with APIs can be difficult and time-consuming, especially when first
starting out, it's best to informally test your hypotheses with these search tools as you form your
research question. And as we'll discuss soon, this search API is the only way you can get certain data without paying.

## First API Login

Let's log into the Twitter API and execute our first query! (Don't worry, I'll
explain everything about how APIs work next. First let's just get data onto
our computer.)

First, we need your API keys. Log in to the developer portal.
Create a new project under "Projects & Apps". Name your project
`fsi-seminar` and answer that your purpose is to learn the Twitter API. 
After filling out the questionnaire, you'll be met with the alphanumeric keys
generated for you to use the Twitter API. Copy both the "API Key" and the
"API Secret Key" into a new Colab notebook. (You won't need to your Authentication
Token. This is used when you need special privileges, like posting tweets from
your account.)

```python
import tweepy # https://github.com/tweepy/tweepy

consumer_key = "" # put your information here!
consumer_secret = "" # put your information here!

auth = tweepy.OAuthHandler(consumer_key, consumer_secret)
api = tweepy.API(auth)

# get tweet ID
tweet = api.get_status(1412424266763603968)
tweet.text
```

And there you go! You should see the text from a tweet from NASA. 
**What do you notice about how the text is formatted?**

# Scrape a profile

If you need to scrape a profile, you are limited to the latest 3200 tweets.
If you've set up th API (and placed it into the variable `api`) you can 
easily run the following code and get the latest 3200 tweets exported to 
a CSV. 

```python
def get_all_tweets(screen_name):
    alltweets = []  
    new_tweets = api.user_timeline(screen_name = screen_name, count=200)
    alltweets.extend(new_tweets)

    oldest = alltweets[-1].id - 1
    
    # keep grabbing tweets until there are no tweets left to grab
    while len(new_tweets) > 0:
        new_tweets = api.user_timeline(screen_name = screen_name, count=200, max_id=oldest)
        alltweets.extend(new_tweets)
        oldest = alltweets[-1].id - 1
        print(f"...{len(alltweets)} tweets downloaded so far")
    
    # transform the tweepy tweets into a 2D array that will populate the csv 
    outtweets = [[tweet.id_str, tweet.created_at, tweet.text] for tweet in alltweets]
    
    # write the csv  
    with open(f'new_{screen_name}_tweets.csv', 'w') as f:
        writer = csv.writer(f)
        writer.writerow(["id","created_at","text"])
        writer.writerows(outtweets)

get_all_tweets('SCREEN_NAME')  # Change me
```

**What do you notice about how this CSV was created differently than other code
we've looked at?**

<details> 
    <summary><a class="btn btn-purple">View some takeaways</a></summary>
    <ul>
        <li>Because we're using tweepy, we can get to the text and timestamp information straight from what tweepy calls a Tweet object. You can't do this with JSON, but tweepy already parsed the most important features and making them easily accessible.</li>
        <li>We're using python's <a href="https://docs.python.org/3/library/csv.html">csv library</a> instead of Pandas to write the CSV. If you're not analyzing the data and just want to make a CSV, using this library can be useful.</li>
    </ul>
</details>

## Get profile information

```python
user = api.get_user('SCREEN_NAME')
```

🪐 **Exercise: Get the location of NASA through their Twitter profile.**

<details><summary><a class="btn btn-purple">View Solution</a></summary>
<script src="https://gist.github.com/kmcelwee/d23a027129b0b4f2026afb519a8873c5.js"></script>
</details>

## Collecting tweets by hashtag

Twitter's Search API is similar to their advanced search feature, in that 
they use the same syntax for both. In fact, it's probably best to
construct your query with their UI, test it there, and then paste it into
your code once your sure that's what you want.

```python
# Paris's lat: 48.8566, long:2.3522, radius: 6mi
search_query = '#covid geocode:48.8566,2.3522,6mi min_faves:10'

# Get 10 items. If items() is left blank, it will get as many as possible,
#  but that command may take a while to execute.
tweets_cursor = tweepy.Cursor(api.search, q=search_query).items(10)
tweets = [tweet for tweet in tweets_cursor]
```

[See this query in the Twitter UI.](https://twitter.com/search?q=%23covid%20geocode%3A48.8566%2C2.3522%2C6mi%20min_faves%3A10&src=typed_query&f=live){: .btn}

Here I'm plugging in Paris's geocode and a radius and minimum number of favorites
to 10. Similar to the Advanced Search UI, you can look up by "Latest" or "Popular", 
and/or filter by language.

If I wanted to collect all tweets to the President that mention climate
change, the query would look something like:

```python
search_query = '"climate change" OR "global warming" to:POTUS'
```

[See this query in the Twitter UI.](https://twitter.com/search?q=%22climate%20change%22%20OR%20%22global%20warming%22%20to%3APOTUS&src=typed_query&f=live){: .btn}

Here I've used the `OR` operator to look for either the phrase `climate change`
or `global warming` directed to the account `POTUS`.

There are endless examples. The main limitation is the time window. 
The search API is only valid for the past 7 days on the
free tier. Twitter is currently updating its API, however, so this may change.
Further, if you pursue Twitter analysis with a professor or in a more, you can
apply for academic access, which provides some search functionality for free.

* [Read about tweepy search.](https://docs.tweepy.org/en/v3.5.0/api.html#help-methods)
* [Read about how these search strings can be constructed.](https://developer.twitter.com/en/docs/twitter-api/tweets/search/integrate/build-a-query)

🦠 **Exercises:**
* What could you learn by comparing English tweets in Paris with French tweets in Paris concerning Covid-19?
* What would those queries look like?
* Given the limitations we've discussed what wouldn't you be able to determine?

