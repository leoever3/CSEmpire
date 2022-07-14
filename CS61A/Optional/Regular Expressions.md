## What are Regular Expressions?

Consider the following scenarios:

> 1. You've just written a 500 page book on how to dominate the game of Hog. Your book assumes that all players use six-sided dice. However, in 2035, the newest version of Hog is updated to use 25-sided dice. You now need to find all instances where you mention six-sided dice in your article and update them to refer to 25-sided dice.
> 2. You are in charge of a registry of phone numbers for the SchemeCorp company. You're planning a company social for all employees in the city of Berkeley. To make your guest list, you want to find the phone numbers of all employees living in the Berkeley area codes of 415 or 314.
> 3. You're the communications expert on an interplanetary voyage, and you've received a message from another starship captain with the locations of a large number of potentially habitable planets, represented as strings. You must determine which of these planets lie in your star system.

What do all of these scenarios have in common? They all involve searching for **patterns** within a larger piece of text. These can include extracting strings that *begin with* a certain set of characters, *contain* a certain set of characters, or follow a certain *format*.

**Regular expressions** are a powerful tool for solving these kinds of problems. With regular expression operators, we can write expressions to describe a **set of strings** that match a specified pattern.

For example, the following code defines a function that matches all words that start with the letter "h" (capitalized or lowercase) and end with the lowercase letter "y".

```python
import re
def hy_finder(text):
    """
    >>> hy_finder("Hey! Hurray, I hope you have a lovely day full of harmony.")
    ['Hey', 'Hurray', 'harmony']
    """

    return re.findall(r"\b[Hh][a-z]*y\b", text)
```

Let's examine the above regular expression piece by piece.

