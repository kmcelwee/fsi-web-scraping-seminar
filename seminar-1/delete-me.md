# Python programming refresher

## Tips on learning how to code

## Quick Exercises

## Resources for Learning Python 


# Introduction to Colab

## Executing your first code block

## Shortcuts

## Useful links



# Working with different file formats

## What is a CSV?

If you've ever worked with a spreadsheet, you know what a CSV is. A CSV is just
a standardized way of storing data in a table. CSV stands for "Comma Separated
Value", meaning literally each value in row is separated by a comma. Another 
popular format is TSV or "Tab Separated Value". Here's what a CSV looks like,
(Fortune 100 companies and their Twitter handles):

```CSV
Corporation,URL,Rank,Handle,Sector
Walmart,https://twitter.com/Walmart,1,Walmart,Retailing
Amazon.com,https://twitter.com/amazon,2,amazon,Retailing
Exxon Mobil,https://twitter.com/exxonmobil,3,exxonmobil,Energy
```

And then if loaded into Excel or Google Sheets, it'd look like this:

| Corporation | URL                            | Rank | Handle     | Sector    | 
|-------------|--------------------------------|------|------------|-----------| 
| Walmart     | https://twitter.com/Walmart    | 1    | Walmart    | Retailing | 
| Amazon.com  | https://twitter.com/amazon     | 2    | amazon     | Retailing | 
| Exxon Mobil | https://twitter.com/exxonmobil | 3    | exxonmobil | Energy    | 

CSVs are important because they are non-priorietary and plain text. Therefore
they can easily be parsed and created by the software programs we write. We 

CSVs are limited because they require one value for each row and each column. 
If we were trying to add a `Hashtags Used` column, we might get ten or fifteen
values in each row. If, for example, Walmart used the hashtags "#retail", 
"#IndependenceDay", and "#savings", we could combine with some kind of unique
character like a semicolon: `retail;IndependenceDay;savings`. Or we could
use JSON...

## What is JSON?

Whenever scraping the web, you will inevitably get a JSON (often pronounced
like Jason) response. It's arguably the most popular data format on the web.
JSON stands for "JavaScript Object Notation", but you really don't need to 
remember this. It's a combination of nested lists and dictionaries, the same
kind of lists and dictionaries that you'd use in python.

