---
layout: default
title: "Intro to Pandas"
nav_order: 3
parent: Seminar 2
permalink: /seminar-2/introduction-to-pandas
---

1. TOC
{:toc}

# Introduction to Pandas 🐼

If you need to perform any kind of calculation on tabular data, use [Pandas](https://pandas.pydata.org/).
Pandas is a library that helps programmers query, perform calculations on, and
clean CSVs. If you get nothing else from these seminars, learning Pandas is probably the most
useful investment of your time. Regardless of what you end up doing, you're 
inevitably going to work with data in a table, and Pandas is a lot faster 
than Excel or Google Sheets.

Pandas has been to space. It's used on Wall Street and the Federal Reserve. 
It's used by digital humanitists and data journalists. It's powerful, and 
thankfully, if you know how to code, it's pretty straightforward to learn!

## What are data frames and series?

A "data frame" is a word you'll hear a lot, and it's why the most common variable
used to store a CSV is `df`. It's simply the term used by Pandas (as well as other
data manipulation software) 

In Pandas vernacular, "series" just means "column". A data frame contains multiple
series objects.

## Read and write a CSV

For all our examples we'll be using our CSV of `@dog_feelings` tweets. In 
order to load a CSV you just need to provide a path to a CSV file, whether
that's on your computer or on the internet.

```python
url = 'https://raw.githubusercontent.com/kmcelwee/fsi-web-scraping-seminar/main/data/dog_feelings-tweets.csv'
df = pd.read_csv(url)
```

After changing your CSV, you may want to save it as a file, for that, just use
the [`.to_csv()`](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.to_csv.html)
method, where you just provide a `filename` where you 
want to save your data frame. (Just as a warning though, this will overwrite
anything with the same name!)

```python
df.to_csv('dog_feelings-tweets-v2.csv', index=False)
```

In general, just add `index=False`. It's not worth going into the details here, but
put succinctly, you'll get an extra column if you don't include that flag.

## Selecting columns

To view all columns:

```python
df.columns
```

To work with one column:

```python
# Select the 'retweet_count' column
df['retweet_count']
```

To work with a subset of multiple columns:

```python
# Select the 'retweet_count' and 'favorite_count' columns
df[['retweet_count', 'favorite_count']]
```

## Selecting rows

In order select a subset of rows we often want to filter on a certain condition.
For example, what if we wanted to only get tweets that had
more than 1300 favorites, we could make what's called a "mask".
First we need to create an array of True and False (boolean) values:

```python
df['favorite_count'] > 1300
```

The output of which would be:

```
0        True
1        True
2        True
3        True
4        True
        ...  
1124    False
1125    False
1126    False
1127    False
1128     True
```

You can then apply this as mask to the data frame by using square brackets
like so:

```python
df[df['favorite_count'] > 1300]
```

This will select only the rows where `df['favorite_count'] > 1300` is True.

## Create a new column

All you need to do to create a new column is define it. For example, if we
wanted to add favorites and retweets together for some reason, just
add them together and set them equal to a new column:

```python
df['retweets_plus_favorites'] = df['retweet_count'] + df['favorite_count']
```

There are many ways to apply functions to columns to manipulate them, 
but with this baseline knowledge, I trust you can Google appropriately.
If you want to learn more, check out this YouTube lecture:

