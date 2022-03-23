# Regex Tutorial

In this tutorial you will learn how regular expressions work, as well as how to use them to perform pattern matching in an efficient way in JavaScript.

## Summary

Regular Expressions, commonly known as "regex" or "RegExp", are a specially formatted text strings used to find patterns in text. Regular expressions are one of the most powerful tools available today for effective and efficient text processing and manipulations. For example, it can be used to verify whether the format of data i.e. name, email, phone number, etc. entered by the user is correct or not, find or replace matching string within text content, and so on.

## Table of Contents

- [Anchors](#anchors)
- [Quantifiers](#quantifiers)
- [Grouping Constructs](#grouping-constructs)
- [Bracket Expressions](#bracket-expressions)
- [Character Classes](#character-classes)
- [The OR Operator](#the-or-operator)
- [Flags](#flags)
- [Character Escapes](#character-escapes)

## Regex Components

### Anchors
Anchors have special meaning in regular expressions. They do not match any character. Instead, they match a position before or after characters:

 ^ – The caret anchor matches the beginning of the text.
 $ – The dollar anchor matches the end of the text.

 Example:
```Javascript
 let str = 'JavaScritp';
 console.log(/J/.test(str));
```

 Output:

 ```Javascript
 true
 ```

 The /^J/ match any text that starts with the letter J. It returns true.

The following example returns false because the string JavaScript doesn’t start with the letter S:

```Javascript
let str = 'JavaScript';
console.log(/^S/.test(str));
```

Output:
```Javascript
false
```

### Quantifiers

A number in curly braces {n}is the simplest quantifier. When you append it to a character or character class, it specifies how many characters or character classes you want to match.
We often use the quantifiers to form complex regular expressions. The following shows some regular expression examples that include quantifiers:

Whole numbers:/^\d+$/
Decimal numbers:/^\d*.\d+$/
Whole numbers and decimal numbers:/^\d*(.\d+)?$/
Negative, positive whole numbers & decimal numbers:/^-?\d*(.\d+)?$/

The quantifier * means zero or more. It is the same as {0,}. The following example shows how to use the quantifier * to match the string Java followed by any word character:

```Javascript
let str = 'JavaScript is not Java';
let re = /Java\w*/g

let results = str.match(re);

console.log(results);

```
Output:
```Javascript

["JavaScript", "Java"]
```


### Grouping Constructs
A part of a pattern can be enclosed in parentheses (...). This is called a “capturing group”.

That has two effects:

It allows to get a part of the match as a separate item in the result array.
If we put a quantifier after the parentheses, it applies to the parentheses as a whole.
Examples
Example: email
The previous example can be extended. We can create a regular expression for emails based on it.

The email format is: name@domain. Any word can be the name, hyphens and dots are allowed. In regular expressions that’s [-.\w]+.

The pattern:
```Javascript

let regexp = /[-.\w]+@([\w-]+\.)+[\w-]+/g;

alert("my@mail.com @ his@site.com.uk".match(regexp)); // my@mail.com, his@site.com.uk
```

That regexp is not perfect, but mostly works and helps to fix accidental mistypes. The only truly reliable check for an email can only be done by sending a letter.


### Bracket Expressions

In this part we will just look at one group of symbols in depth, the brackets. [ ]
Brackets indicate a set of characters to match. Any individual character between the brackets will match, and you can also use a hyphen to define a set.

```Javascript
'elephant'.match(/[abcd]/) // -> matches 'a'
```
You can use the ^ metacharacter to negate what is between the brackets.
```Javascript
'donkey'.match(/[^abcd]/) // -> matches 'o'
```
You will often see ranges of the alphabet or all numerals. [A-Za-z] [0-9] Remember that these character sets are case sensitive, unless you set the i flag.
```Javascript
'elephant'.match(/[a-d]/) // -> matches 'a'
'elephant'.match(/[A-D]/) // -> no match
'elephant'.match(/[A-D]/i) // -> matches 'a'
```
{ } Curly braces are used to specify an exact amount of things to match. They are used after an expression: \na{2}\ will only match ‘na’ exactly twice.
```Javascript
'panama'.match(/na{2}/) // -> no match
'banana'.match(/na{2}/) // -> matches 'nana'
```
You can use these in conjunction with a comma to specify more than one amount. {2,} = two or more times, {2,4} = between two and four times.
```Javascript
'banana'.match(/a{2,4}/) // -> no match
'bananaa'.match(/a{2,4}/) // -> matches 'aa'
'bananaaa'.match(/a{2,4}/) // -> matches 'aaa'
'bananaaaa'.match(/a{2,4}/) // -> matches 'aaaa'
'bananaaaaaaaaaaa'.match(/a{2,4}/) // -> matches 'aaaa'
```
( ) Parentheses represent remembered matches. This is especially useful for find-and-replace operations or any time you need to do something with part of the match. When a match is remembered you can use $n to refer to it, starting with $1 up to $9, or with $& to refer to the entire match.
```Javascript
'Firsty McLastname'.match(/([A-Za-z]+)\s([A-Za-z]+)/) // -> matches 'First McLastname' with 'Firsty' remembered as $1 and 'McLastname' as $2
'Firsty McLastname'.replace(/([A-Za-z]+)\s([A-Za-z]+)/, '$1') // -> returns 'Firsty'
'Firsty McLastname'.replace(/([A-Za-z]+)\s([A-Za-z]+)/, '$2, $1') // -> returns 'McLastname, Firsty'
'Firstipher Lasterman'.replace(/([A-Za-z]+)\s([A-Za-z]+)/, '$&') // -> returns 'Firstipher Lasterman'
```
### Character Classes
A character class allows you to match any symbol from a certain character set. A character class is also called a character set. Suppose that you have a phone number like this:
```Javascript
+1-(706)-345-4960
```
And you want to turn it into a plain number:
```Javascript
17063454960
```
Character classes in regular expressions can help you to do this.

Let’s explore the digit character class first. The digit character class is denoted by \d which matches any single digit:
```Javascript
\d
```
The following example uses the \d to match the first number in the phone number:
```Javascript

let phone = '+1-(706)-345-4960';
let re = /\d/;

console.log(phone.match(re));
```
Output:
```Javascript
["1"]
```
When you add the global flag (g), the regular expression will search for all numbers, not the first one:
```Javascript
let phone = '+1-(706)-345-4960';
let re = /\d/g;

console.log(phone.match(re));
```
Output:
```Javascript
["1", "7", "0", "6", "3", "4", "5", "4", "9", "6", "0"]
```
### The OR Operator
Alternation is the term in regular expression that is actually a simple “OR”.

In a regular expression it is denoted with a vertical line character |.

For instance, we need to find programming languages: HTML, PHP, Java or JavaScript.
A usage example:

```Javascript
let regexp = /html|css|java(script)?/gi;

let str = "First HTML appeared, then CSS, then JavaScript";

alert( str.match(regexp) ); // 'HTML', 'CSS', 'JavaScript'
``` 
We already saw a similar thing – square brackets. They allow to choose between multiple characters, for instance gr[ae]y matches gray or grey.

Square brackets allow only characters or character classes. Alternation allows any expressions. A regexp A|B|C means one of expressions A, B or C.

For instance:

gr(a|e)y means exactly the same as gr[ae]y.
gra|ey means gra or ey.
To apply alternation to a chosen part of the pattern, we can enclose it in parentheses:

I love HTML|CSS matches I love HTML or CSS.
I love (HTML|CSS) matches I love HTML or I love CSS.
### Flags
We'll start by defining what exactly is a flag:

A flag is an optional parameter to a regex that modifies its behavior of searching.

A flag changes the default searching behaviour of a regular expression. It makes a regex search in a different way.

A flag is denoted using a single lowercase alphabetic character.

In JavaScript regex, we have a total of 6 flags, each serving a different purpose.
| Flag | Name | Modification |
|:---------: | :------------ | :--------- |
| i | Ignore Casing| Makes the expression search case-insensitively|
| g |Global |Makes the expression search for all occurrences.|
| s |Dot All |Makes the wild character . match newlines as well.|
| m |Multiline |Makes the boundary characters ^ and $ match the beginning and ending of every single line instead of the beginning and ending of the whole string.|
| y |Sticky |Makes the expression start its searching from the index indicated in its lastIndex property.|
| u |Unicode |Makes the expression assume individual characters as code points, not code units, and thus match 32-bit characters as well.|


For an expression created literally, i.e. using the forward slashes //, flags comes after the second slash. In general notation we can expression this as follows:

/pattern/flags
Similarly, for an expression created using RegExp(), flags go as a string in the second argument, as shown below:

new RegExp('pattern', 'flags')

### Character Escapes
Let’s say we want to find literally a dot. Not “any character”, but just a dot.

To use a special character as a regular one, prepend it with a backslash: \..

That’s also called “escaping a character”.

For example:

```javascript

alert( "Chapter 5.1".match(/\d\.\d/) ); // 5.1 (match!)
alert( "Chapter 511".match(/\d\.\d/) ); // null (looking for a real dot \.)
```
Parentheses are also special characters, so if we want them, we should use \(. The example below looks for a string "g()":
```javascript
alert( "function g()".match(/g\(\)/) ); // "g()"
```
## Author info:
check page : https://www.javascripttutorial.net/

I am Eder Rodrigo Ramirez Contreras and my Gitgub is https://github.com/kdher/
