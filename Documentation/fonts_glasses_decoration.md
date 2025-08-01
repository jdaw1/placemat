# Fonts and glass decoration

**Link to the main program**: [placemat.ps](../PostScript/placemat.ps?raw=1)

**Links to documentation**: 
&#9654;&#xFE0E;&nbsp;[Introduction,&nbsp;and&nbsp;a&nbsp;first&nbsp;placemat](introduction_first_placemat.md#readme)&nbsp; 
&#9655;&#xFE0E;&nbsp;*Fonts&nbsp;and&nbsp;glass&nbsp;decoration*&nbsp; 
&#9654;&#xFE0E;&nbsp;[Compound&nbsp;Strings&nbsp;and&nbsp;non&#8209;ASCII&nbsp;characters](compound_strings_characters.md#readme)&nbsp; 
&#9654;&#xFE0E;&nbsp;[Page&#8209;level&nbsp;controls](page_level.md#readme)&nbsp; 
&#9654;&#xFE0E;&nbsp;[Arrangement&nbsp;of&nbsp;glasses&nbsp;on&nbsp;the&nbsp;page](PackingStyles.md#readme)&nbsp; 
&#9654;&#xFE0E;&nbsp;[Non&#8209;Glasses&nbsp;Pages](not_glasses.md#readme)&nbsp; 
&#9654;&#xFE0E;&nbsp;[Document&#8209;level&nbsp;controls](document.md#readme)&nbsp; 
&#9654;&#xFE0E;&nbsp;[Type&nbsp;sizes](type_sizes.md#readme)&nbsp; 
&#9654;&#xFE0E;&nbsp;[Translations](translations.md#readme)&nbsp; 
&#9654;&#xFE0E;&nbsp;[Code&nbsp;injection](code_injection.md#readme)&nbsp; 
&#9654;&#xFE0E;&nbsp;[Bitmap&nbsp;images](bitmap_images.md#readme)&nbsp; 
&#9654;&#xFE0E;&nbsp;[Debugging](debugging.md#readme)

----

## Abovetitles, Overtitles, and FillTexts

<img align="right" width="476" height="477" src="images/Circlearrays_Titles_Abovetitles_Belowtitles_Overtitles_FillTexts.png">

