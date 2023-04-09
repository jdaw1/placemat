# Compound Strings and non-ASCII characters

**Link to the main program**: [placemat.ps](../PostScript/placemat.ps?raw=1). And link to the [stand-alone PostScript program](../PostScript/glyph_log.ps) which logs all the glyphs from the font specified in its line&nbsp;15.

**Links to documentation**: 
&#9654;&#xFE0E;&nbsp;[Introduction,&nbsp;and&nbsp;a&nbsp;first&nbsp;placemat](introduction_first_placemat.md#readme)&nbsp; 
&#9654;&#xFE0E;&nbsp;[Fonts&nbsp;and&nbsp;glass&nbsp;decoration](fonts_glasses_decoration.md#readme)&nbsp; 
&#9655;&#xFE0E;&nbsp;*Compound&nbsp;Strings&nbsp;and&nbsp;non&#8209;ASCII&nbsp;characters*&nbsp; 
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

Some wanted text is more complicated than a plain [ASCII](http://en.wikipedia.org/wiki/ASCII) string. 
[PostScript](http://en.wikipedia.org/wiki/PostScript) is an early-1980s language, and one of the ways in which it shows its age is its incompatibility with Unicode. 
This document shows how to access non-ASCII characters, and the more general concept of a compound string.


## Strings, and compound strings

The basic unit of Postscript text is the string, which are delimited with round brackets.
```PostScript
(This is an unexciting PostScript string.)
```  

Strings can contain any of the ninety-five printable ASCII characters, so those numbered 32&ndash;126.

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

| Compound string                                               | Rendered as                              |
|:--------------------------------------------------------------|:-----------------------------------------|
| `/dagger`                                                     | &dagger;                                 |
| `[/daggerdbl]`                                                | &Dagger;                                 |
| `/sterling`                                                   | &pound;                                  |
| `/dollar`                                                     | $                                        |
| `($)`                                                         | $                                        |
| `[ [/yen] ]`                                                  | &yen;                                    |
| `[(C) /aacute (lem)]`                                         | C&aacute;lem                             |
| `[(Roz) /egrave (s)]`                                         | Roz&egrave;s                             | 
| `[(Po) /ccedilla (as)]`                                       | Po&ccedil;as                             |
| `[(Quinta do Bom) /fi (m)]`                                   | Quinta do Bom&#64257;m                   |
| `[(Croft Quinta da Ro) /ecircumflex (da S) /emacron (rikos)]` | Croft Quinta da Ro&ecirc;da S&#275;rikos |
| `[(Tinta C) /atilde (o)]`                                     | Tinta C&atilde;o                         |
| `[(Ch) /acircumflex (teau L) /eacute (oville-Barton)]`        | Ch&acirc;teau L&eacute;oville-Barton     |
| `[(Mo) /edieresis (t & Chandon)]`                             | Mo&euml;t & Chandon                      |
| `(JDAW)`                                                      | ![&lsquo;JDAW&rsquo;, not kerned](images/JDAW_unkerned.png) |
| `[(JDA) {-0.06 Kern} (W)]`                                    | ![&lsquo;JDAW&rsquo;, kerned](images/JDAW_kerned.png) |

</div>

These examples are not entirely idle. 
Five glasses fit very elegantly on one sheet of A4. 
So if there are four wines, a spare circle is labelled &dagger;. 
If there are eight glasses on 2&times;A4, the spares are &dagger; &Dagger;. 
Seven glasses on 2&times;A4 have three spares, usually &pound; $ &yen;.

The last two rows of the table show the effect of `Kern`ing, code being in curly brackets `{}`, the number being the horizontal movement as a proportion of the font size (font = `/DejaVuSerif`). 

Some fonts have thousands of glyphs. 
Other fonts have fewer: not every glyph is present in every font. 
E.g.,&nbsp;`/emacron`&nbsp;=&nbsp;&#275; is present in the fonts of the `/TrebuchetMS` family, but not in (my computer&rsquo;s version of) the `/Garamond` family, nor in many other fonts. 
Indeed, `/emacron` is missing from so many fonts that the text on [Croft&rsquo;s website](https://croftport.com/en/products/serikos-vintage/2017/) doesn&rsquo;t use it consistently, even though the &ldquo;&#275;&rdquo; appears on the labels of S&#275;rikos bottles. 
If a glyph is missing from a font then there should be a warning on the log page, but, anyway, check your output.

There follow a selection of other glyphs that might be useful to users of the placemat software.

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
&dagger;&#xFE0E;&nbsp;`/dagger`&nbsp;&nbsp;&nbsp;&nbsp; 
&Dagger;&#xFE0E;&nbsp;`/daggerdbl`&nbsp;&nbsp;&nbsp;&nbsp; 
&loz;&#xFE0E;&nbsp;`/lozenge`&nbsp;&nbsp;&nbsp;&nbsp; 
&bull;&#xFE0E;&nbsp;`/bullet`&nbsp;&nbsp;&nbsp;&nbsp; 
&middot;&#xFE0E;&nbsp;`/periodcentered`&nbsp;&nbsp;&nbsp;&nbsp; 
&sect;&#xFE0E;&nbsp;`/section`&nbsp;&nbsp;&nbsp;&nbsp; 
&copy;&#xFE0E;&nbsp;`/copyright`&nbsp;&nbsp;&nbsp;&nbsp; 
&reg;&#xFE0E;&nbsp;`/registered`&nbsp;&nbsp;&nbsp;&nbsp; 
&trade;&#xFE0E;&nbsp;`/trademark`&nbsp;&nbsp;&nbsp;&nbsp; 
&spades;&#xFE0E;&nbsp;`/spade`&nbsp;&nbsp;&nbsp;&nbsp; 
&hearts;&#xFE0E;&nbsp;`/heart`&nbsp;&nbsp;&nbsp;&nbsp; 
&diams;&#xFE0E;&nbsp;`/diamond`&nbsp;&nbsp;&nbsp;&nbsp; 
&clubs;&#xFE0E;&nbsp;`/club`

**Currencies, fractions, maths**:&nbsp;&nbsp;&nbsp;&nbsp; 
&pound;&#xFE0E;&nbsp;`/sterling`&nbsp;&nbsp;&nbsp;&nbsp; 
&euro;&#xFE0E;&nbsp;`/Euro`&nbsp;&nbsp;&nbsp;&nbsp; 
&yen;&#xFE0E;&nbsp;`/yen`&nbsp;&nbsp;&nbsp;&nbsp; 
&#8361;&#xFE0E;&nbsp;`/won`&nbsp;&nbsp;&nbsp;&nbsp; 
&cent;&#xFE0E;&nbsp;`/cent`&nbsp;&nbsp;&nbsp;&nbsp; 
&frac12;&#xFE0E;&nbsp;`/onehalf`&nbsp;&nbsp;&nbsp;&nbsp; 
&frac14;&#xFE0E;&nbsp;`/onequarter`&nbsp;&nbsp;&nbsp;&nbsp; 
&frac34;&#xFE0E;&nbsp;`/threequarters`&nbsp;&nbsp;&nbsp;&nbsp; 
&#8539;&#xFE0E;&nbsp;`/oneeighth`&nbsp;&nbsp;&nbsp;&nbsp; 
&#8540;&#xFE0E;&nbsp;`/threeeighths`&nbsp;&nbsp;&nbsp;&nbsp; 
&#8532;&#xFE0E;&nbsp;`/twothirds`&nbsp;&nbsp;&nbsp;&nbsp; 
&asymp;&#xFE0E;&nbsp;`/approxequal`&nbsp;&nbsp;&nbsp;&nbsp; 
&ge;&#xFE0E;&nbsp;`/greaterequal`&nbsp;&nbsp;&nbsp;&nbsp; 
&le;&#xFE0E;&nbsp;`/lessequal`&nbsp;&nbsp;&nbsp;&nbsp; 
&times;&#xFE0E;&nbsp;`/multiply`&nbsp;&nbsp;&nbsp;&nbsp; 
&divide;&#xFE0E;&nbsp;`/divide`

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
&hellip;&nbsp;&nbsp;&nbsp;&nbsp; 
&Omega;&nbsp;`/Omega`

**Arrows**:&nbsp;&nbsp;&nbsp;&nbsp; 
&rarr;&#xFE0E;&nbsp;`/arrowright`&nbsp;&nbsp;&nbsp;&nbsp; 
&larr;&#xFE0E;&nbsp;`/arrowleft`&nbsp;&nbsp;&nbsp;&nbsp; 
&uarr;&#xFE0E;&nbsp;`/arrowup`&nbsp;&nbsp;&nbsp;&nbsp; 
&darr;&#xFE0E;&nbsp;`/arrowdown`&nbsp;&nbsp;&nbsp;&nbsp; 
&harr;&#xFE0E;&nbsp;`/arrowboth`&nbsp;&nbsp;&nbsp;&nbsp; 
&rArr;&#xFE0E;&nbsp;`/arrowdblright`&nbsp;&nbsp;&nbsp;&nbsp; 
&lArr;&#xFE0E;&nbsp;`/arrowdblleft`&nbsp;&nbsp;&nbsp;&nbsp; 
&uArr;&#xFE0E;&nbsp;`/arrowdblup`&nbsp;&nbsp;&nbsp;&nbsp; 
&dArr;&#xFE0E;&nbsp;`/arrowdbldown`&nbsp;&nbsp;&nbsp;&nbsp; 
&hArr;&#xFE0E;&nbsp;`/arrowdblboth`&nbsp;&nbsp;&nbsp;&nbsp; 
&#9658;&#xFE0E;&nbsp;`/triagrt`&nbsp;&nbsp;&nbsp;&nbsp; 
&#9668;&#xFE0E;&nbsp;`/triaglf`&nbsp;&nbsp;&nbsp;&nbsp; 
&#9650;&#xFE0E;&nbsp;`/triagup`&nbsp;&nbsp;&nbsp;&nbsp; 
&#9660;&#xFE0E;&nbsp;`/triagdn`



## Accents and diacritics

Some wines, and some people, have accents in their names.

In PostScript the name of an accented character consists of a *base*, and a *diacritic*. 
The name of the glyph is the former followed by the latter. 
For example, &atilde;&nbsp;=&nbsp;`/atilde` and &Atilde;&nbsp;=&nbsp;`/Atilde`. 
Observe the case sensitivity.

The table shows the names of the diacritics, and with which base characters which of these are available in the font `/TimesNewRomanPS-BoldMT`.

<div align="center">

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

</div>

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
&#329;&nbsp;`/napostrophe`

**More extended Latin**:&nbsp;&nbsp;&nbsp;&nbsp; 
&#305;&nbsp;`/dotlessi`&nbsp;&nbsp;&nbsp;&nbsp; 
&thorn;&nbsp;`/thorn`&nbsp;&nbsp;&nbsp;&nbsp; 
&THORN;&nbsp;`/Thorn`&nbsp;&nbsp;&nbsp;&nbsp; 
&eth;&nbsp;`/eth`&nbsp;&nbsp;&nbsp;&nbsp; 
&ETH;&nbsp;`/Eth`&nbsp;&nbsp;&nbsp;&nbsp; 
&#331;&nbsp;`/eng`&nbsp;&nbsp;&nbsp;&nbsp; 
&#330;&nbsp;`/Eng`&nbsp;&nbsp;&nbsp;&nbsp; 
&#312;&nbsp;`/kgreenlandic`


## Unicode

Some fonts allow access to some characters by their unicode hexadecimal number. 
Typically four hex digits are prefixed with &ldquo;`/uni`&rdquo;; five hex digits are prefixed with &ldquo;`/u`&rdquo;. 
E.g.,&nbsp;`/uni1D00` =&nbsp;&ldquo;&#x1D00;&rdquo; =&nbsp;[small&#8209;caps&nbsp;A](http://www.fileformat.info/info/unicode/char/1d00/index.htm); 
`/u1D538` =&nbsp;&ldquo;&#x1D538;&rdquo; =&nbsp;[double&#8209;struck&nbsp;A](http://www.fileformat.info/info/unicode/char/1d538/index.htm).


## Errors

Not all fonts have all glyphs, and not all fonts allow Unicode-style naming. 
Indeed, more strongly, few fonts have most glyphs. 
So the usual advice applies: carefully check the output.

Attempts to use a non-existent glyph are logged. 
Further, as a small assist, there is a [stand-alone PostScript program](../PostScript/glyph_log.ps) which logs all the glyphs from the font specified in its line&nbsp;15, and shows them in a simple PDF.
