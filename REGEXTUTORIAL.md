# All About Regex

Regex, short for regular expression, is a sequence of characters used to match and manipulate patterns in text. It provides a powerful and flexible way to search, extract, and replace specific strings of characters based on defined rules, making it useful for tasks like data validation and text processing.

## Summary

Regex is a powerful tool. As specified above, one of the usages of this tool is to validate data. Regex is used to match the data with a predefined sequence of characters. Some common examples of data validation are:
1.	Matching email addresses and ensuring a valid email address is provided or used.
2.	Matching passwords to a specification. Regex pattern is used to validate that password matches the requirements of the application.
3.	Matching international phone nos. To validate that provided or used phone no matches conventional format of international phone nos.
In this tutorial we will look at the different components of Regex. We will be using the following Regex to explain some of the components.
```
/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z]{2,6})$/
```
This Regex pattern defines a valid email address. We will be using this Regex pattern to understand some of the different components of the Regex. 

Since there are more components than used in this example, the components that do not feature in above, have been explained with their respective examples.

At the end of the tutorial we will look at how this Regex pattern and explore various components that make up this Regex and how it validates an email address. [Email-Example-Explained](#example-explained)

## Table of Contents

- [Anchors](#anchors)
- [Quantifiers](#quantifiers)
- [OR Operator](#or-operator)
- [Character Classes](#character-classes)
- [Flags](#flags)
- [Grouping and Capturing](#grouping-and-capturing)
- [Bracket Expressions](#bracket-expressions)
- [Greedy and Lazy Match](#greedy-and-lazy-match)
- [Boundaries](#boundaries)
- [Back-references](#back-references)
- [Look-ahead and Look-behind](#look-ahead-and-look-behind)
- [Email-Example-Explained](#example-explained)

## Regex Components

### Anchors

Anchors ``^`` and ``$`` play a special role in defining a Regex pattern.

``^``- The caret anchor defines the beginning of a word or a string

and

``$``- The dollar sign defines end of a word or a string

In the example of a valid email address, we see that ``^`` is placed in the beginning of the string to represent the start of an email string. The string ends with a ``$`` anchor, representing end of the email address.

There are other anchors that are not used in the example above and we will be exploring some of them later in this tutorial.

### Quantifiers

Quantifiers in regex are special characters or sequences that, as the name suggests it quantifies the number of occurrences of the preceding element. They are used to define how many times a character or combination of characters can appear. Some common quantifiers include:

- ``*`` asterisk: Matches zero or more occurrences of the preceding element.
- ``+`` plus: Matches one or more occurrences of the preceding element.
- ``?`` question mark: Matches zero or one occurrence of the preceding element.
- ``{n}`` n defines the no. of occurrences of character or character group: Matches exactly `n` occurrences of the preceding element.
- ``{n,}`` n with comma: Matches n or more occurrences of the preceding element.
- {n,m} n and m both are a number and m > n: Matches a range (between n and m) of occurrences of the preceding element.

These quantifiers provide control over the repetition of elements in regex patterns, allowing for more flexible and precise matching.

In the example above
both ``([a-z0-9_\.-]+)`` and ``([\da-z\.-]+)`` use ``+`` plus quantifier

The first group ``([a-z0-9_\.-]+)`` will have one or more occurrences of lowercase alphabets, digits, underscore, dots and dashes, as defined by quantifier ``+`` . Please note this part of email will be invalid if an uppercase or special character like * or # or $ or any other special character is provided as valid email should have characters as defined by character class ``[a-z0-9_\.-]``

Similarly second group ``([\da-z\.-]+)``  should have one or more occurrences of lowercase alphabets, digits, dots and dashes.

Can you guess what does this character class ``([a-z]{2,6})`` mean?

You may have guessed it by now that in this group lowercase alphabets should have between minimum of 2 and maximum of 6 occurrences.

If this is re written as ``([a-z]{2,})`` or ``([a-z]{2})``. The lowercase alphabets occurrences can 2 or more in the first case and exactly 2 in the second case.

** See below to learn character classes

### OR Operator

The OR operator is represented by ``|`` pipe symbol. It allows for matching multiple patterns. Since the example of email Regex does not feature an OR operator, lets look at the following code snippet to understand its application.

```
const pattern = /Javascript|Typescript/;// The Regex pattern using OR operator
const string = "I love both Javascript and Typescript";// String to validate presence of words Javascript and Typescript
// Testing Regex 
if (pattern.test(string)) {
  console.log("Pattern matched");
} else {
  console.log("Pattern not found");
}
```
When we run this code it will log “”Pattern matched” in the console. 
It will log “Pattern matched” till the string has either “Javascript “and/or “Typescript” in it. If none of these words are there, it will log “Pattern not found”

### Character Classes

Character classes define a set or range of characters that can be matched at a specific position within a string. They are enclosed within square brackets ``[ ]`` and specifies the acceptable characters. Some common examples of character classes include:

1.``[abc]``: Matches any single character among a, b, or c.

2.``[0-9]``: Matches any digit from 0 to 9.

3.``[a-zA-Z]``: Matches any uppercase or lowercase letter.

4.``[\d]``: Shorthand character class that matches any digit (equivalent to [0-9]).

5.``[\w]``: Shorthand character class that matches any word character (equivalent to [a-zA-Z0-9_]).

6.``[\s]``: Shorthand character class that matches any whitespace character (such as space, tab, or newline).

In the example of email Regex the character classes have been used at a few places

``[a-z0-9_\.-]``. This character class defines that only lowercase alphabets, digits, underscore, dots and dashes can be used.

``[\da-z\.-]`` . This character class defines that only lowercase alphabets, digits, dots and dashes can be used

and

``[a-z]`` . In this instance a character in this position should match a lowercase alphabet

Character Classes are also known as Bracket Expressions.

### Flags

In Regex, flags are the modifiers that define how a pattern is matched.

In the email Regex example above no flag has been provided so it will stop after searching for the first email in the string. If a string has more than one email, we can provide a flag ``g`` at the end of the string and remove ``^`` caret and ``$`` dollar sign. revised string will be ``\([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z]{2,6})\g``. Adding a flag ``m`` will change the searching pattern to search even in new lines.

Some of the common flags and their behaviour are as below:

``g``- global: Matches all occurrences of the pattern throughout the input string, rather than stopping at the first match.

``i``- case-insensitive: Matches the pattern regardless of case sensitivity, so uppercase and lowercase letters are treated as equivalent.

``m``- multiline: Changes the behaviour of the "^" and "$" anchors to match the beginning and end of each line within a multiline string, rather than just the start and end of the entire string.

### Grouping and Capturing

Grouping and capturing in regex involve enclosing a portion of the pattern in parentheses ``( )”. This allows for isolating and extracting specific portions of the matched text.

In email example above

``([a-z0-9_\.-]+)``, ``([\da-z\.-]+)``, ``([a-z]{2,6})`` are examples of grouping.

This allows to define pattern for different parts of email.

``([a-z0-9_\.-]+)`` allows for a pattern to define username of email that can contain one or many occurrences of lowercase alphabets, digits, underscore, dots and dashes.

``([\da-z\.-]+)`` allows for a pattern to define domain name of email that can contain one or many occurrences of lowercase alphabets, digits, dots and dashes.

``([a-z]{2,6})`` allows for a pattern to define domain extension of email that can contain 2-6 occurrences of lowercase alphabets.

### Bracket Expressions

Bracket expression are also known as character classes. Please refer to section on character classes.

### Greedy and Lazy Match

Our example of regex for email does not have any explicit greedy or lazy matches. 

Quantifiers ``+`` and ``{2-6}`` in the email Regex work in their own way. ``+`` matching as many occurrences of character classes whereas ``{2,6}`` limits the match to between 2-6 occurrences. 

By default, all quantifiers are greedy but can be converted into lazy by adding ``?`` after the quantifier

A greedy match occurs when a quantifier, such as "*", "+", or "{m,n}", matches as much as possible, consuming the maximum number of characters that still allows the overall pattern to match. It aims to maximize the match length.

In contrast, a lazy (also known as non-greedy or reluctant) match occurs when a quantifier is followed by a "?" character. It matches as little as possible, consuming the minimum number of characters necessary for the overall pattern to match. It aims to minimize the match length.


### Boundaries

Boundaries in regex define positions in the input string where a match must occur or not occur.
Most commonly used boundary is the word boundary and is denoted by ``\b``. Word is wrapped between these boundaries for an exact match. using this before and after a word will match any word containing that word un the end or beginning of that word.

As an example, ``\bstring\b`` will only match exact word 'string'. But this will not match words 'hamstring' or 'stringent'. Modifying this as ``\bstring`` will match the word 'stringent' and ``string\b`` will match the word 'hamstring'.

To not match a word ``\B`` that starts or end with a particular character or word. In this instance ``\Bstring\B`` will not match words 'string' 'hamstring' or 'stringent'. However ,if you have a word that surrounds the word string with other characters alphabets, that word can be validated.

Anchors are also a type of boundary ``^`` caret symbol defines the beginning of a string and ``$`` dollar symbol defines end of the string.

In the example of Regex for an email 

```
/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z]{2,6})$/
```
``^`` defines beginning of an email and ``$`` defines the end of an email

### Back-references

Back-references in Regex are a feature that allows to refer back to a previously matched group in a pattern.
Group can be referenced back by using ``\N`` where ``N`` is group no.

Regex:

``(\w).*\1``

This will select the words that have same alphabet repeated multiple times in a word e.g. 'root', 'fantastic' etc.

``(\w)`` captures the single alphabet and stores in the first capturing group
``.*`` matches any number of characters
``\1`` is the back-reference to the first captured group which is ``(\w)``

### Look-ahead and Look-behind

Lookahead and lookbehind are zero-width assertions in regular expressions that allow you to check for patterns without including them in the actual match. They are useful for creating more complex matching conditions.

Lookahead assertion is denoted by (?=...) and checks if a pattern is followed by another pattern. It does not consume any characters during matching.

Lookbehind assertion is denoted by (?<=...) and checks if a pattern is preceded by another pattern. It also does not consume any characters during matching.

Positive Lookahead:
Pattern: \w+(?=ing)
Description: This pattern matches any word that is followed by the letters "ing".

Positive Lookbehind:
Pattern: (?<=\d{2})\d+
Description: This pattern matches any number that is preceded by two digits.

Replacing ``=`` in the pattern with ``!`` we can change the behaviour to not match. This is also referred to as Negative Lookahead or Negative Lookbehind.

## Example Explained

Let’s look at the Original Example

```
/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z]{2,6})$/
```
Explanation:

``^'' caret represents the beginning of the string

``([a-z0-9_\.-]+)`` represents a group of characters as defined by the character class representing lowercase alphabets, digits, underscore, dots and dashes and ``+`` sign represents one or more occurrences of these characters. This represents the username portion of email.

``@`` is literal '@' and this means username is followed by character '@'.

``([\da-z\.-]+)`` This group represents the domain name and can have one or more occurrences of alphabets, digits, dots and dashes as defined by its character class.

``\.`` is literal '.' and this means domain name is followed by a dot `` . ``

``([a-z]{2,6})`` is the domain extension and have between 2-6 occurrences of lowercase alphabets.

Examples of valid email address as per Regex pattern

1. john.doe@example.com
2. mary.saunders_123@example.com

Examples of invalid email addresses

1. John.doe@example.com (as Username cannot have an uppercase alphabet)
2. john*doe@example.con (as Username cannot have a non-alphanumeric character other than underscore, dash and dot )
3. john.doe@example_123.co (as Domain name cannot have an underscore)
4. john.doe@example.c (as Domain extension should have min 2 alphabets)
5. john.doe@example.com123 (as Domain extension cannot have non alphabet)


## Author

My Name is Sanjay Chopra. I am learning to code and currently going through a Full Stack Developer Bootcamp through Monash University. I currently run a successful Retail Business and hoping to be a full stack developer.
Outside of work I am an avid Cricket follower and have interest in photography and flying drones.

You can click on link below to get in touch with me.
[contact](mailto:sanjaybenu@gmail.com?subject=Regex_Tutorial) or visit [github/sanjaybenu](https://github.com/sanjaybenu) to checkout my other projects.
