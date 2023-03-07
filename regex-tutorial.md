# Regex Tutorial

This is an all in one tutorial gist that will explain regex and its components.

## Summary

Below you will learn all about the different components of regular expressions and what we use them for. Each component has a decription of the component itself, a multi-line text sample and the code snippet of the component in question to describe its functionality.

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

Description

// An anchor allows you to select desired words in a paragraph. Using the '^' symbol, you select the word at the beginning of a line. Using the '$' symbol, you select the word at the end of a line. Using both of the symbols, with '^' at the front of the word and '$' at the end of the word, you can find an exact line match.

Given this multi line text sample:

> apple

> apple pie

> apple iphone

> applesauce

> banana bread

> apple cider

> banana pudding

> banana split

> french fries

> cinnamon and apple


#### Anchor to beginning of line
```
/(^apple)/gm
```

#### Anchor to end of line
```
/(apple$)/gm
```

#### Anchor to start and end of line (exact line match)
```
/(^apple$)/gm
```


### Quantifiers

Description

// An quantifier allows you specify how many times a certain word must be present in order to find a match. There are both greedy and lazy quantifiers. Using a * is a greedy quantifier and *? is a lazy quantifier, both symbolizing that the keyword must match zero or more times. Lazy quantifier matches the previous token between zero and unlimited times, as few times as possible, expanding as needed. Greedy quantifier matches the previous token between zero and unlimited times, as many times as possible, giving back as needed. 

Given this multi line text sample:

> apple

> apple pie

> apple iphone

> applesauce

> banana bread

> apple cider

> banana pudding

> banana split

> french fries

> cinnamon and apple

#### Greedy quantifier
```
/(apple*)/gm
```

#### Lazy quantifier
```
/(apple*?)/gm
```

### OR Operator

Description

// An OR operator allows two different words to be found on either side of the "|" operator. For example, if we use the OR operator to search for "apple|banana", we can search for "apple" as the first alternative and "banana" as the second alternative.

Given this multi line text sample:

> apple

> apple pie

> apple iphone

> applesauce

> banana bread

> apple cider

> banana pudding

> banana split

> french fries

> cinnamon and apple

#### OR operator for either apple or banana
```
/(apple|banana)/gm
```

### Character Classes

Description

// Character classes allow us to include certain characters or ranges of characters. For example, "[0-9a-fA-F]" allows us to include all numbers and letters regardless of capitalization. If we want to search for multiple spellings of the same word, we can use gr[ae]y to search for "gray" or "grey".

Given this multi line text sample:

> grey

> gray

#### character classes to search for both gray and grey
```
/(gr[ae]y)/gm
```

### Flags

Description

// Flags allow us to set which parameters we would like our search term to follow when searching. The most common flags are global and multi-line, labelled as "g" and "m". Other flags include "i" for non-case senstive, "x" for extended meaning ignoring white spaces and more. We use these flags at the end of the regular expression.

Given this multi line text sample:

> apple

> apple pie

> Apple iphone

> Applesauce

> banana bread

> apple cider

> banana pudding

> banana split

> french fries

> cinnamon and apple

#### "gm" flags return all lowercase apple
```
/(apple)/gm
```

#### "gmi" returns all apple regardless of case
```
/(apple)/gmi
```

### Grouping and Capturing
Description

// Groups group multiple patterns as a whole, and capturing groups provide extra submatch information when using a regular expression pattern to match against a string. A group is a part of a regex pattern enclosed in parentheses () metacharacter. We create and capture a group by placing the regex pattern inside the set of parentheses ( apple ) . 

#### grouping to capture the word apple
```
/(apple)/gm
```

### Bracket Expressions

Description

// A bracket expression is an expression enclosed in square brackets "[]". This is an expression that mathces a specific set of single characters and may match a specific set of multi-character collating elements based on the expression inside the brackets. We can use similar examples as character classes above. 

Given this multi line text sample:

> grey

> gray

> A different color

#### Bracket expression allows us to select specific characters in place. This would select the first two lines
```
/(gr[ae]y)/gm
```

#### Bracket expression allows us to select all characters in all lines using ranges
```
/[0-9a-fA-F]/gm
```

### Greedy and Lazy Match

Description

// Greedy and lazy quantifiers are different ways to search; one providing as many as possible (greedy), and the other as few as possible (lazy). The greedy quantifier tells the engine to match as many instances of the token as possible. We use the "+" character to match between 1 and unlimited times, as many as possible. We use the "?" characters to match between one and unlimited times, as few as possible.

Given this single line text sample:

> "lazy" will only select what is within the first set and second set of quotes, but greedy will select the whole "line".

#### Lazy match will select "lazy" AND "line"
```
/(".+?")/gm
```

#### Greedy match will select "lazy" AND "line" as well as all characters between these two words
```
/(".+")/gm
```

### Boundaries

Description

// We use \b to denote boundaries in regular expressions. Boundaries are similar to achors, however there is a difference. Boundaries make assertions about what can be matched to the left and right of the current position. For example, \bcat\b means that no characters can be in the same word as "cat", so it would match "cat" in the word "black cat", but not in a word such as "certificate". 

Given this multi line text sample:

> black cat

> tomcat

> catfish

#### Boundary at front and end will match the first line, "black cat"
```
/(\bcat\b)/gm
```

#### Boundary at the front will match the second line, "tomcat"
```
/(\bcat)/gm
```

#### Boundary at the end will match the last line, "catfish"
```
/(cat\b)/gm
```

### Back-references

Description

// Back references allow us to resuse the same text as previously matched by a capturing group labeled \N where N is the captured group number. For example, we can use the regular expression "/\b(\w+)\b\s+\1\b/gm" which will match repeated words such as regex regex. The parentheses capture a word to group one, then use the back reference \1 to tell the engine to match the charaters that were captured by group 1.

Given this single line text sample:

> regex regex


#### /1 back reference will match regex regex, while without it we would only match regex
```
\b(\w+)\b\s+\1\b/gm
```

### Look-ahead and Look-behind

Description

// Look-ahead and look-behind are zero length assertions just like the start and end of a line or the start and end of a word. Instead of matching the characters, look ahead and look behind will result in match or no match. Negative lookahead is used if you want to match something not followed by something else, while positive does the opposite. Positive and negative look behind do the same if you want to or do not want to match something preceding something else.

Given this single line text sample:

> qwerty

> queen

> bunch

> lunch


#### negative look ahead will return the q not followed by u, in this case the q in qwerty
```
\q(?!u)/gm
```

#### positive look ahead will return the q followed by u, in this case the q in queen
```
\q(?=u)/gm
```

#### negative look behind will return the u not preceded by l, in this case the u in bunch
```
\(?<!l)u/gm
```

#### positive look ahead will return the u proceded by l, in this case the u in lunch
```
\(?<=l)u/gm
```

## Author

My name is Conner Laursen and I am the author of this regex tutorial. I am currently enrolled in a full stack coding bootcamp through the University of Washington, trying to change my career into technology. Feel free explore my profile at https://github.com/connerlaursen