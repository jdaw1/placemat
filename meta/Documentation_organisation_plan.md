# Organisation of the Documentation: A Plan


The documentation was a jumble when at jdawiseman.com, and the transfer to GitHub makes it worse. 

The following is a possible organsisation, in which it is envisaged that:
- Top-level bullets are pages;
	* Second-level bullets are main sections;
		- Third-level bullets are content within those sections, perhaps paragraph-sized.

----

- Basics
	* Introduction
	* Making Your First Placemat: Advice for Beginners
	* Postscript basics
		- `(strings)`
		- `/Names`
		- `[ (arrays) (usually) (of)  (strings) ]`
		- `[/quotedblleft (Compound strings) /quotedblright]` = &ldquo;Compound strings&rdquo;
	* Essential parameters
		- `Circlearrays`
		- `Titles`
		- `Belowtitles`, `Abovetitles`, `Overtitles`
		- `Names`
		- `HeadersLeft`, `HeadersCenter`, `HeadersRight`
		- `PaperType`, `TastingNotesPaperType`
		- `ParametersVersionDateTimeAdobeFormat`
		- `ThePortForumIcon`&hellip;
	* Units: 360pt = 127mm.

- Decoration within glass circles
	* Fonts
	* `ColourScheme`&hellip;
	* `InlineTitles`
	* `OutlineTitles`
	* `CrossHatching`&hellip;
	* Stars and flowers and hearts
	* `Spirals`
	* `FillTexts` 
	* Rotation
	* `VerticalMiddling`&hellip;
	* `GlassesCirclesFadingFactor` and `GlassesCrossedOut`
	* `GlassesPageWhiteCirclesBehind`
	* `GlassesAnnotations`

- Decoration, page-level
	* `Headers`&hellip;, `Footers`&hellip;
	* `BackgroundTexts`&hellip;
	* H&#8322;O boxes;	
	* `Droplets`
	* Separating flights within a page
	* `ThePortForumIconColour`

- Layout of glasses
	* `GlassesOnSheets` and `GlassesOnTastingNotePages`
	* `PackingStyles`
	* `MaxRadius` and `ShrinkRadii`
	* Type-size constraints and `ExclusionAnnulus`&hellip;
	* `Rotate180AlternateNames`
	* `NamesShowTop`, `NamesShowBottom`, `NamesFontSizeMin`, `NamesFontSizeMax`

- Other page types
	* Separate parameterisation (`CirclearraysTastingNotes`, etc)
	* Tasting-note pages
	* Side-by-side Glasses and TastingNotes
	* Place Names
	* Pre-Pours
	* Vote Recorders
	* Decanting Notes
	* Accounts
	* Neck Tags
	* Cork Display
	* Decanter labels
	* Sticky labels
	* `EmptyGlassesPageAtStart`

- Document-level controls
	* `PDF_title`
	* `ExternalLinks`
	* `PageOrdering`&hellip;
	* `PagesToBeInserted`
	* Numbers of copies
	* Suppressing pages
	* `MirrorPages`&hellip;
	* CMYK black
	* Copyright
	* `Margin`&hellip;, `OuterGlassesMargin`&hellip;, `OuterMargin`&hellip;
	* `#`Linking to specific pages within the PDF
	* `LicensingAgreement`&hellip;
	* `OutputLogTo`&hellip;
	* `TestingSuppressPageTypes`, `TestingMaxNumPagesToShow`, `TestingShowThesePagesOnly`

- Page-size advice

- Code injection
	* Inside strings: `Kern`ing and underlining
	* Inside strings: changing font, superscripts and subscripts
	* Inside strings: Berry Bros & Rudd
	* Variables which parameters may inspect
		- `TypeOfPagesBeingRendered`
		- `PageWidth`, `PageHeight`, `MgnL`, `MgnR`, `MgnT`, `MgnB`
		- `SheetNum`
		- `WithinPage`, `WithinTitles`
		- `NameNum`, `ThisName`
		- `Radii`, `RadiiCirclearrayBaseline`, `RadiiCirclearrayInside`
		- `GlassPositions`
		- `TitleFontSizes`, `AbovetitleFontSizes`, `BelowtitleFontSizes`, `OvertitleFontSizes`
		- `CircletextMaxFontSizes`
		- `TastingSheetNum`
		- `PlaceNameSetNum`
		- `PrePourSheetNum`
		- `StickyLabelCopyNum`
		- `VoteRecorderTopTextNum`, `VoteRecorderSheetNum`
		- `DecantingNotesCopyNum`
		- `NeckTagsCopyNum`
		- Special case: if `FlightSeparationPaintSeparately` then `FlightSeparationPaintCode` may read `FlightSeparationLineNum`
	* Pre and Post: `PrologueCode`, `EpilogueCode` `PaintBackgroundCode`, `PaintForegroundCode`



- Accented characters of `/TimesNewRomanPS-BoldMT`, and their PostScript glyphs

- There was a page of &ldquo;the infrequently updated list of re-usable routines&rdquo;: does that belong here at all?

----
