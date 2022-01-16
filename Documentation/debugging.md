# Debugging

**Link to the main program**: [placemat.ps](../PostScript/placemat.ps?raw=1)

**Links to documentation**: 
&#9654;&#xFE0E;&nbsp;[Introduction,&nbsp;and&nbsp;a&nbsp;first&nbsp;placemat](introduction_first_placemat.md#readme)&nbsp; 
&#9654;&#xFE0E;&nbsp;[Fonts&nbsp;and&nbsp;glass&nbsp;decoration](fonts_glasses_decoration.md#readme)&nbsp; 
&#9654;&#xFE0E;&nbsp;[Compound&nbsp;Strings&nbsp;and&nbsp;non&#8209;ASCII&nbsp;characters](compound_strings_characters.md#readme)&nbsp; 
&#9654;&#xFE0E;&nbsp;[Page&#8209;level&nbsp;controls](page_level.md#readme)&nbsp; 
&#9654;&#xFE0E;&nbsp;[Arrangement&nbsp;of&nbsp;glasses&nbsp;on&nbsp;the&nbsp;page](PackingStyles.md#readme)&nbsp; 
&#9654;&#xFE0E;&nbsp;[Non&#8209;Glasses&nbsp;Pages](not_glasses.md#readme)&nbsp; 
&#9654;&#xFE0E;&nbsp;[Document&#8209;level&nbsp;controls](document.md#readme)&nbsp; 
&#9654;&#xFE0E;&nbsp;[Type&nbsp;sizes](type_sizes.md#readme)&nbsp; 
&#9654;&#xFE0E;&nbsp;[Translations](translations.md#readme)&nbsp; 
&#9654;&#xFE0E;&nbsp;[Code&nbsp;injection](code_injection.md#readme)&nbsp; 
&#9654;&#xFE0E;&nbsp;[Bitmap&nbsp;images](bitmap_images.md#readme)&nbsp; 
&#9655;&#xFE0E;&nbsp;*Debugging*

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
But sometimes errors are fiddlier, especially with [injected code](code_injection.md#readme). 


## Diagnostic assistance

### Basics

Failures can happen in the software because of bugs in the software itself, or because of a type error in a parameter, or because of a bug in [injected code](code_injection.md#readme). 

As with the built-in error support, the log will show the error, and the state of the stack. 
It will also show the value of `TypeOfPagesBeingRendered`, though the value `/DistillerLog` can mean a generic page. 

Next in the log will be the contents of the top three dictionaries on the dictionary stack. 
Distinctive variables in these can be a great help in locating the place of failure. 
Values of these variables can help more.

### DeBugLevel

One of the first names defined within the code, so shortly below the parameters, is `DeBugLevel`. 
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
`DeBugLevel` is primarily for the programmer rather than users, but can be of use to the latter. 
If I&rsquo;m having difficulty, standard practice is:
```PostScript
/DeBugLevel 40 def
```


## WatchExpression

Two small routines can help debug injected code. 

* `WatchExpression` is a simple monitor of a variable. E.g., `/WithinTitles WatchExpression` outputs to the log a line resembling `WithinTitles   =   2`. The item passed can be a name, or `{code}`. If it is an undefined name, then that is safely reported as &ldquo;&#8209;&#8209;Undefined&#8209;&#8209;&rdquo;. But if the parameter is code then the user is not shielded from it failing.

* `WatchExpressions`, plural, takes an array, each item of which is as for `WatchExpression`. E.g.:
```PostScript 
[ /TypeOfPagesBeingRendered  /NameNum /ThisName  /SheetNum /WithinPage /WithinTitles ]  WatchExpressions
```

A few `WatchExpressions` can ease the debugging of injected code.


## Bugs

If the bug is in the software, please raise an [issue](http://github.com/jdaw1/placemat/issues). 
Take an expansive view of a bug: call it a bug if the failure was within your injected code, but that might have succeeded if the software had been more generous.

A significant proportion of bugs found related to injected code: please report problems.
