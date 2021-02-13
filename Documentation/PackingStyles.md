# Arrangement of glasses on the page

**Documents**: 
1. [Introduction, and a first placemat](introduction_first_placemat.md); 
2. [Compound Strings and non-ASCII characters](compound_strings_characters.md);
3. [Fonts and glass decoration](fonts_glasses_decoration.md);
4. [Type sizes](type_sizes.md);
5. [Page-level controls](page_level.md);
6. *Arrangement of glasses on the page*;
7. [Non-Glasses Pages](not_glasses.md);
8. [Document-level controls](document.md);
9. [Code injection](code_injection.md);
10.[Bitmap images](bitmap_images.md).

----

## Introduction

The core purpose of the software is to have a place to put glasses. 
Already known are the PaperType (e.g., `/A3`), and how many glasses are to go on the page. 
The user has much control over the layout of the glasses.

The user specifies an array, `PackingStyles`, which is a list of packing styles. 
In turn each style from the list is taken, and each allowed variation is tested. 
Broadly, if a later-tested style allows a larger radius than the current best, then the old best is replaced by this better style.

If the element of `PackingStyles` is just the style, it doesn&rsquo;t need to be in an array. 
But the elements of `PackingStyles` can have constraints and small variations. 
If an element of `PackingStyles` has an such extra detail, then that element must be an array, starting with the style name. 
E.g.,: `[ /Diamonds  /OnlyIfSheetNumMin 1  /OnlyIfSheetNumMax 1  /GlassesNumMin 3  /GlassesNumMax 3  /OnlyIfOrientation /Landscape  /RowsNumMin 3  /RowsNumMax 4  /Mirror ]`. 