1. First, we use `r""`, which denotes a **raw string** in Python. Raw strings handle the backslash character `\` differently than regular string literals. For example, the `\b` in this regular expression is treated as a sequence of two characters. If we were to use a string literal without the additional `r`, `\b` would be treated as a single character representing an ASCII bell code.
2. We then begin and end our regular expression with `\b`. This ensures that word boundaries exist before the "h" and after the "y" in the string we want to match.
3. We use `[Hh]` to represent that we want our word to start with either a capital or lowercase "h" character.
4. We want our word to contain 0 or more (denoted by the `*` character) lowercase letters between the "h" and "y". We use `[a-z]` to refer to this set.
5. Finally, we use the character `y` to denote that our string should end with the lowercase letter "y".

## Regular Expression Operators

Regular expressions are most often constructed using combinations of **operators**. The following special characters represent operators in regular expressions: `\`, `(`, `)`, `[`, `]`, `{`, `}`, `+`, `*`, `?`, `|`, `$`, `^`, and `.`.

We can still build regular expressions without using any of these special characters. However, these expressions would only be able to handle *exact matches*. For example, the expression `potato` would match all occurences of the characters p, o, t, a, t, and o, *in that order*, within a string.

Leveraging these operators enables us to build much more interesting expressions that can match a wide range of patterns. We'd recommend using interactive tools like [regexr.com](https://regexr.com/) or [regex101.com](https://regex101.com/) to practice using these.

Let's take a look at some common operators.

| Pattern | Description                                                  | Example  | Example Matches  | Example Non-matches |
| :------ | :----------------------------------------------------------- | :------- | :--------------- | :------------------ |
| `[]`    | Denotes a *character class*. Matches characters in a set (including ranges of characters like `0-9`). Use `[^]` to match characters outside a set. | `[top]`  | t, o, p          | s, march, 3         |
| `.`     | Matches *any character* other than the newline character.    | `1.`     | 1a, 1?, 11       | 1, 1\n              |
| `\d`    | Matches any *digit character*. Equivalent to `[0-9]`. `\D` is the *complement* and refers to all non-digit characters. | `\d\d`   | 12, 42, 60       | 4, 890              |
| `\w`    | Matches any *word character*. Equivalent to `[A-Za-z0-9_]`. `\W` is the complement. | `\d\w`   | 1a, 9_, 4Z       | 14, a5              |
| `\s`    | Matches any *whitespace character*: spaces, tabs, or line breaks. `\S` is the complement. | `\d\s\w` | 1 s, 9 *, 4* Z   | 1s, 1 s             |
| `*`     | Matches *0 or more* of the previous pattern.                 | `a*`     | , a, aa, aaaaa   | schmorp, mlep       |
| `+`     | Matches *1 or more* of the previous pattern.                 | `lo+l`   | lol, lool, loool | ll, lal             |
| `?`     | Matches *0 or 1* of the previous pattern.                    | `lo?l`   | lol, ll          | lool, lulz          |
| `|`     | Usage: `Char1 | Char2 `. Matches *either Char1 or Char2*.    | `a|b`    | a, b             | c, d                |
| `()`    | Creates a *group*. Matches occurences of all characters within a group. | `(<3)+`  | <3, <3<3, <3<3<3 | <<, 33              |
| `{}`    | Used like `{Min, Max}`. Matches a *quantity* between Min and Max of the previous pattern. | `a{2,4}` | aa, aaa, aaaa    | a, aaaaa            |
| `^`     | Matches the *beginning* of a string.                         | `^aw+`   | aw, aww, awww    | wa, waaa            |
| `$`     | Matches the *end* of a string.                               | `\w+y$`  | hey, bay, stay   | yes, aye            |
| `\b`    | Matches a *word boundary*, the beginning or end of a word.   | `\w+e\b` | bridge, smoothie | next, everlasting   |

## Regular Expressions in Python

In Python, we use the `re` module (see the Python [documentation](https://docs.python.org/3/library/re.html) for more information) to write regular expressions. The following are some useful function in the `re` module:

- `re.search(pattern, string)` - returns a match object representing the first occurrence of `pattern` within `string`
- `re.sub(pattern, repl, string)` - substitutes all matches of `pattern` within `string` with `repl`
- `re.fullmatch(pattern, string)` - returns a match object, requiring that `pattern` matches the entirety of `string`
- `re.match(pattern, string)` - returns a match object, requiring that `string` starts with a substring that matches `pattern`
- `re.findall(pattern, string)` - returns a list of strings representing all matches of `pattern` within `string`, from left to right





#### BNF grammar for parsing through regular expression patterns

1. basic: character | word
2. grouping allows for an entire regular expression to be treated as a single unit (apple)
3. piping allows for a pattern to match an expression on either side. (apple) | (banana)
4. character classes allow for the pattern to match any singular `character` defined within the class.[0-9] [A-Z] [abc0-9]
5. quantifiers allow for a pattern to match a specified number of a unit. + * {2, 7}

```pseudocode
rstring: "r\"" regex* "\""

?regex: basic | group | pipe | class | quantifiers

character: LETTER | NUMBER
word: WORD
?basic: character | word

group: "(" regex* ")"
pipe: regex* "|" regex*

range: LETTER "-" LETTER | NUMBER "-" NUMBER
class: "[" (range*character*)* "]"

?quantifiers: plus_quant | star_quant | num_quant
plus_quant: (group | class | character) "+"
star_quant: (group | class | character) "*"
num_quant: (group | class | character) "{" ( (NUMBER) | (NUMBER ",") | ("," NUMBER) | (NUMBER "," NUMBER) ) "}" 


%ignore /\s+/
%import common.LETTER
%import common.NUMBER
%import common.WORD
```



#### CSV

CSV, which stands for "Comma Separated Values," is a file format to store columnar information.

#### URL

URLs look like the following:

![URL](https://developer.mozilla.org/en-US/docs/Learn/Common_questions/What_is_a_URL/mdn-url-all.png)

For example, in the link `https://cs61a.org/resources/#regular-expressions`, we would have:

- Scheme: `https`
- Domain Name: `cs61a.org`
- Path to the file: `/resources/`
- Anchor: `#regular-expressions`