---
layout: default
title: Intro to Tweepy
nav_order: 4
parent: Seminar 1
permalink: /seminar-1/tweepy
---

# Introduction to Tweepy

Let's log into the Twitter API and execute our first query! 

## Twitter Advanced Search

Before using the Twitter API, consider Twitter Advanced Search. You can often
get a lot of answers before writing a line of code! Other forms of site-specific syntax 
can also be useful

## First API Login

First, we need your authentication token. Log in to the developer portal.
Create a new project under "Projects & Apps". Name your project
`fsi-seminar` and answer that your purpose is to learn the Twitter API. 
After filling out the questionaire, you'll be met with the alphanumeric keys
generated for you to use the Twitter API. Copy both the "API Key" and the
"API Secret Key" into a new Colab notebook.


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

And there you go! You should see the text from a tweet from NASA. What
do you notice about how the text is formatted?

# Scrape a profile

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

get_all_tweets('SCREEN_NAME')
```

What do you notice about how this CSV was created differently than other code
we've looked at?

<details> 
    <summary>Toggle to see some answers:</summary>
    <ul>
        <li>Because we're using tweepy, we can get to the text and timestamp information straight from what tweepy calls a Tweet object. You can't do this with JSON, but tweepy already parsed the most important features and making them easily accessible.</li>
        <li>We're using python's <a href="https://docs.python.org/3/library/csv.html">csv library</a> instead of Pandas to write the CSV. If you're not analyzing the data and just want to make a CSV, using this library can be useful.</li>
    </ul>
</details>

# Get profile information

```python
user = api.get_user('SCREEN_NAME')
```

🪐 **Exercise: Get the location of NASA through their Twitter profile.**

<details><summary><a class="btn btn-purple">View Solution</a></summary>
<script src="https://gist.github.com/kmcelwee/d23a027129b0b4f2026afb519a8873c5.js"></script>
</details>

# Collecting tweets by hashtag

Read more about the search parameters [here](https://docs.tweepy.org/en/v3.5.0/api.html#help-methods).

```python
tweet_list = api.search('#pride')
for tweet in tweet_list:
    print(tweet.text)
```

You can read more about how these search strings can be constructed 
[here](https://developer.twitter.com/en/docs/twitter-api/tweets/search/integrate/build-a-query).
But tweepy isn't very reliable with complex searches. By default this command will return 
ten or so tweets, but by setting the `count` parameter, you
can gather more.
