# What the Regex!?

Introduction to Regex components and how they match strings and more!

## Summary

Using the components described below this summary, I've put together an example of how to match an email when it is proper. So we filter out such things as `john @ gmail.com`, `johngmailcom` and `john@gmailcom`. Allowing us to quickly give user feedback when needing a proper email address.

We first start by adding our flags `/ /` to determine it is a regex search pattern.

We start with anchors `/^` to say we want to begin at the start of the word. We then search for white space characters with `\S+@` then we say we want to follow it with @. That is then checked for another space afterwards using `\S+` again and followed by any matching character using `\.`. We then want to make sure there are no white spaces after . with `\S+`. We finish by then using `$/` to note that we end our expression at the end of the string.

`/^\S+@\S+\.\S+$/`

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

## Regex Components

### Anchors

```
^Match     will match any string that percedes the Match
me$        Will match any string that ends with the me
^Match me$ will match a string with the exact match Match me
```

### Quantifiers

```
abc*        matches a string that has ab followed by zero or more c
abc+        matches a string that has ab followed by one or more c
abc?        matches a string that has ab followed by zero or one c
abc{2}      matches a string that has ab followed by 2 c
abc{2,}     matches a string that has ab followed by 2 or more c
abc{2,5}    matches a string that has ab followed by 2 up to 5 c
a(bc)*      matches a string that has a followed by zero or more copies of the sequence bc
a(bc){2,5}  matches a string that has a followed by 2 up to 5 copies of the sequence bc
```

### OR Operator

```
a(b|c)     matches a string that has a followed by b or c (and captures b or c)
a[bc]      same as previous, but without capturing b or c
```

### Character Classes

```
\d         matches a single character that is a digit
\w         matches a word character (alphanumeric character plus underscore)
\s         matches a whitespace character (includes tabs and line breaks)
.          matches any character
```

### Flags

We are learning how to construct a regex but forgetting a fundamental concept: flags.

A regex usually comes within this form /abc/, where the search pattern is delimited by two slash characters /. At the end we can specify a flag with these values (we can also combine them each other):

- g (global) does not return after the first match, restarting the subsequent searches from the end of the previous match

- m (multi-line) when enabled ^ and $ will match the start and end of a line, instead of the whole string

- i (insensitive) makes the whole expression case-insensitive (for instance /aBc/i would match AbC)

### Grouping and Capturing

```
a(bc)           parentheses create a capturing group with value bc
a(?:bc)*        using ?: we disable the capturing group
a(?<foo>bc)     using ?<foo> we put a name to the group
```

### Bracket Expressions

```
[abc]            matches a string that has either an a or a b or a c -> is the same as a|b|c
[a-c]            same as previous
[a-fA-F0-9]      a string that represents a single hexadecimal digit, case insensitively
[0-9]%           a string that has a character from 0 to 9 before a % sign
[^a-zA-Z]        a string that has not a letter from a to z or from A to Z. In this case the ^ is used as negation of the expression
```

### Greedy and Lazy Match

The quantifiers ( \* + {}) are greedy operators, so they expand the match as far as they can through the provided text.

For example, <.+> matches <div>simple div</div> in This is a <div> simple div</div> test. In order to catch only the div tag we can use a ? to make it lazy:

```

<.+?> matches any character one or more times included inside < and >, expanding as needed

```

Notice that a better solution should avoid the usage of . in favor of a more strict regex:

```

<[^<>]+> matches any character except < or > one or more times included inside < and >

```

### Boundaries

```

\babc\b performs a "whole words only" search

```

`\b` represents an anchor like caret (it is similar to $ and ^) matching positions where one side is a word character (like \w) and the other side is not a word character (for instance it may be the beginning of the string or a space character).
It comes with its negation, \B. This matches all positions where \b doesn’t match and could be if we want to find a search pattern fully surrounded by word characters.

```

\Babc\B matches only if the pattern is fully surrounded by word characters

```

### Back-references

```

([abc])\1 using \1 it matches the same text that was matched by the first capturing group

([abc])([de])\2\1 we can use \2 (\3, \4, etc.) to identify the same text that was matched by the second (third, fourth, etc.) capturing group

(?<foo>[abc])\k<foo> we put the name foo to the group and we reference it later (\k<foo>). The result is the same of the first regex

```

### Look-ahead and Look-behind

```

d(?=r) matches a d only if is followed by r, but r will not be part of the overall regex match

(?<=r)d matches a d only if is preceded by an r, but r will not be part of the overall regex match

```

You can use also the negation operator!

```

d(?!r) matches a d only if is not followed by r, but r will not be part of the overall regex match

(?<!r)d matches a d only if is not preceded by an r, but r will not be part of the overall regex match

```

## Author

**[Souhila Mimisou ](https://github.com/souhila27)** - Avid code enthusiast and striving for greatness in application development of all things Javascript!
