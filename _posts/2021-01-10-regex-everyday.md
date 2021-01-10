---
published: true
comments: true
layout: post
title: RegEx Everyday [Part 1]
author: Riad Afridi Shibly
categories: programming
tags: [personalities, regex]
image: regex-p1.jpg
---

## What is Regular Expression?
If you're here and you don't know anything about regular expression let's start with a few examples. What do we do with a regular expression? Simple, we search in a string or we replace in a pattern with another one.

### Let's see some use cases
You've got a file containing a large amount of text and you want to find all the emails, or at least all the strings which look like emails. The difference between string search and regex search is that when you search with the string `find` method you normally look for strings that are exactly the same. But with the regular expression, you search for a string that is similar to the pattern you're searching for or maybe you're looking for similar kinds of strings. You don't wanna find the exact phone number but rather you want to find something which at least looks like a phone number.

## RegEx in Python
The regular expression in all languages is almost the same, subtle difference here and there. Well, to use regex in python we'll use the `re` module. Let's see the basic structure of using regular expression in python.

```python
import re

pattern = re.compile(r'hello')
text = 'hello world, and hello everyone'

print(re.findall(pattern, text))
```

Let's find phone numbers which look like this, `880-123-456`. Let's analyze this number for a bit. We need some string which has 3 digits at the front then a dash then again three digits and so on. We need to build a regular expression. First, we need to understand how to tell the regex engine that I need a digit. Well, `\d` represents a digit. So we can build our pattern like this.

```python
import re

patt = re.compile(r'\d\d\d-\d\d\d-\d\d\d')
```

Easy enough! We've used python **Raw** string here otherwise we had to escape all the backslashes which would be a nightmare.

Here `\d` matches any digit `0-9`. This type of thing is called **character classes** in a regular expression. We can define like this `[0123456789]` which means match any single character. We can use short-cut to represent ranges though simply by saying `[0-9]`. When we say `\d` we exactly mean `[0-9]`. That means `\d` is a shorthand for `[0-9]`. We'll see more shorthand notations later.

### Repetition
Well, we've seen the character class. Now it's a good time to learn about repetitions. In our phone number example, we've used `\d` exactly 3 times. Now the obvious question is, is there any shorthand for that? And the answer is YES, the same pattern can be written like this, `r'\d{3}-\d{3}-\d{3}'`. We represent repetitions inside curly braces.


## Final Program
Let's finalize the program. We're searching for `patt` in `text`. In our case, the `patt` is a phone number regex.

```python
import re

patt = re.compile(r'\d{3}-\d{3}-\d{3}')
text = """
003 is not the same as 002-321.
but the phone number is 003-321-314.
You may also call in 321-239-311.
"""

print(re.findall(patt, text))  // prints ['003-321-314', '321-239-311']
```

That's it for today. We'll see more character classes, repetitions, shorthand notation in the next one. Bye.