The general mathematical problem, largest possible radius for *n* non-overlapping circles in a particular rectangle, is difficult (see [PackoMania](http://www.packomania.com/) for solutions to many special cases). 
This code has enough generality that it often finds the best, and when it can&rsquo;t, such as 14 glasses on `/A3`, its solution is within 1% of the mathematical optimal, and usually much closer. 

For many possible tastings, `PackingStyles` can be left at its default value. 
For example, if there are 24 different Madeiras over four `/A4` pages, the defaults work (though, of course, very important, don&rsquo;t forget to invite [me](http://www.jdawiseman.com/author.html)). 
In such a case the default value of `GlassesOnSheetsMaxPerSheet` would cause `GlassesOnSheets` to be four page-defining arrays each of length six glasses, which would cause the chosen element of `PackingStyles` to be `/RectangularDislocation`.

But if table space were tight, it could be better to have fifteen on an `/A3`, six on an `/A4`, and three on the right side of an `/A4`, so using table space of only 210mm&times;3&frac12; = 735mm per person.

There follow descriptions and pictures of the various allowable styles. 
(The two PDFs ([non-`/Array`](images/PackingStyles.pdf), [`/Array`](images/PackingStyles_Array.pdf)) from which the bitmaps were made show the element of `PackingStyles` in the header.)

## Efficient packings

There are several classes of packing which might use space quite efficiently.

### Diamonds

`/Diamonds`: circles in each row and column lie midway between those in neighbouring rows and columns.

The code tests every number of rows from 1 to the number of glasses. 
If some of these are not wanted, for whatever reason, control is possible by the likes of `[ /Diamonds /RowsNumMin 3 /RowsNumMax 4 ]`.

<div align="center">

| Example | `PackingStyles` element<br>`PaperType` = *width*&times;*height* |
|:-------:|:---------------------------------------|
| ![A4_04_Diamonds](images/A4_04_Diamonds.png) | `/Diamonds`<br>`/A4` = 210mm&times;297mm |
| ![A4_05_Diamonds](images/A4_05_Diamonds.png) | `/Diamonds`<br>`/A4` = 210mm&times;297mm |
| ![A3_13_Diamonds](images/A3_13_Diamonds.png) | `/Diamonds`<br>`/A3` = 420mm&times;297mm |
| ![USLegal_09_Diamonds](images/USLegal_09_Diamonds.png) | `/Diamonds`<br>`/USLegal` = 14&Prime;&times;8&frac12;&Prime; |
| ![USLegal_09_Diamonds_Mirror](images/USLegal_09_Diamonds_Mirror.png) | `[ /Diamonds /Mirror ]`<br>`/USLegal` = 14&Prime;&times;8&frac12;&Prime; |

</div>

### RectangularDislocation

`/RectangularDislocation`: The next four examples are rectangular, optionally with a horizontal &lsquo;dislocation&rsquo; in the middle, that having, `/Diamonds`-style, circles lying between the circles in the adjacent row.

<div align="center">

| Example | `PackingStyles` element<br>`PaperType` = *width*&times;*height* |
|:-------:|:---------------------------------------|
| ![A4_05_RectangularDislocation](images/A4_05_RectangularDislocation.png) | `/RectangularDislocation`<br>`/A4` = 210mm&times;297mm |
| ![A4_06_RectangularDislocation](images/A4_06_RectangularDislocation.png) | `/RectangularDislocation`<br>`/A4` = 210mm&times;297mm |
| ![A3_11_RectangularDislocation](images/A3_11_RectangularDislocation.png) | `/RectangularDislocation`<br>`/A3` = 420mm&times;297mm |
| ![A3_11_RectangularDislocation_Mirror](images/A3_11_RectangularDislocation_Mirror.png) | `[ /RectangularDislocation /Mirror ]`<br>`/A3` = 420mm&times;297mm |

</div>

### SquareGrid

`/SquareGrid` can be similar to `/RectangularDislocation`. 
In the latter the glasses fill the page: observe the six-glass example above, in which the circles touch their vertical neighbours, but have a slight gap from the horizontal neighbour. 
In `/SquareGrid` there is no dislocation, and by default the vertical and horizontal distances are the same and equal to the diameter. 
`/SquareGrid` has two optional one-parameter flags: `/HorizontalAlignment` (which must have a value of one of `/Left`, `/Right`, `/Centre`, or `/Justify`); and `/VerticalAlignment` (one of `/Top`, `/Bottom`, `/Middle`, or `/Justify`). 
Obviously either `/Justify` can allow distances to differ.

<div align="center">

| Example | `PackingStyles` element<br>`PaperType` = *width*&times;*height* |
|:-------:|:---------------------------------------|
| ![USL_06_SquareGrid](images/USL_06_SquareGrid.png) | `/SquareGrid`<br>`/A4` = 210mm&times;297mm |

</div>

### DiamondsAndRectangular

`/DiamondsAndRectangular`: for some numbers of glasses and aspect ratios, the best fit can come from a pattern that is a combination of `/Diamonds` and a rectangular pattern. 
The diamonds can be offset from the diamonds either vertically or horizontally.

<div align="center">

| Example | `PackingStyles` element<br>`PaperType` = *width*&times;*height* |
|:-------:|:---------------------------------------|
| ![A3_14_DiamondsAndRectangular](images/A3_14_DiamondsAndRectangular.png) | `/DiamondsAndRectangular`<br>`/A3` = 420mm&times;297mm |
| ![A3_14_DiamondsAndRectangular_RectColsToLeftOrRowsBelow_0](images/A3_14_DiamondsAndRectangular_RectColsToLeftOrRowsBelow_0.png) | `[ /DiamondsAndRectangular /RectColsToLeftOrRowsBelow 0 ]`<br>`/A3` = 420mm&times;297mm |
| ![A3_14_DiamondsAndRectangular_RectColsToLeftOrRowsBelow_2](images/A3_14_DiamondsAndRectangular_RectColsToLeftOrRowsBelow_2.png) | `[ /DiamondsAndRectangular /RectColsToLeftOrRowsBelow 2 ]`<br>`/A3` = 420mm&times;297mm |
| ![USL2_14_DiamondsAndRectangular](images/USL2_14_DiamondsAndRectangular.png) | `/DiamondsAndRectangular`<br>`/USL2` = 17&Prime;&times;11&Prime; |
| ![USLegal_09_DiamondsAndRectangular](images/USLegal_09_DiamondsAndRectangular.png) | `/DiamondsAndRectangular`<br>`/USL2` = 14&Prime;&times;8&frac12;&Prime; |

</div>

### DiamondsPlus

`/DiamondsPlus` is mostly three-row diamonds (or, if `/Portrait`, three-column), with two extras set between the three rows (columns). 
It is the best packing of seven or ten glasses on several paper sizes.

There is a generalisation of `/DiamondsPlus` over any odd number of rows (columns), not yet coded.

<div align="center">

| Example | `PackingStyles` element<br>`PaperType` = *width*&times;*height* |
|:-------:|:---------------------------------------|
| ![A4_07_DiamondsPlus](images/A4_07_DiamondsPlus.png) | `/DiamondsPlus`<br>`/A4` = 210mm&times;297mm |

</div>

### RectangularAlternateNudge

`/RectangularAlternateNudge`: in this rectangular variant, alternate rows (or columns) are slightly nudged, better to fill the space.

Thus `/RectangularAlternateNudge` is a small deviation away from greater symmetry, about which the the author is unenthusiastic. 
Because of this non-enthusiasm, by default, `/RectangularAlternateNudge` comes with a sub-parameter: `[ /RectangularAlternateNudge /ImprovementPointsMin 2 ]`. 
This imposes an additional requirement: this packing style is chosen only if it is an improvement on the previous best radius of &ge;&nbsp;2pt &asymp;&nbsp;0.7mm. 
The next four examples show six glasses on:
* `/USL` = 8&frac12;&Prime;&times;11&Prime;, with margins of 24pt = &#8531;&Prime; and space of 6pt for the header, using the packing styles /Diamonds (radius &asymp; 117.465);
* `/SquareGrid` and `/RectangularDislocation` (radius = 123); and 
* `/RectangularAlternateNudge` (radius &asymp; 125.568). 

So the radius improves by &asymp; 2.6pt&nbsp;&asymp;0.9mm, and hence the diameter by &asymp; 1.8mm. 
But on `/A4` the improvement in the radius is much less: only &asymp; 0.28pt &asymp; 0.098mm, which seems insufficient to justify the asymmetry&rsquo;s aesthetic damage.

<div align="center">

| Example | `PackingStyles` element<br>`PaperType` = *width*&times;*height* | Radius |
|:-------:|:---------------------------------------|:---|
| ![USL_06_Diamonds](images/USL_06_Diamonds.png) | `/Diamonds`<br>`/USL` = 8&frac12;&Prime;&times;11&Prime; | 117.465pt<br>41.44mm |
| ![USL_06_SquareGrid](images/USL_06_SquareGrid.png) | `/SquareGrid`<br>`/USL` = 8&frac12;&Prime;&times;11&Prime; | 123pt<br>43.39mm |
| ![USL_06_RectangularDislocation](images/USL_06_RectangularDislocation.png) | `/RectangularDislocation`<br>`/USL` = 8&frac12;&Prime;&times;11&Prime; | 123pt<br>43.39mm |
| ![USL_06_RectangularAlternateNudge](images/USL_06_RectangularAlternateNudge.png) | `/RectangularAlternateNudge`<br>`/USL` = 8&frac12;&Prime;&times;11&Prime; | 125.568pt<br>44.30mm |

</div>

### RectangularAlternateSplitNudge

`RectangularAlternateSplitNudge`, by making the nudged rows go in both directions, lessens the aesthetic damage of the non-`Split` nudge, but makes an even smaller gain in the radius. 

<div align="center">

| Example | `PackingStyles` element<br>`PaperType` = *width*&times;*height* |
|:-------:|:---------------------------------------|
| ![USL2_10_RectangularAlternateSplitNudge](images/USL2_10_RectangularAlternateSplitNudge.png) | `/RectangularAlternateSplitNudge`<br>`/USL2` = 17&Prime;&times;11&Prime; |
| ![USL2_12_RectangularAlternateSplitNudge](images/USL2_12_RectangularAlternateSplitNudge.png) | `/RectangularAlternateSplitNudge`<br>`/USL2` = 17&Prime;&times;11&Prime; |
| ![USL2_12_RectangularAlternateSplitNudge_Mirror](images/USL2_12_RectangularAlternateSplitNudge_Mirror.png) | `[ /RectangularAlternateSplitNudge /Mirror ]`<br>`/USL2` = 17&Prime;&times;11&Prime; |

</div>

Both `/RectangularAlternateSplitNudge` and `/RectangularAlternateNudge` admit use of flags `/ProhibitVerticalNudging` or `/ProhibitHorizontalNudging`. 
Obviously using both would be strange.


### Bespoke5 and Bespoke7

`/Bespoke5` and `/Bespoke7` are ignored for more than five and seven glasses, respectively.

<div align="center">

| Example | `PackingStyles` element<br>`PaperType` = *width*&times;*height* |
|:-------:|:---------------------------------------|
| ![A4_05_Bespoke5](images/A4_05_Bespoke5.png) | `/Bespoke5`<br>`/A4` = 297mm&times;210mm |
| ![A4_05_Bespoke5_Mirror](images/A4_05_Bespoke5_Mirror.png) | `[ /Bespoke5 /Mirror ]`<br>`/A4` = 297mm&times;210mm |
| ![USLegal_07_Bespoke7](images/USLegal_07_Bespoke7.png) | `/Bespoke7`<br>`/USLegal` = 14&Prime;&times;8&frac12;&Prime; |
| ![USLegal_07_Bespoke7_Mirror](images/USLegal_07_Bespoke7_Mirror.png) | `[ /Bespoke7 /Mirror ]`<br>`/USLegal` = 14&Prime;&times;8&frac12;&Prime; |

</div>

### Temple

`/Temple` is an intricate pattern, that has the largest radius for 10 glasses on `/USL`, and for 13 glasses on either `/USLegal` or `/USL2`. 
The sub-parameter `/TempleExtraColsToLeftOrRowsBelow` is followed by one integer, and is to `/Temple` as `/RectColsToLeftOrRowsBelow` is to `/DiamondsAndRectangular`.

<div align="center">

| Example | `PackingStyles` element<br>`PaperType` = *width*&times;*height* |
|:-------:|:---------------------------------------|
| ![USL_10_Temple](images/USL_10_Temple.png) | `/Temple`<br>`/USL` = 8&frac12;&Prime;&times;11&Prime; |
| ![USLegal_13_Temple](images/USLegal_13_Temple.png) | `/Temple`<br>`/USLegal` = 14&Prime;&times;8&frac12;&Prime; |
| ![USL2_13_Temple_TempleExtraColsToLeftOrRowsBelow_0](images/USL2_13_Temple_TempleExtraColsToLeftOrRowsBelow_0.png) | `/Temple`<br>`/USL2` = 17&Prime;&times;11&Prime; |

</div>

## Inefficient packings

There are classes of packing which, though they can have decorative or other advantages, are not space efficient.

### Arch, and PostsAndLintel

`/PostsAndLintel` arranges the circles around the left, top and right edges of the page, optionally with some circles at the bottom centre. 
This design might be particularly appropriate if the central circles held the candidate blends of a vintage, with some of the components around the edge. 
`/Arch` is similar, with the circles on a half ellipse.

<div align="center">

| Example | `PackingStyles` element<br>`PaperType` = *width*&times;*height* |
|:-------:|:---------------------------------------|
| ![A3_10_Arch_CentralGlasses_3](images/A3_10_Arch_CentralGlasses_3.png) | `[ /Arch /CentralGlasses 3 ]`<br>`/A3` = 420mm&times;297mm |
| ![A3_08_PostsAndLintel_CentralGlasses_1](images/A3_08_PostsAndLintel_CentralGlasses_1.png) | `[ /PostsAndLintel /CentralGlasses 1 ]`<br>`/A3` = 420mm&times;297mm |
| ![A3_10_PostsAndLintel_CentralGlasses_2_Mirror](images/A3_10_PostsAndLintel_CentralGlasses_2_Mirror.png) | `[ /PostsAndLintel /CentralGlasses 2 /Mirror ]`<br>`/A3` = 420mm&times;297mm |

</div>

### Sides, LeftSide, RightSide, TopRow, MiddleRow, BottomRow

`/Sides`, `/LeftSide`, `/RightSide`, `/TopRow`, `/MiddleRow`, and `/BottomRow` are mostly self-explanatory. 

`/RightSide` (and, *mutatis mutandis*, `/LeftSide`) have a particular use. 
Consider a tasting with 17 glasses. 
This could be set as 6 + 6 + 5 on 3&times;`/A4`. 
But if table space were tight, 14 on 1&times;`/A3` and 3 on 1&times;`/RightSide` `/A4` would use only 2&frac12; `/A4` widths, if the unused half of the `/A4` were tucked under the `/A3`. 
Suppressing the ornaments tucked under the `/A3`, such as `HeadersCenter`, would look neater. 
This can be done by adding to the array an extra flag, `/SuppressNonRightOrnaments` (or `/SuppressNonLeftOrnaments`), which for the pages using that packing style suppresses the unwanted headers, footers, icons, and water boxes. 
Example item of PackingStyles: `[ /RightSide /GlassesNumMax 3 /SuppressNonRightOrnaments ]`.

<div align="center">

| Example | `PackingStyles` element<br>`PaperType` = *width*&times;*height* |
|:-------:|:---------------------------------------|
| ![A3_06_Sides](images/A3_06_Sides.png) | `Sides`<br>`/A3` = 420mm&times;297mm |
| ![A3_04_TopRow](images/A3_04_TopRow.png) | `TopRow`<br>`/A3` = 420mm&times;297mm |
| ![A3_04_BottomRow](images/A3_04_BottomRow.png) | `BottomRow`<br>`/A3` = 420mm&times;297mm |
| ![A3_04_MiddleRow](images/A3_04_MiddleRow.png) | `MiddlemRow`<br>`/A3` = 420mm&times;297mm |
| ![A4_03_LeftSide](images/A4_03_LeftSide.png) | `/LeftSide`<br>`/A4` = 297mm&times;210mm |
| ![A4_03_RightSide](images/A4_03_RightSide.png) | `/RightSide`<br>`/A4` = 297mm&times;210mm |

</div>

## Array: custom arrangements

It is possible to specify an arrangement with an array, thus:
```Postscript
[ /Array /Positions [0 2] [2 2] [4 2] [6 2]  [0 1] [3 1] [6 1]  [0 0] [3 0] [6 0] ]
```
The style is `/Array`. 
That can have any of the selection controls, such as `/OnlyIfOrientation /Landscape`. 
After which is `/Positions`. 
After the `/Positions` marker is a list of points, typically of the form `[x y]`, with *y* increasing up the page. 
The code then chooses the radius and separately scales the *x* and *y* directions such that things fit as snugly as possible, obviously subject to the other upper bounds on the radius. 
The glass ordering is that given in the array: there is no subsequent sorting or ordering.

There is a more complicated variant, in which some of the sub-arrays are of the form `[x y x' y']`. 
The first two elements are used, as before, and fix the radius and the canvas. 
The circle at (*x*,*y*) is then moved in a straight line towards (*x'*,*y'*). 
A circle stops moving if it collides with another circle (a tangential touch not being a collision); if it collides with the edge of the page; or it arrives at (*x'*,*y'*).

The example image shows an alternation of the previous code extract, with:
```Postscript
[ /Array /Positions [0 2] [2 2 3 2] [4 2 3 2] [6 2]  [0 1] [3 1] [6 1]  [0 0] [3 0] [6 0] ]
```

<div align="center">

![A3_10_Array](images/A3_10_Array.gif)

</div>

The difference is the movement of the circles at (2,2) and (4,2), both towards (3,2). 
For the author&rsquo;s taste, the closer relationship of the two B0 circles means they should be touching, rather than equally spaced between A0 and C0.

## Other flags, constraints, and sub-parameters

There are other flags and constraints and sub-parameters, as follows.

* `/Mirror`: the alternate chirality. 
If there isn&rsquo;t a sensible meaning to this, ignored.

* `/ShoveLeft` and `/ShoveRight`: if there is spare space between the circles, probably because the radius has been shrunk to that on another sheet, the circles are shoved leftwards (or rightwards) against that margin. 
But not heeded in every base style.

* `/PackingDirectionTopToBottom bool` and `/PackingDirectionLeftToRight bool` and `/PackingNestingColumnMajor bool`: by default most layouts start at the top-left, work across to the top-right, then start the second row slightly further down on the left. 
This can be changed: glasses can run right-to-left, bottom-to-top, and the nesting order of columns and rows can be exchanged. 
For large pre-poured tastings on `/A3` or `/USL2`, generally one pre-pours the youngest first. 
If these are in the front row, it is more fiddly to lower subsequent older vintages into place. 
Adding `/PackingNestingColumnMajor true` fixes this. 
(The global value of `PackingNestingColumnMajor` is the default value within PackingStyles, and also affects the ordering in Cork-Display pages.)

* `/ProhibitVerticalNudging` or `/ProhibitHorizontalNudging`: have the obvious effect in base styles `/RectangularAlternateNudge` and `/RectangularAlternateSplitNudge`.

* `/RectColsToLeftOrRowsBelow int` chooses the position of the diamonds-style block in `/DiamondsAndRectangular`.

* `/TempleExtraColsToLeftOrRowsBelow int` chooses the position of the &lsquo;hole&rsquo; in `/Temple`.

* `/CentralGlasses int`: both `/PostsAndLintel` and `/Arch` packings can have 0, 1, 2, or 3 glasses in the centre, the remainder running round the edge or semi-ellipse.

* `/RowsNumMin int` and `/RowsNumMax int`: minimum and maximum number of rows permitted. 
Relevant in the `/Diamonds`, `/RectangularDislocation`, `/SquareGrid`, `/RectangularAlternateNudge`, and `/PostsAndLintel` packing styles.

* `/OnlyIfSheetNumMin int` and `/OnlyIfSheetNumMax int`: specifying permitted values for the internal variable SheetNum, which is 0 on the first sheet, 1 on the second, etc.

* `/GlassesNumMin int` and `/GlassesNumMax int`: permitted number of glasses. 
If outside range, this packing specification not used.

* `/OnlyIfOrientation name`, the sub-parameter being one of `/Landscape`, `/Portrait`, or `/Either`, the last being the default if this sub-parameter absent. 
If `Orientation` not matching, this packing specification not used.

* `/ImprovementPointsMin num` and `/ImprovementProportionMin num`: this specification used only if beating previous best by the required amount, either absolute (e.g., 2 points) or as a proportion (e.g., 0.01 = 1%).

If `PackingStyles` is empty, or contains only invalid/impossible layouts, then instead several of the regular layouts are tried.


## Radius constraints

There is aesthetic merit in imposing that radii are consistent across pages within a single session. 
This is controled by `ShrinkRadii`, which can be:
* `/NotAtAll`, which leaves each page at its own best possible;
* `/ToSmallestSamePageOrdering`, which ensures consistency within each session;
* `/ToSmallest`, which ensures consistency over the whole document;
* `[ 0 0 0 … 1 1 1 … 2 2 ]`, which is an arbitrary array of the same length as `GlassesOnSheets`, pages&rsquo; radii being forces to their lesser if elements satisfy PostScript&rsquo;s `eq` condition.

There is also the simple numerical parameter `MaxRadius`, defaulting to 150 &rArr; diameter &le;&nbsp;300pt =&nbsp;4&#8537;&Prime; &asymp;&nbsp;106mm.


## Code extracts

Some extracts from the code used to make the many examples on this page.

```Postscript
/ThePortForumIconPlacement /None def

/VoteRecorders false def
/CorkDisplayNumCopies 0 def
/NeckTagsNumCopies 0 def
/TastingNotePagesNumCopies 0 def
/DecantingNotesNumCopies 0 def

/TitlesFont     /LucidaGrande-Bold def
/CircletextFont /LucidaGrande-Bold def
/HeaderFont     /LucidaSans-TypewriterBold def

/FontSizesRatioTitlesMin 999 def

/CircletextsMinNumSpacesBetween 1.5 def
/CircletextMaxFontSizeAbsolute 12 def

/InlineTitles false def

/WaterBoxes /None def

/ShrinkRadii /NotAtAll def
/MaxRadius 9999 def

/OutputLogToPage false def
```