<details>
<summary>Toggle to see an example tweet JSON from Twitter:</summary>
<pre><code>
{
  "created_at": "Mon Jul 27 19:00:10 +0000 2020",
  "id": 1287825123974750208,
  "id_str": "1287825123974750208",
  "full_text": "There are ten years to go until the @WHO 2030 goal of eliminating #HCV and our actions are more important now than ever. With #WorldHepatitisDay around the corner, hear what Professor Jacob George thinks it\u2019ll take to achieve elimination: https://t.co/SlbgJxJzDk",
  "truncated": false,
  "display_text_range": [
    0,
    238
  ],
  "entities": {
    "hashtags": [
      {
        "text": "HCV",
        "indices": [
          66,
          70
        ]
      },
      {
        "text": "WorldHepatitisDay",
        "indices": [
          126,
          144
        ]
      }
    ],
    "symbols": [],
    "user_mentions": [
      {
        "screen_name": "WHO",
        "name": "World Health Organization (WHO)",
        "id": 14499829,
        "id_str": "14499829",
        "indices": [
          36,
          40
        ]
      }
    ],
    "urls": [],
    "media": [
      {
        "id": 1287825098561527811,
        "id_str": "1287825098561527811",
        "indices": [
          239,
          262
        ],
        "media_url": "http://pbs.twimg.com/ext_tw_video_thumb/1287825098561527811/pu/img/-GrgzBLpAkhh-lqq.jpg",
        "media_url_https": "https://pbs.twimg.com/ext_tw_video_thumb/1287825098561527811/pu/img/-GrgzBLpAkhh-lqq.jpg",
        "url": "https://t.co/SlbgJxJzDk",
        "display_url": "pic.twitter.com/SlbgJxJzDk",
        "expanded_url": "https://twitter.com/abbvie/status/1287825123974750208/video/1",
        "type": "photo",
        "sizes": {
          "thumb": {
            "w": 150,
            "h": 150,
            "resize": "crop"
          },
          "large": {
            "w": 512,
            "h": 512,
            "resize": "fit"
          },
          "medium": {
            "w": 512,
            "h": 512,
            "resize": "fit"
          },
          "small": {
            "w": 512,
            "h": 512,
            "resize": "fit"
          }
        }
      }
    ]
  },
  "extended_entities": {
    "media": [
      {
        "id": 1287825098561527811,
        "id_str": "1287825098561527811",
        "indices": [
          239,
          262
        ],
        "media_url": "http://pbs.twimg.com/ext_tw_video_thumb/1287825098561527811/pu/img/-GrgzBLpAkhh-lqq.jpg",
        "media_url_https": "https://pbs.twimg.com/ext_tw_video_thumb/1287825098561527811/pu/img/-GrgzBLpAkhh-lqq.jpg",
        "url": "https://t.co/SlbgJxJzDk",
        "display_url": "pic.twitter.com/SlbgJxJzDk",
        "expanded_url": "https://twitter.com/abbvie/status/1287825123974750208/video/1",
        "type": "video",
        "sizes": {
          "thumb": {
            "w": 150,
            "h": 150,
            "resize": "crop"
          },
          "large": {
            "w": 512,
            "h": 512,
            "resize": "fit"
          },
          "medium": {
            "w": 512,
            "h": 512,
            "resize": "fit"
          },
          "small": {
            "w": 512,
            "h": 512,
            "resize": "fit"
          }
        },
        "video_info": {
          "aspect_ratio": [
            1,
            1
          ],
          "duration_millis": 23200,
          "variants": [
            {
              "content_type": "application/x-mpegURL",
              "url": "https://video.twimg.com/ext_tw_video/1287825098561527811/pu/pl/CP2MxUPgcPIgHHVc.m3u8?tag=10"
            },
            {
              "bitrate": 832000,
              "content_type": "video/mp4",
              "url": "https://video.twimg.com/ext_tw_video/1287825098561527811/pu/vid/512x512/4ZytClsHjo1Xu3Ov.mp4?tag=10"
            },
            {
              "bitrate": 432000,
              "content_type": "video/mp4",
              "url": "https://video.twimg.com/ext_tw_video/1287825098561527811/pu/vid/320x320/GazJ0V7Ou1aV3R0I.mp4?tag=10"
            }
          ]
        },
        "additional_media_info": {
          "monetizable": false
        }
      }
    ]
  },
  "source": "<a href=\"https://www.spredfast.com/\" rel=\"nofollow\">Khoros</a>",
  "in_reply_to_status_id": null,
  "in_reply_to_status_id_str": null,
  "in_reply_to_user_id": null,
  "in_reply_to_user_id_str": null,
  "in_reply_to_screen_name": null,
  "user": {
    "id": 531892451,
    "id_str": "531892451",
    "name": "AbbVie",
    "screen_name": "abbvie",
    "location": "Global",
    "description": "AbbVie's global handle featuring biopharmaceutical news & updates managed by our corp digital team. Review our guidelines here: http://t.co/qwZuFRpxk5",
    "url": "https://t.co/IibBdsMrEg",
    "entities": {
      "url": {
        "urls": [
          {
            "url": "https://t.co/IibBdsMrEg",
            "expanded_url": "http://www.AbbVie.com",
            "display_url": "AbbVie.com",
            "indices": [
              0,
              23
            ]
          }
        ]
      },
      "description": {
        "urls": [
          {
            "url": "http://t.co/qwZuFRpxk5",
            "expanded_url": "http://bit.ly/AbbVieSocialGuidelines",
            "display_url": "bit.ly/AbbVieSocialGu\u2026",
            "indices": [
              128,
              150
            ]
          }
        ]
      }
    },
    "protected": false,
    "followers_count": 64331,
    "friends_count": 498,
    "listed_count": 899,
    "created_at": "Wed Mar 21 03:42:59 +0000 2012",
    "favourites_count": 1786,
    "utc_offset": null,
    "time_zone": null,
    "geo_enabled": false,
    "verified": true,
    "statuses_count": 6293,
    "lang": null,
    "contributors_enabled": false,
    "is_translator": false,
    "is_translation_enabled": false,
    "profile_background_color": "071D49",
    "profile_background_image_url": "http://abs.twimg.com/images/themes/theme14/bg.gif",
    "profile_background_image_url_https": "https://abs.twimg.com/images/themes/theme14/bg.gif",
    "profile_background_tile": false,
    "profile_image_url": "http://pbs.twimg.com/profile_images/1278082623886278656/pIvFxKYq_normal.jpg",
    "profile_image_url_https": "https://pbs.twimg.com/profile_images/1278082623886278656/pIvFxKYq_normal.jpg",
    "profile_banner_url": "https://pbs.twimg.com/profile_banners/531892451/1591220916",
    "profile_link_color": "071D49",
    "profile_sidebar_border_color": "FFFFFF",
    "profile_sidebar_fill_color": "EFEFEF",
    "profile_text_color": "333333",
    "profile_use_background_image": false,
    "has_extended_profile": false,
    "default_profile": false,
    "default_profile_image": false,
    "following": null,
    "follow_request_sent": null,
    "notifications": null,
    "translator_type": "none"
  },
  "geo": null,
  "coordinates": null,
  "place": null,
  "contributors": null,
  "is_quote_status": false,
  "retweet_count": 2,
  "favorite_count": 5,
  "favorited": false,
  "retweeted": false,
  "possibly_sensitive": false,
  "lang": "en"
}
</code>
</pre>
</details>

