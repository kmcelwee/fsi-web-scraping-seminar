---
layout: default
title: "Python programming refresher"
nav_order: 1
parent: Seminar 1
permalink: /seminar-1/python
---

# Python programming refresher

1. TOC
{:toc}

## Tips on learning how to code 

The following are pieces of advice from programmers at the CDH and the library:

* Google is a programmer's best friend. Any problem you have, there's a 99.9 percent
chance another person has had that exact problem before.
* There are so many free resources on the internet to help you. Use them!
* This is just writing instructions. Programming isn't math. Don't count yourself out just because you aren't the best at mathematics.
* The best way to become a coder is to code. Try things out. Mess up.
* We're starting with python, but programming language really doesn't matter. The 
most important thing is to get started.
* Don't expect to understand anything the first time around. Be kind to yourself, this is a whole new way of thinking.
* Be persistent. Coding takes time, and the solution is out there. You will figure
it out if you keep working at it!
* [Resist imposter syndrome.](https://adainitiative.org/continue-our-work/impostor-syndrome-training/)

## Exercises

If you don't know how to proceed, try googling the solution. Prepare an answer
before clicking the "View Solution" button.

**Exercise 1:** Create a list of all integers between 1 and 10 and assign it to a variable. Print them out.

<details><summary><a class="btn btn-purple">View Solution</a></summary>
<script src="https://gist.github.com/kmcelwee/ae02565da0d7f02ab91eb6215807748e.js"></script>
</details>

**Exercise 2:** Write a sentence and store it as a variable. Write a function to return the
word count of that sentence.

<details><summary><a class="btn btn-purple">View Solution</a></summary>
<script src="https://gist.github.com/kmcelwee/a78dd62fd5a06e0060e86a804f11f11a.js"></script>
</details>

**Exercise 3:** Make a dictionary that translates each letter of the alphabet into it's
corresponding place in the alphabet (e.g. `"a" => 1`, `"b" => 2`)

<details>
<summary><a class="btn btn-purple">View Solution</a></summary>
<script src="https://gist.github.com/kmcelwee/0775fa1537f7d63a55b799e83d3a8db2.js"></script>
</details>

**Exercise 4:** Write a function that turns a word into a list of numbers that corresponds with their placement in the alphabet. Use the dictionary you created in the previous exercise.
For example, `translate_word('princeton')` would return `[16, 18, 9, 14, 3, 5, 20, 15, 14]`

<details>
<summary><a class="btn btn-purple">View Solution</a></summary>
<script src="https://gist.github.com/kmcelwee/02f969d68fe82b75efd12a1bb833f67d.js"></script>
</details>

**Exercise 5:** What are some errors you could encounter when writing the `translate_word` function?

<details><summary><a class="btn btn-purple">View Solution</a></summary>

<ul>
    <li>We would get an error if we fed <code>'Princeton'</code> into the function because it contains
        an uppercase letter. (Try it out to see what kind of error you would get.)
To ensure that the string is lowercase, use <code>word = word.lower()</code>.</li>
    <li>This function expects a word. If we fed <code>'FSI Class of 2025!'</code> into it, it would cause
an error because the blank space character and the exclamation point isn't in our dictionary.
Python's <a href="https://www.tutorialspoint.com/python/string_isalpha.htm"><code>str.isalpha()</code></a>
function can tell us if any of the characters in a string aren't a letter.
</li>
</ul>

With these considerations in mind, we can rewrite this function.

<script src="https://gist.github.com/kmcelwee/73351c7636036f1e70de98e345af5da2.js"></script>
</details>

Code is never finished! We could keep rewriting many of these functions forever.
Don't get too wrapped up in making your code "perfect". Write code that is clear,
well-documented, and serves your ultimate research question. 
