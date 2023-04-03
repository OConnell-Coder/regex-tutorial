# Regex Tutorial for Matching an Email Address Format

A Regular Expression (often shortened to regex) is an arrangement of characters used in coding and search algorithms to define a specific type of pattern. This allows the program to search for a certain pattern, even if the exact characters are unknown. For example, this would allow the program to search anywhere on the page for an email address, phone number, or URL without already knowing the details of the aforementioned item. It is universal to all coding languages and many text editors too. Regex are often used in coding to validate user input is entered correctly. It tells the program that an email should like stuff@stuff.com. But how can we tell the program to look for a pattern like that? It works by defining the type and number of characters and the order they should appear. In this tutorial, we'll use the regex for matching an email as an example. Let's break it down.

## Summary

Regex for Matching an Email:

    /^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/

This tells the program to look for a pattern starting with any number of alphanumeric characters, including the underscore, period, and dash symbols.  
Then it tells it that it will be followed by the @ symbol.  
That will be followed by any numerical digit from 0-9, any letter from a-z, and potentially a period or dash, again in no particular order.  
Then there will be a period.  
After that, there will be another string of characters from a-z (including a period) that is anywhere from 2-6 characters long.

As you match the written-out description to the coded one above it, you may start to notice logical patterns emerging. However, what do you make of all the seemingly random symbols in between? To understand those, we'll have to dive deep into the world of regular expressions, so take a deep breath and prepare for the plunge.

## Table of Contents

