# Compound Strings and non-ASCII characters

**Documents**: 
1.  [Introduction, and a first placemat](introduction_first_placemat.md);  
2.  *Compound Strings and non-ASCII characters*;  
3.  [Fonts and glass decoration](fonts_glasses_decoration.md);  
4.  [Type sizes](type_sizes.md);  
5.  [Page-level controls](page_level.md);  
6.  [Arrangement of glasses on the page](PackingStyles.md);  
7.  [Non-Glasses Pages](not_glasses.md);  
8.  [Document-level controls](document.md);  
9.  [Code injection](code_injection.md);  
10. [Bitmap images](bitmap_images.md).

----

Some wanted text is more complicated than a plain [ASCII](http://en.wikipedia.org/wiki/ASCII) string. 
[PostScript](http://en.wikipedia.org/wiki/PostScript) is an early-1980s language, and one of the ways in which it shows its age is its incompatibility with Unicode. 
This document shows how to access non-ASCII characters, and the more general concept of a compound string.


## Strings, and compound strings

The basic unit of Postscript text is the string, which are delimited with round brackets.
```PostScript
(This is an unexciting PostScript string.)
```  
Strings can contain ASCII characters, of which there are almost a hundred. 

Other characters can be accessed by their name. 
E.g., `/acircumflex` is &ldquo;&acirc;&rdquo;; 
`/dagger` is &ldquo;&dagger;&ldquo;; 
`/sterling` is &ldquo;&pound;&ldquo;; and
`/fi` is the ligature &ldquo;&#64257;&ldquo;, a single character which joins the &lsquo;f&rsquo; and &lsquo;i&rsquo; without an ugly collision between the tail of the former and the dot of the latter. 

These concepts have been unified and extended by the placemat software into a &lsquo;compound string&rsquo;. 
A compound string is any of:
* A string;
* A glyph name;
* Code, which can either change the graphics state, or leave compound strings on the stack;
* An array, so bounded by square brackets = `[]`, containing other compound strings.

Some examples:

<div align="center">

| Compound string | Rendered as |
|:----------------|:------------|
| `/dagger`       | &dagger;    |
| `[/daggerdbl]`  | &Dagger;    |
| `/sterling`     | &pound;     |
| `/dollar`       | $           |
| `($)`           | $           |
| `[ [/yen] ]`    | &yen;       |
| `[(Quinta do Bom) /fi (m)]` | Quinta do Bom&#64257;m |
| `[(Ch) /acircumflex (teau L) /eacute (oville-Barton)]` | Ch&acirc;teau L&eacute;oville-Barton |
| `(JDAW)`                   | ![&lsquo;JDAW&rsquo;, not kerned](images/JDAW_unkerned.png) |
| `[(JDA) {-0.06 Kern} (W)]` | ![&lsquo;JDAW&rsquo;, kerned](images/JDAW_kerned.png) |

</div>

These examples are not entirely idle. 
Five glasses fit very elegantly on one sheet of A4. 
So if there are four wines, a spare circle is labelled &dagger;. 
If there are eight glasses on 2&times;A4, the spares are &dagger; &Dagger;. 
Seven glasses on 2&times;A4 have three spares, usually &pound; $ &yen;.

The last two rows of the table show the effect of `Kern`ing, code being in curly brackets `{}`, the number being the horizontal movement as a proportion of the font size (font = `/DejaVuSerif`). 

Some fonts have thousands of glyphs. 
Other fonts have fewer &mdash; not every glyph is present in every font. 
Check your output!

There follow a selection of the glyphs most likely to be useful to users of the placemat software.

## Glyph names

**Punctuation**:&nbsp;&nbsp;&nbsp;&nbsp; 
&lsquo;&nbsp;`/quoteleft`&nbsp;&nbsp;&nbsp;&nbsp; 
&rsquo;&nbsp;`/quoteright`&nbsp;&nbsp;&nbsp;&nbsp; 
&ldquo;&nbsp;`/quotedblleft`&nbsp;&nbsp;&nbsp;&nbsp; 
&rdquo;&nbsp;`/quotedblright`&nbsp;&nbsp;&nbsp;&nbsp; 
&hellip;&nbsp;`/ellipsis`&nbsp;&nbsp;&nbsp;&nbsp; 
&ndash;&nbsp;`/endash`&nbsp;&nbsp;&nbsp;&nbsp; 
&mdash;&nbsp;`/emdash`&nbsp;&nbsp;&nbsp;&nbsp; 
&lsaquo;&nbsp;`/guilsinglleft`&nbsp;&nbsp;&nbsp;&nbsp; 
&rsaquo;&nbsp;`/guilsinglright`&nbsp;&nbsp;&nbsp;&nbsp; 
&sbquo;&nbsp;`/quotesinglbase`&nbsp;&nbsp;&nbsp;&nbsp; 
&bdquo;&nbsp;`/quotedblbase`

**Ligatures and letters**:&nbsp;&nbsp;&nbsp;&nbsp; 
&#64257;&nbsp;`/fi`&nbsp;&nbsp;&nbsp;&nbsp; 
&#64258;&nbsp;`/fl`&nbsp;&nbsp;&nbsp;&nbsp; 
&aelig;&nbsp;`/ae`&nbsp;&nbsp;&nbsp;&nbsp; 
&AElig;&nbsp;`/AE`&nbsp;&nbsp;&nbsp;&nbsp; 
&oelig;&nbsp;`/oe`&nbsp;&nbsp;&nbsp;&nbsp; 
&OElig;&nbsp;`/OE`&nbsp;&nbsp;&nbsp;&nbsp; 
&szlig;&nbsp;`/germandbls`&nbsp;&nbsp;&nbsp;&nbsp; 

**Symbols**:&nbsp;&nbsp;&nbsp;&nbsp; 
&dagger;&nbsp;`/dagger`&nbsp;&nbsp;&nbsp;&nbsp; 
&Dagger;&nbsp;`/daggerdbl`&nbsp;&nbsp;&nbsp;&nbsp; 
&loz;&nbsp;`/lozenge`&nbsp;&nbsp;&nbsp;&nbsp; 
&bull;&nbsp;`/bullet`&nbsp;&nbsp;&nbsp;&nbsp; 
&middot;&nbsp;`/periodcentered`&nbsp;&nbsp;&nbsp;&nbsp; 
&sect;&nbsp;`/section`&nbsp;&nbsp;&nbsp;&nbsp; 
&copy;&nbsp;`/copyright`&nbsp;&nbsp;&nbsp;&nbsp; 
&reg;&nbsp;`/registered`&nbsp;&nbsp;&nbsp;&nbsp; 
&trade;&nbsp;`/trademark`&nbsp;&nbsp;&nbsp;&nbsp; 
&spades;&nbsp;`/spade`&nbsp;&nbsp;&nbsp;&nbsp; 
&hearts;&nbsp;`/heart`&nbsp;&nbsp;&nbsp;&nbsp; 
&diams;&nbsp;`/diamond`&nbsp;&nbsp;&nbsp;&nbsp; 
&clubs;&nbsp;`/club`

**Currencies, fractions, maths**:&nbsp;&nbsp;&nbsp;&nbsp; 
&pound;&nbsp;`/sterling`&nbsp;&nbsp;&nbsp;&nbsp; 
&euro;&nbsp;`/Euro`&nbsp;&nbsp;&nbsp;&nbsp; 
&yen;&nbsp;`/yen`&nbsp;&nbsp;&nbsp;&nbsp; 
&#8361;&nbsp;`/won`&nbsp;&nbsp;&nbsp;&nbsp; 
&cent;&nbsp;`/cent`&nbsp;&nbsp;&nbsp;&nbsp; 
&frac12;&nbsp;`/onehalf`&nbsp;&nbsp;&nbsp;&nbsp; 
&frac14;&nbsp;`/onequarter`&nbsp;&nbsp;&nbsp;&nbsp; 
&frac34;&nbsp;`/threequarters`&nbsp;&nbsp;&nbsp;&nbsp; 
&#8539;&nbsp;`/oneeighth`&nbsp;&nbsp;&nbsp;&nbsp; 
&#8540;&nbsp;`/threeeighths`&nbsp;&nbsp;&nbsp;&nbsp; 
&#8532;&nbsp;`/twothirds`&nbsp;&nbsp;&nbsp;&nbsp; 
&asymp;&nbsp;`/approxequal`&nbsp;&nbsp;&nbsp;&nbsp; 
&ge;&nbsp;`/greaterequal`&nbsp;&nbsp;&nbsp;&nbsp; 
&le;&nbsp;`/lessequal`&nbsp;&nbsp;&nbsp;&nbsp; 
&times;&nbsp;`/multiply`&nbsp;&nbsp;&nbsp;&nbsp; 
&divide;&nbsp;`/divide`

**Greeks**:&nbsp;&nbsp;&nbsp;&nbsp; 
&alpha;&nbsp;`/alpha`&nbsp;&nbsp;&nbsp;&nbsp; 
&beta;&nbsp;`/beta`&nbsp;&nbsp;&nbsp;&nbsp; 
&gamma;&nbsp;`/gamma`&nbsp;&nbsp;&nbsp;&nbsp; 
&delta;&nbsp;`/delta`&nbsp;&nbsp;&nbsp;&nbsp; 
&epsilon;&nbsp;`/epsilon`&nbsp;&nbsp;&nbsp;&nbsp; 
&zeta;&nbsp;`/zeta`&nbsp;&nbsp;&nbsp;&nbsp; 
&eta;&nbsp;`/eta`&nbsp;&nbsp;&nbsp;&nbsp; 
&theta;&nbsp;`/theta`&nbsp;&nbsp;&nbsp;&nbsp; 
&iota;&nbsp;`/iota`&nbsp;&nbsp;&nbsp;&nbsp; 
&kappa;&nbsp;`/kappa`&nbsp;&nbsp;&nbsp;&nbsp; 
&lambda;&nbsp;`/lambda`&nbsp;&nbsp;&nbsp;&nbsp; 
&mu;&nbsp;`/mu`&nbsp;&nbsp;&nbsp;&nbsp; 
&nu;&nbsp;`/nu`&nbsp;&nbsp;&nbsp;&nbsp; 
&xi;&nbsp;`/xi`&nbsp;&nbsp;&nbsp;&nbsp; 
&omicron;&nbsp;`/omicron`&nbsp;&nbsp;&nbsp;&nbsp; 
&pi;&nbsp;`/pi`&nbsp;&nbsp;&nbsp;&nbsp; 
&rho;&nbsp;`/rho`&nbsp;&nbsp;&nbsp;&nbsp; 
&sigma;&nbsp;`/sigma`&nbsp;&nbsp;&nbsp;&nbsp; 
&tau;&nbsp;`/tau`&nbsp;&nbsp;&nbsp;&nbsp; 
&upsilon;&nbsp;`/upsilon`&nbsp;&nbsp;&nbsp;&nbsp; 
&phi;&nbsp;`/phi`&nbsp;&nbsp;&nbsp;&nbsp; 
&chi;&nbsp;`/chi`&nbsp;&nbsp;&nbsp;&nbsp; 
&psi;&nbsp;`/psi`&nbsp;&nbsp;&nbsp;&nbsp; 
&omega;&nbsp;`/omega`&nbsp;&nbsp;&nbsp;&nbsp; 
&Alpha;&nbsp;`/Alpha`&nbsp;&nbsp;&nbsp;&nbsp; 
etc

**Arrows**:&nbsp;&nbsp;&nbsp;&nbsp; 
&rarr;&nbsp;`/arrowright`&nbsp;&nbsp;&nbsp;&nbsp; 
&larr;&nbsp;`/arrowleft`&nbsp;&nbsp;&nbsp;&nbsp; 
&uarr;&nbsp;`/arrowup`&nbsp;&nbsp;&nbsp;&nbsp; 
&darr;&nbsp;`/arrowdown`&nbsp;&nbsp;&nbsp;&nbsp; 
&harr;&nbsp;`/arrowboth`&nbsp;&nbsp;&nbsp;&nbsp; 
&rArr;&nbsp;`/arrowdblright`&nbsp;&nbsp;&nbsp;&nbsp; 
&lArr;&nbsp;`/arrowdblleft`&nbsp;&nbsp;&nbsp;&nbsp; 
&uArr;&nbsp;`/arrowdblup`&nbsp;&nbsp;&nbsp;&nbsp; 
&dArr;&nbsp;`/arrowdbldown`&nbsp;&nbsp;&nbsp;&nbsp; 
&hArr;&nbsp;`/arrowdblboth`


## Accents and diacritics

Some wines, and some people, have accents in their names.

In PostScript the name of an accented character consists of a *base*, and a *diacritic*. 
The name of the glyph is the former followed by the latter. 
For example, `/atilde` is &ldquo;&atilde;&rdquo;, and `/Atilde` is &ldquo;&Atilde;&rdquo;. 
Observe the case sensitivity.

The table shows the names of the diacritics, and with which base characters which of these are available in the font `/TimesNewRomanPS-BoldMT`.

|                      | `a` | `A` | `e` | `E` | `i` | `I` | `o` | `O` | `u` | `U` | `y` | `Y` | `c` | `C` | `g` | `G` | `h` | `H` | `l` | `L` | `n` | `N` | `r` | `R` | `s` | `S` | `t` | `T` | `w` | `W` | `z` | `Z` |
|:---------------------|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| `acute` | &aacute; | &Aacute; | &eacute; | &Eacute; | &iacute; | &Iacute; | &oacute; | &Oacute; | &uacute; | &Uacute; | &yacute; | &Yacute; | &#263; | &#262; |  |  |  |  | &#314; | &#313; | &#324; | &#323; | &#341; | &#340; | &#347; | &#346; |  |  | &#7811; | &#7810; | &#378; | &#377; |
| `circumflex` | &acirc; | &Acirc; | &ecirc; | &Ecirc; | &icirc; | &Icirc; | &ocirc; | &Ocirc; | &ucirc; | &Ucirc; | &#375; | &#374; | &#265; | &#264; | &#285; | &#284; | &#293; | &#292; |  |  |  |  |  |  | &#349; | &#348; |  |  | &#373; | &#372; |  |  |
| `grave` | &agrave; | &Agrave; | &egrave; | &Egrave; | &igrave; | &Igrave; | &ograve; | &Ograve; | &ugrave; | &Ugrave; | &#7923; | &#7922; |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  | &#7809; | &#7808; |  |  |
| `dieresis` | &auml; | &Auml; | &euml; | &Euml; | &iuml; | &Iuml; | &ouml; | &Ouml; | &uuml; | &Uuml; | &yuml; | &Yuml; |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  | &#7813; | &#7812; |  |  |
| `tilde` | &atilde; | &Atilde; |  |  | &#297; | &#296; | &otilde; | &Otilde; | &#361; | &#360; |  |  |  |  |  |  |  |  |  |  | &ntilde; | &Ntilde; |  |  |  |  |  |  |  |  |  |  |
| `breve` | &#259; | &#258; | &#277; | &#276; | &#301; | &#300; | &#335; | &#334; | &#365; | &#364; |  |  |  |  | &#287; | &#286; |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| `macron` | &#257; | &#256; | &#275; | &#274; | &#299; | &#298; | &#333; | &#332; | &#363; | &#362; |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| `ogonek` | &#261; | &#260; | &#281; | &#280; | &#303; | &#302; |  |  | &#371; | &#370; |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| `caron` |  |  | &#283; | &#282; |  |  |  |  |  |  |  |  | &#269; | &#268; | &#487; | &#486; |  |  | &#318; | &#317; | &#328; | &#327; | &#345; | &#344; | &scaron; | &Scaron; | &#357; | &#356; |  |  | &#382; | &#381; |
| `cedilla` |  |  |  |  |  |  |  |  |  |  |  |  | &ccedil; | &Ccedil; | &#291; | &#290; |  |  | &#316; | &#315; | &#326; | &#325; | &#343; | &#342; | &#351; | &#350; |  |  |  |  |  |  |
| `dot` |  |  | &#279; | &#278; |  | &#304; |  |  |  |  |  |  |  |  |  |  |  |  | &#320; | &#319; |  |  |  |  |  |  |  |  |  |  |  |  |
| `dotaccent` |  |  |  |  |  |  |  |  |  |  |  |  | &#267; | &#266; | &#289; | &#288; |  |  |  |  |  |  |  |  |  |  |  |  |  |  | &#380; | &#379; |
| `hungarumlaut` |  |  |  |  |  |  | &#337; | &#336; | &#369; | &#368; |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| `slash` |  |  |  |  |  |  | &oslash; | &Oslash; |  |  |  |  |  |  |  |  |  |  | &#322; | &#321; |  |  |  |  |  |  |  |  |  |  |  |  |
| `ring` | &aring; | &Aring; |  |  |  |  |  |  | &#367; | &#366; |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| `bar` |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  | &#295; | &#294; |  |  |  |  |  |  |  |  | &#359; | &#358; |  |  |  |  |
| `commaaccent` |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  | &#351; | &#350; | &#355; | &#354; |  |  |  |  |


**More accents and diacritics**:&nbsp;&nbsp;&nbsp;&nbsp; 
&#509;&nbsp;`/aeacute`&nbsp;&nbsp;&nbsp;&nbsp; 
&#508;&nbsp;`/AEacute`&nbsp;&nbsp;&nbsp;&nbsp; 
&#507;&nbsp;`/aringacute`&nbsp;&nbsp;&nbsp;&nbsp; 
&#506;&nbsp;`/Aringacute`&nbsp;&nbsp;&nbsp;&nbsp; 
&#271;&nbsp;`/dcaron`&nbsp;&nbsp;&nbsp;&nbsp; 
&#270;&nbsp;`/Dcaron`&nbsp;&nbsp;&nbsp;&nbsp; 
&#273;&nbsp;`/dcroat`&nbsp;&nbsp;&nbsp;&nbsp; 
&#272;&nbsp;`/Dcroat`&nbsp;&nbsp;&nbsp;&nbsp; 
&#309;&nbsp;`/jcircumflex`&nbsp;&nbsp;&nbsp;&nbsp; 
&#308;&nbsp;`/Jcircumflex`&nbsp;&nbsp;&nbsp;&nbsp; 
&#311;&nbsp;`/kcedilla`&nbsp;&nbsp;&nbsp;&nbsp; 
&#310;&nbsp;`/Kcedilla`&nbsp;&nbsp;&nbsp;&nbsp; 
&#312;&nbsp;`/kgreenlandic`&nbsp;&nbsp;&nbsp;&nbsp; 
&#329;&nbsp;`/napostrophe`

**More extended Latin**:&nbsp;&nbsp;&nbsp;&nbsp; 
&#305;&nbsp;`/dotlessi`&nbsp;&nbsp;&nbsp;&nbsp; 
&thorn;&nbsp;`/thorn`&nbsp;&nbsp;&nbsp;&nbsp; 
&THORN;&nbsp;`/Thorn`&nbsp;&nbsp;&nbsp;&nbsp; 
&eth;&nbsp;`/eth`&nbsp;&nbsp;&nbsp;&nbsp; 
&ETH;&nbsp;`/Eth`&nbsp;&nbsp;&nbsp;&nbsp; 
&#331;&nbsp;`/eng`&nbsp;&nbsp;&nbsp;&nbsp; 
&#330;&nbsp;`/Eng`
