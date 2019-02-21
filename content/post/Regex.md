---
title: "Regex"
date: 2019-02-20T17:59:03+05:30
draft: False,
tags : [
    "random",
   ]
---
# [Regex](https://dev.to/emmawedekind/regex-cheat-sheet-2j2a)

Uses `test() `to get a boolean response and `match()` to extract the match


## Patterns


`/blah/` -> For finding characters
`/yes|no|maybe/;` - > `|` for OR condition

Eg:

```
let testString = "My test string";
let testRegex = /string/;
testRegex.test(testString);
```
---
`i` for case sensitivity

```
const match = "Hello World!".match(/hello/i); // "Hello"
````

---

`g` to extract all matches in an array

---

Uses `.` as a placeholder

```
// To match "cat", "BAT", "fAT", "mat"

const regexWithWildcard = /.at/gi;
const testString = "cat BAT cupcake fAT mat dog";
const allMatchingWords = testString.match(regexWithWildcard); 
// ["cat", "BAT", "fAT", "mat"]

```


```
// Match "cat" "fat" and "mat" but not "bat"

const regexWithCharClass = /[cfm]at/g;
const testString = "cat fat bat mat";
const allMatchingWords = testString.match(regexWithCharClass); 

// ["cat", "fat", "mat"]

```
----

### For range of al[habets]
```


const regexWithCharRange = /[a-e]at/;
const catString = "cat";
const batString = "bat";
const fatString = "fat";

regexWithCharRange.test(catString); // true
regexWithCharRange.test(batString); // true
regexWithCharRange.test(fatString); // false

```
---

### To negate

```
const allCharsNotVowels = /[^aeiou]/gi;
const allCharsNotVowelsOrNumbers = /[^aeiou0-9]/gi;

```

---

### Match occurrences n times

Use the asterisk *

`const zeroOrMoreOsRegex = /hi*/gi;`


---

### Lazy matching

- Defaultly matches the longest.So use ?

```
const testString = "catastrophe";
const greedyRexex = /c[a-z]*t/gi;
const lazyRegex = /c[a-z]*?t/gi;

testString.match(greedyRexex); // ["catast"]
testString.match(lazyRegex); // ["cat"]

```

### `^` for matching character at the beginning

`const startingStringRegex = /^Emma/;`

---

### Ending Patterns

`const startingStringRegex = /Emma$/;`

---

##  Alphanumeric

```
const longHand = /[A-Za-z0-9_]+/;
const shortHand = /\w+/;
```

## Everything except letters & numbers

```
const noAlphaNumericCharRegex = /\W/gi;
const weirdCharacters = "!_$!!";
const alphaNumericCharacters = "ab283AD";

noAlphaNumericCharRegex.test(weirdCharacters); // true
noAlphaNumericCharRegex.test(alphaNumericCharacters); // false

```

## Numbers

```

const digitsRegex = /\d/g;
const stringWithDigits = "My cat eats $20.00 worth of food a week.";

stringWithDigits.match(digitsRegex); // ["2", "0", "0", "0"]


// Non-numbers `\D`

```

### Bits

`\s` - > Whitespace

`\S` - > Non-whitespace

`{lowerBound, upperBound}` ->  /hi{1,4}/

`{lowerBound,}`

`{requiredCount}`