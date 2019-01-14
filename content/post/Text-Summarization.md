---
title: "Text Summarization"
date: 2019-01-14T12:35:39+05:30
draft: false
tags : [
    "random"
   ]
---

[Source](https://stackabuse.com/text-summarization-with-nltk-in-python/)

The process for summarization a paragraph

> So, keep working. Keep striving. Never give up. Fall down seven times, get up eight. Ease is a greater threat to progress than hardship. Ease is a greater threat to progress than hardship. So, keep moving, keep growing, keep learning. See you at work.

## Paragraph to sentences

```
So, keep working
Keep striving
Never give up
Fall down seven times, get up eight
Ease is a greater threat to progress than hardship
Ease is a greater threat to progress than hardship
So, keep moving, keep growing, keep learning
See you at work

```

## Text Preprocessing

Removing special characters,stop words and numbers

```
keep working
keep striving
never give
fall seven time get eight
ease greater threat progress hardship
ease greater threat progress hardship
keep moving keep growing keep learning
see work
```

## Tokenizing the Sentences

```
['keep',
 'working',
 'keep',
 'striving',
 'never',
 'give',
 'fall',
 'seven',
 'time',
 'get',
 'eight',
 'ease',
 'greater',
 'threat',
 'progress',
 'hardship',
 'ease',
 'greater',
 'threat',
 'progress',
 'hardship',
 'keep',
 'moving',
 'keep',
 'growing',
 'keep',
 'learning',
 'see',
 'work']

 ```

 ## Weighted Frequency of Occurrence

 Each word by dividing its frequency by the frequency of the most occurring word.

 ```

Word	Frequency	Weighted Frequency
ease	    2	            0.40
eight	    1	            0.20
fall	    1	            0.20
get	        1	            0.20
give	    1	            0.20
greater	    2	            0.40
growing	    1	            0.20
hardship	2	            0.40
keep	    5	            1.00
learning	1	            0.20
moving	    1	            0.20
never	    1	            0.20
progress	2	            0.40
see	        1	            0.20
seven	    1	            0.20
striving	1	            0.20
threat	    2	            0.40
time	    1	            0.20
work	    1	            0.20
working	    1	            0.20
```

## Replace Words by Weighted Frequency in Original Sentences

```
Sentence	        Sum of Weighted Frequencies
So, keep working	1 + 0.20 = 1.20
Keep striving	    1 + 0.20 = 1.20
Never give up	    0.20 + 0.20 = 0.40
Fall down seven 
times, 
get up eight	    0.20 + 0.20 + 0.20 + 0.20 +                       0.20 = 1.0
Ease is a greater
threat to progress
than hardship	       0.40 + 0.40 + 0.40 + 0.40                       + 0.40 = 2.0
Ease is a 
greater threat
to progress than 
hardship	        0.40 + 0.40 + 0.40 + 0.40 +                       0.40 = 2.0
So, keep moving,
 keep growing, 
 keep learning	    1 + 0.20 + 1 + 0.20 + 1 + 0.20 = 3.60
See you at work	    0.20 + 0.20 = 0.40
```

## Sort Sentences in Descending Order of Sum

> So, keep moving, keep growing, keep learning. Ease is a greater threat to progress than hardship.