
# Introduction to Regular Expressions

## Introduction

In this lesson, we'll learn about how we can use **_Regular Expressions_** for pattern matching and filtering when working with text data. 

## Objectives

You will be able to:

- Identify common use cases where regular expressions are useful 
- Create regex code to capture meaningful patterns found in text 


## What Are Regular Expressions?

**_Regular Expressions_** are a type of pattern that describe some text. We can use these regular expressions to quickly match patterns and filter through text documents. Regular Expressions (or regex, for short) are an important tool anytime we need to pull information from a larger text document without manually reading the entire thing. For data scientists, regex is extremely useful for data gathering. With regex, we can quickly scrape webpages by using regex to search through the html and find the info needed. 

### Use Cases for NLP

Regex is especially useful for Natural Language Processing. By definition, just about any text document you work with on an NLP task is going to be one that contains a large amount of text. One of the more common NLP-specific use cases for regex is to use regex during the tokenization stage to define the rules for where we should split strings into separate tokens. As an example, NLTK's basic `word_tokenize()` function would split a word that contains an apostrophe into 3 separate tokens -- `'they're'` gets broken into `["they", "'", "re"]`. This is because the word tokenizer has instructions to just grab sequences of letters as the basic tokens, and an apostrophe isn't a letter. When preprocessing text data, it's quite common to use some small regex patterns to create a more intelligent tokenization scheme to avoid problems like this, so that our tokenizer treats words like `'they're'` as a single token. 


## Creating Basic Patterns

Regex is only as good as the **_Patterns_** we create. We can use these patterns to find, or to replace text. There are many, many things we can do with regex, and covering them all is outside the scope of this lesson. Instead, we'll just focus on some of the more useful, basic patterns that allow us to begin using regex to work with text data. 

Let's take a look at a basic regex pattern, to get a feel for what they look like. 

```python
import re
sentence = 'he said that she said "hello".'
pattern = 'he'
p = re.compile(sentence)
p.findall() # Output will be ['he', 'he, 'he']
```

We define a pattern by a Python string. We can then use the regular expressions library, `re`, to compile this pattern. Once we have a compiled pattern, we just need to pass in a string and the pattern will find every instance of that pattern in the string. 

For people new to regex, the results from the pattern above might be surprising at first. The pattern successfully matches the word 'he', but it also matches the letters 'he' that are found inside of the words 'she' and 'hello'.  Subsequences inside of larger sequences are fair game to regex. If we just wanted to match the word 'he', we would need to specify that the pattern needs to start and end with a space, or use of **_anchors_** for things like word boundaries. 


## Ranges, Groups, and Quantifiers

Obviously, we don't want to have to explicitly type every valid match for any search into our pattern. That would defeat the purpose. Luckily, we don't have to type every possible uppercase letter to match on uppercase letters. Instead, we can use a **_Range_** such as `[A-Z]`. This will match any uppercase letter. Ranges are always inside of square brackets. We can put many things inside of ranges at the same time, and regex will match on any of them. For instance, if we wanted to find any uppercase letter, lowercase letter, or digit, we could use `[A-Za-z0-9]`. 


### Character Classes

Character classes are a special case of ranges. Since it's quite a common task to use ranges to do things like match on words or numbers, regex actually includes character classes as a shortcut. For instance, we could use `\d` to match any digit -- this is equivalent to using `[0-9]`. We could also use `\w` to match on any word. In the same vein, we can use `\D` to get anything that _isn't_ a digit, or `\W` to match on everything that isn't a word. There are a few other types of character classes as well. For a full list, check out the cheat sheet below!


### Groups and Quantifiers

Groups are kind of like ranges, but they specify an exact pattern to match on. Groups are denoted by parentheses. Whereas `[A-Z0-9]` matches on any uppercase letter or any digit, `(A-Z0-9)` will only match on the sequence `'A-Z0-9'` exactly. This becomes much more useful when paired with **_Quantifiers_**, which allows us to specify how many times a group should happen in a row. If we want to specify an exact number of times, we can use curly braces. For instance, a group followed by `{3}` will only match on patterns that have that group repeated exactly 3 times. The most common quantifiers are usually:

* `*` (0 or more times)
* `+` (1 or more times)
* `?` (0 or 1 times)

In this way, we can fill a grouping with any pattern, tell and specify the number of times we can expect to see that pattern. When we include things like ranges, groupings, and quantifiers together, it becomes easy to write a pattern that can match complex things, like email addresses -- take a look at the example provided below, and see if you can figure out how it works!

`'([A-Za-z]+)@([A-Za-z]+)\.com'` 

This pattern matches basic email addresses like 'joe@gmail.com', but not 'john.doe@gmail.com', or 'joe@stanford.edu'. Take a look at the pattern again -- how would you need to modify the pattern in order for it to match either of those, as well?

## Always Keep A Cheat Sheet Handy

Regex is confusing, but it gets easier. With that being said, don't worry about trying to memorize all of the different symbols and metacharacters. Instead, focus on how patterns work, and just look up the symbols when you need them. The internet is filled with great regex cheatsheets. Here's an easy one to keep on hand for future reference:

<img src='images/regex_cheat_sheet.png'>


## Summary

In this lesson, we learned about what regular expressions are, how they are used in NLP for specific tasks, and some common patterns and tools in regex. 
