---
layout: default
title: Home
nav_order: 1
permalink: /
---

# Introduction to Web Scraping with Python

A collection of web scraping resources for the 2021 FSI summer course [Humanistic Approaches to Media and Data](https://sifp.princeton.edu/humcf).
If you need to contact me or learn more about my path into becoming a programmer check out my [profile on the Center for Digital Humanities website](https://cdh.princeton.edu/people/kevin-mcelwee/).

## Seminar Goals

Goal of [Seminar 1](seminar-1/index) (3 hours):

* [Review basics of programming with Python.](seminar-1/python)
* [Introduce Google Colab.](seminar-1/colab)
* [Understand data types and file formats (CSV & JSON).](seminar-1/json-and-csv)
* [Log into the Twitter API and execute our first query.](seminar-1/tweepy)
* [Be familiar with rules and limitations of working with APIs.](seminar-1/apis)
* [Trim raw JSON files into a useable CSV file.](seminar-1/munge-json)
* [Talk about potential projects / get inspiration](seminar-1/examples)


Goal of Seminar 2 (3 hours):

* Understand basics of manipulating tabular data with Pandas.
* Draw inspiration from accessible research driven by APIs.
* Generate basic plots with data collected from the previous.

## Tools

We will be working exclusively with Google Colab. In order to interact with the 
Twitter API, we will be using the Python wrapper [`tweepy`](https://docs.tweepy.org/en/stable/).

## Prerequisites

The seminars expect that you already have an approved Twitter Developer Acccount. 
[Apply for access to the Twitter API](https://developer.twitter.com/en/apply-for-access).
A basic understanding of Python is also expected.

## Coding Resources

* [YouTube Python Tutorials](https://www.youtube.com/results?search_query=python+tutorials)
* [O'Reilly Learn](https://learning.oreilly.com/home/): A collection of every programming
book you'll ever need. A subscription is free with your netID and offers video lectures,
introductory books, and answers to [frequently asked programming questions.](https://learning.oreilly.com/answers/search/)
* [Free programming books](https://github.com/EbookFoundation/free-programming-books/blob/master/books/free-programming-books.md#python):
    Tons of programming materials are free online. It doesn't matter too much how you get
    started, as long as you just start!

## Useful Links

* [Twitter Documentation](https://developer.twitter.com/en/docs)
* [Tweepy Documentation](https://docs.tweepy.org/en/stable/)
* [StackOverflow](https://stackoverflow.com/)
* [Google Colaboratory](https://colab.research.google.com)
* [YouTube Python Tutorials](https://www.youtube.com/results?search_query=python+tutorials)
* [Practice coding Python online](https://www.hackerrank.com/domains/python)
* [YouTube Pandas Tutorials](https://www.youtube.com/results?search_query=pandas+tutorials)
* [Introduction to Cultural Analytics & Python](https://melaniewalsh.github.io/Intro-Cultural-Analytics/welcome.html)
* [Coursera Python Web Data course](https://www.coursera.org/learn/python-network-data)

## Vocabulary

* Web scraping: Collecting data from the internet in an automated way
* API: Application Programming Interface. In the context of web scraping, it is a system used by web site owners to monitor and control how data exits their platform.
* HTTP Methods: (e.g. POST, GET, UPDATE, DELETE) For web scraping we're only interested in what are called "GET requests", a request made to the website's server for information. With that request, you include the type of information you need, and usually an authorization token.
* Rate limiting: The speed limit placed on programmers that prevents them from making too many requests at once and overworking a site's servers. This varies from site to site.
* JSON: JavaScript Object Notation. A lightweight data format used throughout the web. If you receive a response through an API, it will almost certainly be in this format.
* Wrapper: In web scraping a wrapper is a library of code that translates the API into a language that you're comfortable programming in.
* Python: The language most often used for writing quick scripts for web scraping and data analysis. If you are using an API, there's a good chance that there's a wrapper in Python. Python has also been embraced by the data science community and has many libraries to support data cleaning and visualization.

## Thank you 

Thank you to [Kavita Kulkarni](https://cdh.princeton.edu/people/kavita-kulkarni/) for her guidance in constructing these seminars. And thank you to Melanie Walsh for basically [creating this course first](https://melaniewalsh.github.io/Intro-Cultural-Analytics/welcome.html) 😄