* [Python Pandas Tutorial (Part 6): Add/Remove Rows and Columns From DataFrames](https://www.youtube.com/watch?v=HQ6XO9eT-fc)

## Working with different datatypes

To see the different datatypes in our `df`, type `df.dtypes`. 
You'll get the following result:

```
timestamp         object
id                 int64
text              object
favorite_count     int64
retweet_count      int64
hashtags          object
```

We're oversimplifying here, but `int64` means that the column contains an integer
and the `object` columns here are strings.

When we want to filter by date though (which we often want to do), we need to 
parse the timestamp column as a "datetime" object. You do this with the
`pd.to_datetime` function. You can you can overwrite the `timestamp` column
like so:

```python
df['timestamp'] = pd.to_datetime(df['timestamp'])
```

Now we can create new columns like "month" or "day-of-week" using the [`.dt`](https://pandas.pydata.org/docs/reference/api/pandas.Series.dt.html)
accessor.

```python
df['month'] = df['timestamp'].dt.month
df['day-of-week'] = df['timestamp'].dt.dayofweek
```

## Most common functions

### [`.shape`](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.shape.html)

Often you'll want to get the number of rows or columns in a data frame. You can
access this info using the `.shape` attribute:

```python
# return a list that gives the shape of the data frame
df.shape
# >>> (1129, 6)

# number of rows in data frame
df.shape[0]
# number of columns in a data frame
df.shape[1]
```

### [`.head()`](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.head.html) & [`.tail()`](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.tail.html)

If you just want to see the first few or last few rows of a data frame, use the
[`.head()`](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.head.html) and 
[`.tail()`](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.tail.html)
methods.

```python
# Show the first 5 rows of a df
df.head()
# Show the first 10 rows of a df
df.head(10)
# Show the last 5 rows of a df
df.tail()
# Show the last 10 rows of a df
df.tail(10)
```

### [`.sort_values()`](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.sort_values.html)

Sort a dataframe by the given column.

```python
# Sort df by the column 'favorite_count'
df.sort_values('favorite_count')
# Sort df by the column 'favorite_count' in ascending order
df.sort_values('favorite_count', ascending=False)
```

### [`.count()`](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.count.html)

If called on a data frame, the count function gives the number of non-null values
in all columns. If called on a series, the count function will return the number of non-null values
in that column.

```python
# How many non-null values are in each column?
df.count()

# How many non-null values are in the column 'hashtags'
df['hashtags'].count()
```

### [`.mean()`](https://pandas.pydata.org/docs/reference/api/pandas.Series.mean.html), [`.median()`](https://pandas.pydata.org/docs/reference/api/pandas.Series.median.html), [`.min()`](https://pandas.pydata.org/docs/reference/api/pandas.Series.min.html), [`.max()`](https://pandas.pydata.org/docs/reference/api/pandas.Series.max.html), and [`.quantile()`](https://pandas.pydata.org/docs/reference/api/pandas.Series.quantile.html)

When provided numerical data, you will inevitably want to find various statistics
on that distribution. Here are some of the most popular:

```python
# Average number of retweets per tweet
df['retweet_count'].mean()
# Median number of retweets per tweet
df['retweet_count'].median()
# Minimum number of retweets per tweet
df['retweet_count'].min()
# Max number of retweets per tweet
df['retweet_count'].max()
# 25th quantile of retweets per tweet
#  (meaning 25 percent of tweets have fewer retweets than this number)
df['retweet_count'].quantile(.25)
```

**Question: Why might you prefer median instead of mean as a way to describe your data?**

<details><summary><a class="btn btn-purple">View Solution</a></summary>
<p>Medians are less sensitive to outliers. Meaning that one large or really small 
numbers won't dramatically change your calculation.</p>

<p>This is most common when talking about incomes. Especially in the US, economists
will discuss "median household income". This is because the "mean household income"
is significantly higher because economic inequality. Mean household income
would be a poor reflection of the actual state of the economy.</p>

<p>For example, if you and three friends made $30k, $45k, $45k, and $50k/year, the mean
would be $45k/year. If Jeff Bezos was added to the mix, the mean just rose
to a few billion, not because you are any richer. The median, however, stayed the same
at $45k.</p>
</details>

### [`.str.contains()`](https://pandas.pydata.org/docs/reference/api/pandas.Series.str.contains.html)

This method returns true if the strings in your column contain a given substring. 
This is useful when filtering rows in our dataset. For example, if we wanted to know
what tweets contain the word "gooooob"

```python
df[df['text'].str.contains('gooooob')]
```

### [`.groupby`](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.groupby.html)

`.groupby()` isn't the most straightforward function, but it is very useful in 
many contexts. Many times you'll want to group categorical data together, and 
run a calculation for each of those groups. For example, if you wanted
to know what the average number of favorites is per day of the week, here's
what that would look like:

```python
# Ensure that the "timestamp" column is appropriately parsed as a datetime
df['timestamp'] = pd.to_datetime(df['timestamp'])
# Create a "day-of-week" column 
df['day-of-week'] = df['timestamp'].dt.dayofweek
# Groupby "day-of-week", select the "favorite_count" column and get the mean
df.groupby('day-of-week')['favorite_count'].mean()
```

The output should look like this:

```
day-of-week
0    65683.261538
1    77871.142857
2    70649.446927
3    74367.388235
4    48420.922619
5    60879.256198
6    70115.652893
Name: favorite_count, dtype: float64
```

`groupby()` is a function that can be difficult to get a handle on, so I 
won't expand too much further. I recommend the following video if you need
to learn more in order to answer your research question:

* [Python Pandas Tutorial (Part 8): Grouping and Aggregating - Analyzing and Exploring Your Data](https://www.youtube.com/watch?v=txMdrV1Ut64)

## Plotting with Pandas

Thankfully, plotting with Pandas (as long as you're keeping things simple) is
pretty straightforward. Just add [`.plot()`](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.plot.html) to whatever series you're working with.
The default is a line chart, but if you want a bar chart, just set `kind='bar'`.
To set a title, just set `title='My awesome graph'`. Everything else, just google
"How to change X in a graph with Pandas". Pandas is built on a library called [Matplotlib](https://matplotlib.org/)
so familiarizing yourself with that library may be helpful, but in general, you
shouldn't need to do too much outside of just changing that plot function.

## 🐕 Exercises

If you don’t know how to proceed, try googling the solution. Prepare an answer before clicking the “View Solution” button.

**1. How many tweets are were sent in 2019? What about August 2019?**

<details><summary><a class="btn btn-purple">View Solution</a></summary>
    <script src="https://gist.github.com/kmcelwee/834dc9345e7911ac2cb53b7145d70e15.js"></script>
</details>

**2. What was the average number of retweets that a tweet would get in 2017? 2018? 2019? ...etc**

<details><summary><a class="btn btn-purple">View Solution</a></summary>
    <script src="https://gist.github.com/kmcelwee/905e52bd77be3d56e7bc7f14d231f57f.js"></script>
</details>

**3. How many tweets contain the word 'gooooob'?**

<details><summary><a class="btn btn-purple">View Solution</a></summary>
    <script src="https://gist.github.com/kmcelwee/3437ce8553327bf9201624a475c7dff4.js"></script>
</details>

**4. How many tweets are in all caps?**

<details><summary><a class="btn btn-purple">View Solution</a></summary>
    <script src="https://gist.github.com/kmcelwee/88a0b9c2fec75b8a6b4bcde17e4cba40.js"></script>
</details>

**5. What's the average length of a sentence in these tweets?**

<details><summary><a class="btn btn-purple">View Solution</a></summary>
</details>

**6. What's the average ratio of favorites to retweets?**

<details><summary><a class="btn btn-purple">View Solution</a></summary>
    <script src="https://gist.github.com/kmcelwee/fa388c21774627a474c92ebf30b7e70e.js"></script>
</details>