As you can see, there's *a lot* of information for just a single tweet, and 
representing that information in a CSV would be nearly impossible. JSON makes it
easy to communicate complex datasets in a plain text format.

### Parsing JSON in Python

Again, JSON is just a combination of dictionaries and lists. To open a JSON
file and get certain values, you'd treat it as you would any list or dictionary.

You can load a JSON file using Python's `json` library:

```python
import json

json_file_path = 'tweet.json'
with open(json_file_path) as f:
    tweet = json.load(json_file_path)

```

Feel free to copy the following code into a Colab notebook and mess around with the `tweet`
variable. Here are some examples of getting certain values:

```python
import json
import requests

r = requests.get('https://raw.githubusercontent.com/kmcelwee/fsi-web-scraping-seminar/main/data/tweet.json')
tweet = json.loads(r.text)
# To get the text of this tweet
tweet['full_text']
# To get the users mentioned in this tweet
tweet['entities']['user_mentions'][0]['screen_name']
```

It can sometimes be difficult to figure out the path to a variable in JSON, so
some trial and error is predictable.

**Exercise: Can you make a list of the hashtags?** 
<details>
    <summary>Toggle to see answer</summary>

```python
import json
import requests

r = requests.get('https://raw.githubusercontent.com/kmcelwee/fsi-web-scraping-seminar/main/data/tweet.json')
tweet = json.loads(r.text)
hashtag_list = []
for hashtag in tweet['entities']['hashtags']:
  hashtag_list.append(hashtag['text'])

print(hashtag_list)
```
</details>



# Introduction to Tweepy

Let's log into the Twitter API and execute our first query!


# Introduction to working with APIs

Before going crazy with Tweepy, it's important to understand what we just did, 
its limitations, and how to apply what we learned to any API

## Wrappers

## Rate Limiting

## Data Limiting

## Secret Keys

## Other popular APIs


# Scrape a Twitter user

Let's combine all the code we've just learned to scrape the JSON from a single 
Twitter user.

## Execute code



# Turn JSON into CSV

## Why turn JSON into a CSV?

## What fields do we want to keep?


