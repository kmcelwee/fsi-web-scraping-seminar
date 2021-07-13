---
layout: default
title: File formats
nav_order: 3
parent: Seminar 1
permalink: /seminar-1/json-and-csv
---

# Working with different file formats

## What is a CSV?

If you've ever worked with a spreadsheet, you know what a CSV is. A CSV is just
a standardized way of storing data in a table. CSV stands for "Comma Separated
Value", meaning literally each value in row is separated by a comma. Another 
popular format is TSV or "Tab Separated Value". It's the same as a CSV, but 
just separates values by tabs. This is especially useful when there are a lot
of commas in your data. Here's what a CSV looks like, (Fortune 100 companies 
and their Twitter handles):

```
Corporation,URL,Rank,Handle,Sector
Walmart,https://twitter.com/Walmart,1,Walmart,Retailing
Amazon.com,https://twitter.com/amazon,2,amazon,Retailing
Exxon Mobil,https://twitter.com/exxonmobil,3,exxonmobil,Energy
```

That data when loaded into Excel or Google Sheets would look like this:

| Corporation | URL                            | Rank | Handle     | Sector    | 
|-------------|--------------------------------|------|------------|-----------| 
| Walmart     | https://twitter.com/Walmart    | 1    | Walmart    | Retailing | 
| Amazon.com  | https://twitter.com/amazon     | 2    | amazon     | Retailing | 
| Exxon Mobil | https://twitter.com/exxonmobil | 3    | exxonmobil | Energy    | 

CSVs are important because they are non-priorietary and plain text. Therefore
they can easily be parsed and created by the software programs we write. We'll
get explain how to parse CSVs when we learn about the 
[Pandas library next week.](../seminar-2/introduction-to-pandas)

One drawback of CSVs is that they are limited to one value for each row and each column. 
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
<summary><a class="btn btn-blue">View an example tweet JSON from Twitter</a></summary>
<script src="https://gist.github.com/kmcelwee/e09c9f03930886b5958fca287e648e36.js"></script>
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

Feel free to copy the following into a Colab notebook and mess around with the `tweet`
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

💡 **Exercise: Can you make a list of the hashtags with the example tweet provided above?** 

<details>
<summary><a class="btn btn-purple">View Solution</a></summary>
<script src="https://gist.github.com/kmcelwee/6e8e20b4321bf2fe2e5ce7a7f171e396.js"></script>
</details>
