# Debugging

**Documents**: 
1.  [Introduction, and a first placemat](introduction_first_placemat.md);  
2.  [Compound Strings and non-ASCII characters](compound_strings_characters.md);  
3.  [Fonts and glass decoration](fonts_glasses_decoration.md);  
4.  [Type sizes](type_sizes.md);  
5.  [Page-level controls](page_level.md);  
6.  [Arrangement of glasses on the page](PackingStyles.md);  
7.  [Non-Glasses Pages](not_glasses.md);  
8.  [Document-level controls](document.md);  
9.  [Code injection](code_injection.md);  
10. [Bitmap images](bitmap_images.md);  
11. [Translations](translations.md);  
12. *Debugging*.

----

<div style="clear: both;"></div>

## Introduction

PostScript is a language with much beauty and power, but it is painful to debug. 
Consider the following near-minimal program.

```PostScript
%!PS

0 sub
```
Of course, this fails: from what is 0 to be subtracted? 
The log file reports:
```
%%[ Error: stackunderflow; OffendingCommand: sub ]%%

Stack:
0
```

Observe: no line number. 
The placemat code has &asymp;2.8k instances of `sub`, and the programmer is told only that an unspecified one of them has failed. 
As written in *Port Vintages* (2018), J. D. A. Wiseman:

> “If you don’t ﬁnd it in the index, look very carefully through the entire catalogue”, *Sears Roebuck and Co., Consumers Guide* (1897), as quoted in *The Art of Computer Programming: Volume 3, Sorting and Searching* (1973), Donald E. Knuth. 

Luckily, we can sometimes do better than to &ldquo;look very carefully&rdquo; through the whole program. 
Built-in to the software is some diagnostic assistance. 
However, if the failure is in the parameters, before the diagnostics are enabled, then this assistance will be absent.


## Error reporting in PostScript

If the code fails while parameters are being set, then PostScript&rsquo;s error reporting is what you have. 
Consider `/Titles [ ThisNotDefined ] def`. 
This fails:
```
%%[ Error: undefined; OffendingCommand: ThisNotDefined ]%%

Stack:
-mark-
/Titles
```

Being told that `ThisNotDefined` is undefined can be a lot of help. 
It might be as simple as a typo. 
If it is, find and fix.

Even if the error is more subtle, the stack is typically enough to deduce the approximate location of the problem. 
Reading from the bottom, the stack starts with `/Titles`: the problem may well have arisen while defining the Titles. 
(The `-mark-` in the stack is `[` or `<<` or `mark`, usually the first of them.) 

Often, but not always, these suffice. 
But sometimes errors are fiddlier, especially with [injected code](code_injection.md). 


## Diagnostic assistance

### Basics

Failures can happen in the software because of bugs int he software itself, or because of a bug in [injected code](code_injection.md). 

As with the built-in error support, the log will show the error, and the state of the stack. 
It will also show the value of `TypeOfPagesBeingRendered`, though the value `/DistillerLog` can mean a generic page. 

Next in the log will be the contents of the top three dictionaries on the dictionary stack. 
Distinctive variables in these can be a great help in locating the place of failure. 
Values of these variables can help more.

### DeBugLevel

Finally, one of the first names defined within the code, so shortly below the parameters, is `DeBugLevel`. 
`DeBugLevel` defaults to 65535, and all values larger than 100 are equivalent do-nothing values.

Most sub-routines in the code begin with a line resembling
```PostScript
	DeBugLevel 25 le {(+ShellSort) OutputToLog} if
```
and end with a matching line
```PostScript
	DeBugLevel 25 le {(-ShellSort) OutputToLog} if
```

There are also a few similar lines beginning with a space, within (rather at the boundary of) a block of code.

So if `DeBugLevel` is &le;100, the code will log its progress. 
Smaller numbers are smaller more-core routines, causing the log to be more verbose. 
`DeBugLevel` is primarily for the programmer rather than users, but can be if use to the latter.


## Bugs

If the bug is in the software, please raise an [issue](http://github.com/jdaw1/placemat/issues). 
Take an expansive view of a bug: call it a bug if the failure was within your injected code, but that might have succeeded if the software had been more generous.

A significant proportion of bugs found related to injected code: please report problems.