The [Introduction](introduction_first_placemat.md#readme) discussed the array parameters `Circlearrays`, `Titles`, and `Belowtitles`.
Also there are analagous parameters `Abovetitles` and `Overtitles`, and text can also be put into `FillTexts`, as shown in the nearby image.

All these arrays must be of the same length. 
If they are not, distillation will output some explanation to the log, and then terminate.

This profusion of places to put information should be used sparsely, and consistently. 
For example, in a vertical, the `Titles` might contain two-digit years, and the `Overtitles` a concise version of the name of the shipper or quinta or winery or ch&acirc;teau or distillery. 
Most `Abovetitles` would be blank =&nbsp;`()`, only a few specifying a non-standard bottle size such as &ldquo;Double Magnum&rdquo;. 
Most `Belowtitles` would be blank, only a few specifying the likes of &ldquo;Cask Sample&rdquo;.

Extracts of code that made the image, for later explanation:
```PostScript
/ColourSchemeTitles /MidGrey def
/FontSizesSetsAboveBelowOver [ 0 0 1 ] def
/InlineTitles false def
/FillTitles true def
/CircletextFontSize 12 def
```

## Circlearrays

The number of copies of each instance of `Circlearrays` is constrained by `CircletextsMinCopies` and `CircletextsMaxCopies`. 
When the latter is used, the &lsquo;current number&rsquo; of copies is on the stack. 
This allows a default value of `/CircletextsMaxCopies {dup 32 gt {dup dup 4 mod sub} {65535} ifelse} bind def`: if there are more than 32, the number is slightly reduced to a multiple of 4. 

Very rarely used, there are also the self-explanatory `CirclearraysFillBehind` and `CirclearraysFillBehindCode`.



## Colours

In the previous image the `Titles` are grey, but the `Overtitles` and others are black. 
There are four relevant parameters, which can take the values `/MidGrey` or `/Black`.
```PostScript
/ColourSchemeTitles      /MidGrey def
/ColourSchemeAbovetitles /Black   def
/ColourSchemeBelowtitles /Black   def
/ColourSchemeOvertitles  /Black   def
```
## Fonts

The code may access any fonts appropriately installed on the machine doing the PS&nbsp;&rarr;&nbsp;PDF conversion. 
Fonts are accessed by their PostScript name. 
On a Mac, in the application *Font Book*, select a font and its PostScript name is shown. 
It is more difficult on Windows &mdash; a search engine can assist. 
Or, **much recommended, distill the file [fonts_illustrated.ps](../PostScript/fonts_illustrated.ps?raw=1), which makes a document showcasing the available fonts**. 

By default fonts are set as follows.
```PostScript
/TitlesFont          [ /TrebuchetMS-Bold /Helvetica-Bold ] def
/CircletextFont      [ /TrebuchetMS      /Helvetica      ] def
/AbovetitlesFont     {TitlesFont} def
/BelowtitlesFont     {AbovetitlesFont} def
/OvertitlesFont      {TitlesFont} def
/NamesFont           {PlaceNames {TitlesFont} {CircletextFont} ifelse} bind def
/SubtitlesFont       {OvertitlesFont} def
/FillTextFont        {TitlesFont} def

/PlaceNamesFont      {NamesFont} def
/BackgroundTextsFont {TitlesFont} def

/HeaderFont          {CircletextFont} def
/FooterFont          {HeaderFont} def
```

A font name can be set to the name of a font: fair enough. 
Or it can be set to an array of font names, the code choosing the first of these that seems to be available. 
I like `/TrebuchetMS-Bold` for the `TitlesFont`, but if distilling online it likely won&rsquo;t be available, so the vanilla `/Helvetica-Bold` is substituted.

In the above&mdash;and readers have not have been introduced to where all these are used&mdash;`TitlesFont` and `/CircletextFont` have been set, the the other font parameters copying them. 
This is quite usual.

<div align="center">

[![Font examples, including from families Gotham, DejaVuSerif, DejaVuSans, Trebuchet, Times, Didot, Cochin, Harrington](images/font_examples.png)](images/font_examples.pdf)

</div>

Other good fonts to use include: 
various weights of `/Gotham`, being a sans-serif font with a hint of drama; 
`DejaVuSerif` and `/DejaVuSans`, which have many unicode characters; 
`/TimesNewRomanPS-BoldMT`, which has glyphs for effectively all the accent-letter combinations; 
`/Didot` and `/Didot-Bold` (the bold being a slightly decorative but stylish choice for the titles of a vertical which are hence digits); 
`/Cochin` and `/Cochin-Bold` (Port-style titles of the form &lsquo;T70&rsquo; being particularly fine); 
`/Harrington` (mischievously over-ornate); 
and many others. 

There is another fussiness in this default. 
Mostly, the curly brackets are unnceccessary. 
Mostly, `/OvertitlesFont TitlesFont def` would work as well as `/OvertitlesFont {TitlesFont} def`. 
The former sets `OvertitlesFont` to a value. 
The latter sets `OvertitlesFont` to code, which is later executed. 
If `TitlesFont` were itself code, such that its output depended on an internal variable such as `WithinTitles`, the latter would be necessary. 
And indeed, `NamesFont` is set to a little code, that is executed each time `NamesFont` is needed. 
(The `bind` is a slight optimisation, which could have been omitted.)

As of the third millennium, most programming environments frown on code injection. 
But in this PostScript program [code injection](code_injection.md#readme) is allowed, often encouraged, and occasionally necessary. 
Those not comfortable with that may safely leave such parameters at their default values. 

## CrossHatching

<img align="right" width="485" height="266" src="images/CrossHatching.png">

The SW63 example shows the check pattern CrossHatching, with `InlineTitles` also `true`. 
There are multiple places this feature can go. 
* Within the Titles, Abovetitles, Belowtitles, or Overtitles (as in the example image). 
* *Inside* the circle, but behind the large text pieces. 
* In the &lsquo;unused&rsquo; space *Outside* the circles, i.e., between the circles. 
Some parameters are consistent across these, so that they align, some differ. 

Again, these possibilities are enabled by some Booleans. 

```PostScript
/CrossHatchingOutside false def
/CrossHatchingInside false def
/CrossHatchingTitles false def
/CrossHatchingAbovetitles {CrossHatchingTitles} def
/CrossHatchingBelowtitles {CrossHatchingTitles} def
/CrossHatchingOvertitles {CrossHatchingTitles} def
/CrossHatchingPlaceNames {CrossHatchingTitles} def
```

The polar gridlines originate from a point with *x* coordinate `CrossHatchingCentreX`, which can take values of `/Name`, `/Left`, `/Center`, `/Right`, or a number being points from the left edge of the page. 
At a big tasting there can be multiple sheets of glasses, and it&rsquo;s more elegant to have the pattern consisent across pages. 
For which `CrossHatchingCentreX` can be `/CenterSheetsSamePageOrdering`: if each person&rsquo;s glasses sheets for this session are in a single row, all the circles and lines originate from the common *x*-centre. 
The *y* coordinate `CrossHatchingCentreY` has possible values `/Name`, `/Bottom`, `/Middle`, `/Top`, or points from the bottom of the page. 

This structure is typical of many of the parameters: the user can choose a value; or can access some pre-written logic by name.

There is another sense in which `CrossHatching` is typical of many features. 
There are a few essential controls. 
And there are many other controls which can almost always remain at their default values, but which may be changed by a fussy user. 
In parts of this documentation such parameters are headed &ldquo;superfluous&rdquo;.

### Superfluous

The number of straight lines is `CrossHatchingNumRadialLines`, defaulting to `80` so 4&frac12;&deg; apart. 
The radii are chosen such that each cell has area `CrossHatchingCellArea`, defaulting to `1296`&nbsp;pt&sup2; = (36pt)&sup2; = (&frac12;&Prime;)&sup2; = (12.7mm)&sup2; = 161.29mm&sup2;.

`CrossHatchingOutsideToPaperEdge` is a Boolean affecting the &lsquo;Outside&rsquo; lines: to paper edge, or to the internal margin? 

Lines are formatted and stroked by the code in `CrossHatchingTitlesStrokeCode`. 
The code must include the `stroke`, this requirement permitting the likes of `gsave 0 setgray 2.4 setlinewidth stroke grestore 1 setgray 0.96 setlinewidth stroke`. 
And analogous `stroke`ing code `CrossHatchingAbovetitlesStrokeCode`, `CrossHatchingBelowtitlesStrokeCode`, and `CrossHatchingOvertitlesStrokeCode`, `CrossHatchingInsideStrokeCode`, `CrossHatchingOutsideStrokeCode` (`CrossHatchingPlaceNames` uses the sub-parameters of CrossHatchingTitles). 
Sometimes used with `CrossHatchingInside` and `CrossHatchingOutside` is `CirclearraysFillBehind`, which fills behind the annulus containing the `Circlearrays` by executing `CirclearraysFillBehindCode`.

The Inside lines (inside the circle but behind the various titles) are less elegant on some other page types. 
Their presence is controlled by `NeckTagsShowCrossHatchingInside`, `DecanterLabelsShowCrossHatchingInside`, and `BottleWrapShowCrossHatchingInside`.

Extracts of code that made the image:
```PostScript
/CrossHatchingTitles true def
/CrossHatchingTitlesStrokeCode     {0 setgray 0.24 setlinewidth stroke} def
/CrossHatchingOvertitlesStrokeCode {1 setgray 0.72 setlinewidth stroke} def
/CrossHatchingCellArea 576 def  % (24pt)^2, (0.333333")^2, (8.466666mm)^2
/InlineTitles true def
/ColourSchemeTitles /Black def
/OvertitleMaxFontSizeProportionTitles  0.333333 def
```

## Shapes: stars and flowers and hearts

<img align="right" width="504" height="222" src="images/Shapes.png">

In the cluttered image optimistically showing D78, the Titles and Belowtitles contain small random flowers and stars and hearts and circles. 

These are enabled by Booleans `ShapesInTitles`, with obvious variations `ShapesInAbovetitles`, `ShapesInBelowtitles`, `ShapesInOvertitles`, and `ShapesInPlaceNames`. 
The array `ShapesToUse` defaults to `[ /Flower /Star /Heart /Circle ]`, and must contain at least one of these.

Each shape is filled with the code `ShapesTitlesFill` (or `ShapesAbovetitlesFill`, `ShapesBelowtitlesFill`, `ShapesOvertitlesFill`), which, if the shapes are `fill`ed, should end with a `fill`. 
After which `ShapesTitlesStroke` (or `ShapesAbovetitlesStroke`, `ShapesBelowtitlesStroke`, `ShapesOvertitlesStroke`) which should end with a `stroke`.
The internal variables `ShapesIntX` and `ShapesIntY` hold that shape&rsquo;s position within the whole; these can be accessed by the painting-code parameters to choose from amongst a set of colourings. 

The radius of each shapes&rsquo;s enclosing circle is random in the range `ShapesEnclosingCircleRadiusMin` to `ShapesEnclosingCircleRadiusMax`. 
An approximation to the typical centre-to-centre separation between adjacent shapes is `ShapesAverageSeparation`; a parameter controlling how far stars are moved from a regular grid is `ShapesAverageMaxTweakPlusMinus`. 
The pattern generates some shapes that are not shown, that are clipped away: if `ShapesPrintQuickerDistillSlower` is `true` these are removed, reducing file size and improving print speed at the price of slowing distillation.

Sometimes, albeit rarely, this `clip`ping is not wanted. 
For instance, if the stars are filled white with no border, the clipping achieves no good. 
Not only no good, but there can be a tiny bleed between the underlying letter&rsquo;s fill and the clipped shape, such that a very thin black border remains. 
Or this non-`clip`ping might be wanted for visual effect. 
Whatever the reason, controlled with the Boolean parameters `ShapesTitlesClip`, `ShapesAbovetitlesClip`, `ShapesBelowtitlesClip`, `ShapesOvertitlesClip`, `ShapesPlaceNamesClip`, for which true means do clip. 
However, it can be an aesthetic fail if all of: filled white with no border; not `clip`ped; `CrossHatchingInside` or `OutlineTitles` being `true`.

Some parameters affect just one of the possible values of `ShapesToUse`.

For the stars, the numbers of points and the step between points are chosen randomly from within `ShapesStarsPointsAndStepsArray`, the default being `[[5 2] [6 2] [7 2] [7 3] [8 3]]`. 
A possible alternative value for ShapesStarsPointsAndStepsArray is `[[3 1.318] [4 1.792] [5 2.278] [6 2.77]]`, being pointier and less polygonal. 

For the flowers the number of petals is chosen randomly from `ShapesFlowersNumPetalsMin` to `ShapesFlowersNumPetalsMax`, and, as a proportion of 360&deg; divided by the number of petals, the angular width of each is chosen randomly from the range `ShapesFlowersAngularWidthMin` to `ShapesFlowersAngularWidthMax`.

Extracts of code that made the image for the Dow &rsquo;78:
```PostScript
/ColourSchemeTitles /Black def
/InlineTitles true def
/ShapesInTitles true def
```


## Spirals

Another playful decoration, a background spiral, is engaged by the Boolean `Spirals`. 

The location of the centre of the spiral is controlled by `SpiralCentreFromCentreAngle` and by `SpiralCentreFromCentreProportionRadiiInside`. 

<img align="right" width="342" height="341" src="images/Spirals.png">

The number of arms is `SpiralNumArms`, and `SpiralAngleOffset` rotates the whole pattern.

The meaning of the Boolean `SpiralClockwise` is obvious.

`SpiralRadiusBetweenArms` is the radius between arms (albeit measured to the centre rather than perpendicular to a tangent). 
If `SpiralRadiusBetweenArms` &ge;&nbsp;32767 =&nbsp;2&sup1;&#8309;&nbsp;&minus;&nbsp;1 =&nbsp;`Infinity`, then it is deemed that `SpiralRadiusBetweenArms`&nbsp;=&nbsp;&infin;&nbsp;&nbsp; &DoubleLongRightArrow;&nbsp;the spiral arms are replaced with straight lines radiating from the centre of this degenerate &lsquo;spiral&rsquo;.

`SpiralStrokeCode`, by default a boring `{stroke}`, can hold formatting of the line (e.g., `{gsave 0.6 setgray 1.44 setlinewidth stroke grestore 1 setgray 0.48 setlinewidth stroke}`). 

Extracts of code that made the image:
```PostScript
/InlineTitles false def
/Spirals true def
/SpiralNumArms 5 def
/SpiralCentreFromCentreProportionRadiiInside 0.618 def
```

Spirals are mentioned in [issue&nbsp;17](http://github.com/jdaw1/placemat/issues/17).


## OutlineTitles

<img align="right" width="476" height="478" src="images/Outline_Rotation.png">

This decorative possibility, shown in the [QvA08](http://www.jdawiseman.com/papers/port_and_wine/quevedo_2008.html) image, has existed since early versions of this code. 
But I now see it as too cluttered so am less fond of it than when it first appeared: &#655;&#7437;&#7437;&#7456;.

It is engaged with the Boolean `OutlineTitles`. 
If that is, then also heeded are `OutlineTitlesAlsoAbovetitles`, `OutlineTitlesAlsoBelowtitles`, and `OutlineTitlesAlsoOvertitles`.

The innermost white is of width `OutlineTitlesInnerWidthWhite`, and the innermost black of width `OutlineTitlesInnerWidthBlack`. 
These grow in successive outlines by factors of `OutlineTitlesMultiplierWhite` (defaulting to &frac12;(1&nbsp;+&nbsp;&radic;5) =&nbsp;the golden ratio &asymp;&nbsp;1.618) and `OutlineTitlesMultiplierBlack` (defaulting to 1, so all the black outlines have the same width). 

The number of black ripples is capped at `OutlineTitlesMaxNum`. 
The code attempts to stop sooner, but a good user constraint can only help, especialy if either multiplier is &lt;1. 

OutlineTitles does not impose as high a burden on a printer as does FillTexts, but can still be difficult for some. Again, test your printer.

Analagous to the cross hatching parameters are `NeckTagsShowOutlineTitles` and `DecanterLabelsShowOutlineTitles`. 

Extracts of code that made the image:
```PostScript
/ColourSchemeTitles /MidGrey def
/RotationTitlesAboveBelowOverCirclearray 30 def
/InlineTitles false def
/OutlineTitles true def
```

The outlining code would be improved by the routine requested in [issue&nbsp;18](http://github.com/jdaw1/placemat/issues/18).

## Rotation

The numeric parameter `RotationTitlesAboveBelowOverCirclearray` rotates the whole circle by that many degrees, in the QvA08  example by `30`. 


## InlineTitles

This decoration is engaged by default, the relevant Booleans being `InlineTitles`, `InlineAbovetitles`, `InlineBelowtitles`, `InlineOvertitles`, and `InlinePlaceNames`. 

How many steps in should it go? 
This is capped at `InlineTitlesMaxNumberContours`, `InlineAbovetitlesMaxNumberContours`, `InlineBelowtitlesMaxNumberContours`, and `InlineOvertitlesMaxNumberContours`. 
(InlinePlaceNames uses the sub-parameters of InlineTitles.)
By default his cap is an elegantly sparse `1`, though `2` can also be elegant.

In the Titles the lines have widths of `InlineTitlesBlackWidth` and `InlineTitlesWhiteWidth`; with obvious variations `InlineAbovetitlesBlackWidth`, `InlineAbovetitlesWhiteWidth`, `InlineBelowtitlesBlackWidth`, `InlineBelowtitlesWhiteWidth`, `InlineOvertitlesBlackWidth` and `InlineOvertitlesWhiteWidth`. 
If the colour scheme is /MidGrey then &ldquo;black&rdquo; means the darker of the two shades, and &ldquo;white&rdquo; the lighter.

If the capped number of contours is large, then it becomes relevant that the code can attempt an estimate of how many contours are needed. 
It does so if `InlineTitlesAttemptMinimiseNumContours` (or `InlineAboveBelowOverAttemptMinimiseNumContours` or `InlinePlaceNamesAttemptMinimiseNumContours`) is `true`. 
If the code&rsquo;s estimate is too low, as might happen if the lines are very thin, then the booleans should be false and the upper bounds set carefully. The attempted estimate is computed using a horrible algorithm, &lsquo;discussed&rsquo; at [comp.lang.postscript](http://groups.google.com/g/comp.lang.postscript/c/86b7Sg8v7B0). 

`InlineStrokePreformatting` is, likely as not, to be either `0 setlinejoin` or `1 setlinejoin`, but could hold other formattings.

If `InlineTitlesPrefillWhite` / `InlineAbovetitlesPrefillWhite` / `InlineBelowtitlesPrefillWhite` / `InlineOvertitlesPrefillWhite`, then the `Titles` / `Abovetitles` / `Belowtitles` / `Overtitles` are filled white before painting the &lsquo;Inlines&rsquo;, so are opaque. 
This is good if there is CrossHatchingInside, but less good with BackgroundTextsGlasses. 
Again, the routine requested in [issue&nbsp;18](http://github.com/jdaw1/placemat/issues/18) would be a blessing.


## FillTexts

The `FillTexts`, shown in the top image, were enabled by
```PostScript
/FillTitles true def
```
The example shown also has `/FillTextAngle -30 def`, but this does not have to be numeric. 
It also accepts some name values: `/LowerLeft`, `/LowerRight`, `/MiddleLeft`, `/UpperCenter`, `/UpperRight`, or `/Name`, the text being perpendicular to a line from from the value of  `FillTextAngle` to the centre of the circle. 
Using one of these values, my favourite pehaps being `/Name`, causes each circle to have a different angle, but the pattern as a whole coheres aesthetically. 

The Booleans `FillTitles`, `FillAbovetitles`, `FillBelowtitles`, `FillOvertitles`, and `FillPlaceNames` control whether their respective elements are filled with multiple copies of some text, outlined. 
The filling texts are in the array `FillTexts`, which is of the same length as `Titles`, and each is outlined `FillTextNumOutlines` times. 
Depending on the values of `ColourSchemeTitles` etc, the colours are either black and white, or 40% grey and white. 
Each rendering of an item of `FillTexts` is suffixed with `FillTextNumSpaces` spaces.

The `FillTexts` are set in the font `FillTextFont`, at a size of at least `FillTextMinFontSizeAbsolute`, and of a size of at least `FillTextMinFontSizeProportionLargestTitleAboveBelowOver` &times; the largest their font sizes.

The formatting of the `PlaceNames` generally matches that of the Titles, except that the filling text is `FillTextPlaceNames`, and the angle is `FillTextAnglePlaceNames`

### Problems with FillTexts

`FillTexts` makes complicated painting paths inside complicated clipping paths. 
This can cause difficulties for some software; this can cause difficulties for some printers.

Use of `FillTexts` makes distillation slow, and produces files that can be too complicated for some printers. 
But being maximally fussy can cause distillation to be very slow in Adobe Distiller, and even slower in &le;&thinsp;2017 versions of GhostScript ([bug&nbsp;report](https://bugs.ghostscript.com/show_bug.cgi?id=695906)). 

The balance between these can be influenced by the parameter `FillTextPedantry`, which can take one of three values.  
* `/Quick`, causing the judgement about whether to paint the FillText to be done purely on the bounding boxes of the two paths. So more FillTexts are painted than necessary, sometimes many more, slowing the printer.  
* `/Sensible`, causing the judgement to be done by the PostScript function `infill`. Generally this is good. But if the edging of the FillText would be inside, and would be inside by so much that it wouldn&rsquo;t be covered by something like `InlineTitlesBlackWidth`, then that small edging would be omitted. Choosing `/Sensible` seems to give optimal output, for only slightly slow distillation: hence its name.  
* `/Fussy` tests using `instroke`, which is much slower to distill, but pedantically correct.

For example, in a draft placemat with `FillTitles`, changing `FillTextPrintQuickerDistillSlower` from `/Quick` to `/Sensible` to `/Fussy` decreased the file size 399k to 368k to 383k, but increased the distill time from 25 seconds to 47 seconds to 198 seconds. 
And it might be that some printers are easily overwhelmed, so `/Quick` won&rsquo;t print at all. 
But some printers can&rsquo;t cope with either; or the resolution is insufficient for the small grey text to look entirely satisfactory. 
So test your printer; do not assume that anything will work first time; and do not assume that all larger more expensive printers cope better.

It also appears that some versions of Adobe Distiller do not always distill or render perfectly these `FillTexts`. This problem can be fixed by opening the PostScript file with Preview on the Mac OS X, and then printing from Preview or saving the PDF file Preview makes and subsequently printing from Acrobat ([technical demonstration of error](http://groups.google.com/group/comp.lang.postscript/browse_frm/thread/d939df0dde60335c)).

But there is also a problem with Preview on the Mac OS X, which crashes if the paths are too complicated. 
The relevant constraint is on the complexity of the path of the item of FillTexts, plus the complexity of the path of the text that is filled (the item of `Titles` or of `Names`, as appropriate). 
As `Names` are typically longer than `Titles`, the problem can typically be remedied by setting `FillPlaceNames` to `false`.


## GlassesCirclesFadingFactor and GlassesCrossedOut

A few wines are not being drunk by a few people. 
Perhaps they don&rsquo;t like wine of that type; perhaps allergic; perhaps something else. 
It helps with set-up if these exclusions are plainly marked. 
This can be done by fading those circles for those people, or by crossing them out, or both. 

Hence the rarely used `GlassesCrossedOut`, a Boolean; and `GlassesCirclesFadingFactor`, a number &ge;0 and &le;1, in which 0 means entirely faded away and 1 is the black-is-black default. 
The selection of &ldquo;those circles for those people&rdquo; is done with code, most likely by accessing the internal variables `NameNum` and `WithinTitles`. 
E.g.:

```PostScript
/GlassesCirclesFadingFactor
{
	Names NameNum get (Julian)   eq  WithinTitles 0 eq  and 
	Names NameNum get (MaryAnne) eq  WithinTitles 1 eq  and  or
		{0.125}  % Mostly faded away
		{1}      % The black-is-black default
	ifelse
} def  % /GlassesCirclesFadingFactor
```

## GlassesPageWhiteCirclesBehind and CirclearraysFillBehind

Sometimes part of the output is converted to a bitmap, for inclusion in a web page or a phpBB post. 
If the bitmap is to have transparency, it might be that a white background is wanted behind each of the circles. 
The Boolean `GlassesPageWhiteCirclesBehind` does what it says.

There can also be paint behind the Circlearrays, activated by the Boolean `CirclearraysFillBehind`. 
The painting is done with `CirclearraysFillBehindCode`.

## GlassesAnnotations

Placemats have been made and printed and used. 
During the tasting, an error is noticed. 
Ouch! 
There are two obvious *desiderata*. 
As the printed PDF is part of the record of the evening, it should not be changed. 
But also it would be unhelpful to allow the errors to confuse future generations. 
(But see [discussion](http://www.theportforum.com/viewtopic.php?p=90575#p90575) and [more discussion](http://www.theportforum.com/viewtopic.php?p=92316#p92316).) 
E.g., the author has attended [a&nbsp;tasting](http://www.theportforum.com/viewtopic.php?t=11196) at which the cork of a purported Smith Woodhouse 1963 showed the vintage to be 196**6**.

A non-printable annotation can be added to the PDF. 
`GlassesAnnotations` is an array of even length, alternating `WithinTitles`-style integers pointing into the arrays such as `Titles`, and compound-string annotations.
Be helpful to future historians: each anotation&rsquo;s text should include the date that the correction was added.
