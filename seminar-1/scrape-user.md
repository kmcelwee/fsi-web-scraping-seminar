# Scrape a Twitter user

Let's combine all the code we've just learned to scrape the JSON from a single 
Twitter user.

## Execute code

You've logged into the Twitter API, now run a query to scrape. You just need to 
insert your 

```python
import tweepy # https://github.com/tweepy/tweepy
import csv

# Twitter API credentials
consumer_key = ""
consumer_secret = ""

def get_all_tweets(screen_name):
    # Twitter only allows access to a users most recent 3240 tweets with this method
    auth = tweepy.OAuthHandler(consumer_key, consumer_secret)
    api = tweepy.API(auth)
    
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
        <li>We're using python's CSV library instead of Pandas to write the CSV. If you're not analyzing the data and just want to make a CSV, using this library can be useful.</li>
    </ul>
</details>