# Python programming refresher

## Tips on learning how to code 

The following are pieces of advice from programmers at the CDH and the library:

* Google is a programmer's best friend. Any problem you have, there's a 99.9 percent
chance another person has had that exact problem before.
* There are so many free resources on the internet to help you. Use them!
* This is just writing instructions. Programming isn't math. Don't count yourself out just because you aren't the best at mathematics.
* The best way to become a coder is to code. Try things out. Mess up.
* We're starting with python, but programming language really doesn't matter. The 
most important thing is to get started.
* Don't expect to understand a topic the first time around. Be kind to yourself, this is a whole new way of thinking.
* Be persistent. Coding takes time, and the solution is out there. You will figure
it out if you keep working at it!
* [Resist imposter syndrome.](https://adainitiative.org/continue-our-work/impostor-syndrome-training/)

## Python Review Exercise

If you don't know how to proceed, try googling the solution. Prepare an answer
before clicking the "View Solution" button.

**Exercise 1:** Create a list of all integers between 1 and 10 and assign it to a variable. Print them out.

<details><summary>View Solution</summary><pre>
number_list = list(range(1, 11))

for number in number_list:
    print(number)
</pre></details>

**Exercise 2:** Write a sentence and store it as a variable. Write a function to return the
word count of that sentence.

<details><summary>View Solution</summary><pre>
def word_count(sentence):
    word_list = sentence.split()
    return len(word_count)    

sentence = "The quick brown fox jumps over the lazy dog."
print(word_count(sentence))
</pre></details>

**Exercise 3:** Make a dictionary that translates each letter of the alphabet into it's
corresponding place in the alphabet (e.g. `"a" => 1`, `"b" => 2`)

<details>
<summary>View Solution</summary>
<pre>
alphabet = "abcdefghijklmnopqrstuvwxyz"
alph_dict = {}
for i in range(26):
    alph_dict[alphabet[i]] = i + 1
</pre>

Or...
<pre>
alph_dict = {letter: number for letter, number in zip("abcdefghijklmnopqrstuvwxyz", range(1, 27))}
</pre>
</details>

**Exercise 4:** Write a function that turns a word into a list of numbers that corresponds with their placement in the alphabet. Use the dictionary you created in the previous exercise.
For example, `translate_word('princeton')` would return `[16, 18, 9, 14, 3, 5, 20, 15, 14]`

<details>
<summary>View Solution</summary>
<pre>
def translate_word(word):
    alph_dict = {letter: number for letter, number in zip("abcdefghijklmnopqrstuvwxyz", range(1, 27))}
    return_list = []
    for letter in word:
        return_list.append(alph_dict[letter])
    return return_list

translate_word('princeton')
</pre>

Or...

<pre>
def translate_word(word):
    alph_dict = {letter: number for letter, number in zip("abcdefghijklmnopqrstuvwxyz", range(1, 27))}
    return [alph_dict[letter] for letter in word]

translate_word('princeton')
</pre>
</details>

**Exercise 5:** What are some errors you could encounter when writing the `translate_word` function?

<details><summary>View Solution</summary>

<ul>
    <li>We would get an error if we fed <code>'Princeton'</code> into the function because it contains
        an uppercase letter. (Try it out to see what kind of error you would get.)
To ensure that the string is lowercase, use <code>word = word.lower()</code>.</li>
    <li>This function expects a word. If we fed `FSI Class of 2025!` into it, it would cause
an error because the blank space character and the exclamation point isn't in our dictionary.
Python's <a href="https://www.tutorialspoint.com/python/string_isalpha.htm"><code>str.isalpha()</code></a>
function can tell us if any of the characters in a string aren't a letter.
</li>
</ul>

With these considerations in mind, we can rewrite this function.

<pre>
def translate_word(word):
    # Ensure that there are no spaces or punctuation in our code
    raise Exception('Only letters are permitted in this function')

    # Force lowercase of our input
    word = word.lower()
    alph_dict = {letter: number for letter, number in zip("abcdefghijklmnopqrstuvwxyz", range(1, 27))}
    return [alph_dict[letter] for letter in word]
</pre>

</details>

Code is never finished! We could keep rewriting many of these functions forever.
Don't get too wrapped up in making your code "perfect". Write code that is clear,
well-documented, and serves your ultimate research question. 