- [Anchors](#anchors)
- [Bracket Expressions](#bracket-expressions)
- [Quantifiers](#quantifiers)
- [Greedy and Lazy Match](#greedy-and-lazy-match)
- [Grouping and Capturing](#grouping-and-capturing)
- [OR Operator](#or-operator)
- [Character Classes](#character-classes)
- [Character Escapes](#character-escapes)
- [Flags](#flags)
- [About the Author](#about-the-author)

## Regex Components

Each component (or piece) of a regex serves a specific purpose. For example, since a regex is a literal, it's wrapped in forward-slashes `/`, which gives it clearly defined beginning and end points. Please note that this tutorial only covers literal notation and not RegExp constructors. Now let's take a look at some of these different components.

### Anchors

Anchors are used to define something's place in the regex. A caret ^ will tell the program that the string begins with the characters that follow it, while a dollar-sign \$ will notate that the string will end with the characters that precede it. If you look at our example on matching an email address, you can see that the regex starts with `/^` and ends with `$/`. However, depending on the way the following (or preceding) characters are formatted, it can mean different things.
If you follow an anchor with specific characters, like `^The`, it will look for an exact match and determine that the searched-for string starts with "The". If it's followed by a Bracket Expression instead, it will know to look for a range of possibilities. For example, `^[a-z]` will look for a string that starts with any lowercase letter of the alphabet. So what exactly is a Bracket Expression?

### Bracket Expressions

As you might have guessed from the above example, a Bracket Expression is a collection of characters contained within brackets that represent a group of possible characters that could match the searched string. These are often called a "positive character group" because it defines anything you might want to include in your search. A hyphen `-` is used to make it a range. For example, `[abc]` is the same as `[a-c]`.  
`[a-z]` = any lowercase letter.  
`[A-Z]` = any uppercase letter.  
`[0-9]` = any whole digit number.  
`[_-]` = underscore and/or hyphen.  
These can be combined in a single bracket expression to allow for a wider range of accepted outcomes.  
`[a-zA-Z]` = any letter (case-insensitive).  
`[a-zA-Z0-9_-]` would search for any of the above possibilities (any letter, number, underscore, hyphen).  
It is important to note that these will search for ANY of the listed requirements (not all).  
You can also use bracket expressions to define a "negative character group" to exclude any unwanted characters, simply by preceding it with the `^` symbol.
`[^xyz]` would exclude anything with ANY of those letters (not the full "xyz" string).  
If we look at our email address example again, we can see that there are three bracket expressions. One for the username `[a-z0-9_\.-]`, one for the domain name `[\da-z\.-]`, and one for the domain type (.com, .edu, .org, etc.) `[a-z\.]`.

### Quantifiers

Quantifiers, as their name implies, set a limit on the number of characters in the string or in a section of the string. These are often contained in curly brackets if there are multiple limits to set (like a minimum and maximum). Here are the basic quantifiers (we'll discuss how to navigate "greedy" and "lazy" matches next).  
`{ n }` = finds a string with this EXACT number of characters.  
`{ n, }` = finds a string with AT LEAST this number of characters (because there is a minimum noted but no maximum noted).  
`{ n, x }` = finds a string with a minimum of "n" characters and a maximum of "x" characters.  
In the email address example, there is only one quantifier limit set using curly brackets: `{2,6}`. It is in the last section, telling the program that the domain type should be a minimum of 2 characters and a maximum of 6 characters. So how can we navigate the idea of "greedy" and "lazy" matches? How can a quantifier even be greedy?

### Greedy and Lazy Match

Quantifiers are "greedy" by nature. They will try to match a pattern as many times as possible. In order to reign in these hungry, hungry quantifiers, there are various ways to tell the regex what limits you desire with specific characters. You can use any of the above quantifiers that were already listed, like `{min, max}`. Additionally, you can use any of the following too.  
`*` = matches pattern zero or more times.  
`+` = matches pattern one or more times.  
`?` = matches pattern zero or one time.  
You can make any of these quantifiers "lazy" by adding a question-mark `?` after it. That will make it try to match the pattern the least possible number of times.  
With the email example, you can see that the username section `([a-z0-9_\.-]+)` and the domain name section `([\da-z\.-]+)` both have a `+` after them to indicate that there are one or more (1+) characters in each of those sections.

### Grouping and Capturing

Something you might have noticed or might have taken for granted until now, is that our regex is broken up into "subexpressions" or subsections. These Grouping Constructs are important because they tell our regex what should be grouped together, often using parentheses. It works similarly to how parentheses work in math equations.  
If you see `(12 x 6) + 3` then you know that you must multiply 12 by 6 before you can add 3, getting an answer of 75.   However, if you see `12 x (6 + 3)`, then you know that you must add 6 and 3 before you can multiply that by 12, getting an answer of 108. Applying this logic to regex subexpressions, you can see how it will affect the code differently depending on where the parentheses are. It is important to note that subexpressions look for exact matches unless specified otherwise. Grouping constructs can be capturing or non-capturing. Capturing means that they will grab the character order for reuse, while non-capturing does not grab the info, so it cannot be reused. A subexpression can be made non-capturing by adding `?:` at the beginning.  
In our email example, we can see the 3 subsections are there for the username `([a-z0-9_\.-]+)`, domain name `([\da-z\.-]+)`, and domain type `([a-z\.]{2,6})`. That way, the regex knows to look for different things for each of those sections. You'll also see that the parentheses connect the bracket expressions with their own quantifiers. That's how the program can tell which parts of the regex go together.

### OR Operator

Like most search engines, regex can also utilize an OR operator. This allows you to search for either one thing or another in a single search (when you don't want both). In regex, we do this by using a pipe character `|`. The pipe can be put either between subexpressions or within one, depending on the desired effect.  
`(abc)|(xyz)` will search for either "abc" OR "xyz".  
`(a|b|c)` will search for either "a" OR "b" OR "c".  
The email address regex does not use an OR operator.

### Character Classes

Character Classes are a specific set of characters that can stand in for any group of characters. The easiest way to understand what that means is to see the examples.  
`.` = matches ANY character (except a new line: `\n`)  
`\d` = matches any Arabic numeral digit, same as `[0-9]`  
`\w` = matches any alphanumeric character and underscore, same as `[A-Za-z0-9_]`  
`\s` = matches a single whitespace character, including tabs and line breaks  
This can be very helpful in shortening a regex if there's already a character class for that group of characters. "Of course, the reverse is also true." By capitalizing any of the above (`\D`, `\W`, `\S`), it will tell the program to EXCLUDE those characters instead.  
In the email example, the domain name subsection contains a `\d` so it can find any whole number [0-9] in the domain name.

### Character Escapes

Within each component, there are "literal" characters and "meta" characters. Literal characters, as their name implies, refer to characters in the regex that are taken literally to refer to characters with a fixed value. Meta characters, on the other hand, are used to affect other characters and change their nature. It is often a stand-in for possibilities or a way to make a character behave differently. This is why sometimes we have to use Character Escapes. Often the backslash `\` is used to escape a character. For example, a curly bracket `{}` often begins a quantifier, so the program will ignore it, but if you need to search for a curly bracket, then you would write `\{` instead. That will make it read the curly bracket as a literal character instead of a meta character. It's important to note that special characters inside of bracket expressions [] are taken literally and lose their meta significance.  
If we look again at our email example, we'll see that the dot before the domain type (.com) is escaped `\.` so that it can search for a literal period (.) instead of a meta period (which stands in for ANY character).

### Flags

Flags are unique additions that can change the limits or the functionality of the expression. They are particularly strange because they go outside of the wrapping slash at the end. This is because they say more about where to search than what to search for.  
`g` = global search (search anywhere for all possible matches)  
`i` = case-insensitive (case doesn't matter, can be uppercase or lowercase)  
`m` = multi-line search (keeps multi-line format for search input)  
The email address regex does not use any flags.

## About the Author

Growing up, I was always told that I "think like a robot." I suppose I took that to heart (or should I say to my PSU) because I decided to learn how to talk to computers. I learned full-stack developer skills from the University of Pennsylvania's LPS Coding Bootcamp.  
At first, it was a drastic change from my previous careers as an English Professor and a Corporate Accountant. But I quickly found that both careers played a foundational role to my understanding of coding. From English, I brought creativity, a propensity for syntax and grammar, and a constant conceptualization of how form and design informs function and communication. From Accounting, I brought efficiency, accuracy, and precision, in a field where attention-to-detail is equally critical.  

My GitHub Profile: https://github.com/OConnell-Coder
