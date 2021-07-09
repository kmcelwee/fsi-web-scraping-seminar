# Python programming refresher

## Tips on learning how to code 

The following are pieces of advice from programmers at the CDH and the library:

* You won't get this the first time around, and that's okay! This website isn't
going anywhere, so feel free to return to it as reference.
* Google is a programmer's best friend. Any problem you have, there's a 99.9 percent
chance another person has had that exact thought before.
* There are so many free resources on the internet to help you.
* This is just writing instructions. It's unforgiving if a single character
is out of place.
* Don't just listen, code. The best way to become a coder is to code!
* We're starting with python, but programming language really doesn't matter.
* Be kind to yourself, this is a whole new way of thinking.
* Programming isn't math. Don't count yourself out just because you aren't
the best at mathematics.
* Be persistent. Coding takes time, and the solution is out there. You will figure
it out if you keep working at it! But also taking a step away from your work for
a walk can also 
* [Resist imposter syndrome](https://adainitiative.org/continue-our-work/impostor-syndrome-training/)

## Python Review Exercise

Before looking at the solution, practice googling the answers. Learning the 
vocabulary and learning how to piece together a Google search is half the battle.

1. Make a list of all numbers between 1 and 10 and assign it to a variable. Print them out.

<details><summary>View Solution</summary><pre>
number_list = list(range(1, 11))

for number in number_list:
    print(number)
</pre></details>

1. Write a sentence and store it in a variable. Write a function to return the
word count of that sentence.

<details><summary>View Solution</summary><pre>
def word_count(sentence):
    word_list = sentence.split()
    return len(word_count)    

sentence = "The quick brown fox jumps over the lazy dog."
print(word_count(sentence))
</pre></details>

1. Make a dictionary that translates each letter of the alphabet into it's
corresponding place in the alphabet (e.g. "a" => 1, "b" => 2)

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

1. Use the dictionary you created above to translate a function that turns a word into a list of numbers.
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
</pre>

Or...

<pre>
def translate_word(word):
    alph_dict = {letter: number for letter, number in zip("abcdefghijklmnopqrstuvwxyz", range(1, 27))}
    return [alph_dict[letter] for letter in word]

translate_word('princeton')
</pre>
</details>

What are things you should consider when you make this function?

<details><summary>View Solution</summary>

<ul>
    <li>Expect the word is lowercase, we would get an error if we fed <code>'Princeton'</code> into the function.
See what kind of error you would get. If you wanted you could set <code>word = word.lower()</code> to
make sure that all the characters are lowercase.</li>
    <li>This function expects a word. If we fed `FSI Class of 2025!` into it, it would cause
an error because the blank space character and the exclamation point isn't in our dictionary.
You can use raise an error if a user inputs the wrong. 
Python's <a href="https://www.tutorialspoint.com/python/string_isalpha.htm"><code>str.isalpha()</code></a>
can tell us if any of the characters in a string aren't a letter.
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

Code is never finished! We could expand this function forever. So don't get
too wrapped up in making your code "perfect". Write code that tries
to avoid easy mistakes, and serves your ultimate research question. If you share
code with others, however, make sure to document your assumptions

</details>
