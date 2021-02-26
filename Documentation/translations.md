# Translations

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
11. *Translations*.

----

## Introduction

Some of the parameters contain text in English. 
Of these, some belong to the wines or to the event and so will vary by tasting (e.g., `Circlearrays`, `HeadersLeft`, `ExternalLinks`, `CopyrightStatementPlacemats`, `BackgroundTextsGlassesTexts`). 
But others could have a more fixed translation, as suggested below.

Many languages are missing; all are incomplete; some are improvable. 
If you have the skills and enthusiasm to repair, please provide translations in [an issue](http://github.com/jdaw1/placemat/issues). 
(Obviously each `(string)` needs translating, not any of the `/ParameterName`.)

The only languages eligible for this page are those written in (extended) Latin, Greek, or Cyrillic. 
Alas, Asian languages are [too difficult in PostScript](http://groups.google.com/g/comp.lang.postscript/c/ktoR1NrLsEc/m/UjOyVOfyPKwJ).

## English

```PostScript
/VoteRecorderTopTexts [
	[ (Wine Of The Night?)  /questiondown ]
	% [ (What is it?) ]  % If uncommenting this, insert a 'true' into the VoteRecorderShowTotalRow array.
] def  % Must be same length as GlassesClusteredOnVoteRecorders, each sub-array containing some number of TopTexts
/VoteRecorderInstruction {VoteRecorderShowTotalRow VoteRecorderSheetNum GetEU {()} {(Record points, not rank.)} ifelse} bind def
/VoteRecorderTotalColTitle [(T) {-0.06 Kern} (otal)] def
/VoteRecorderTotalRowTitle [(T) {-0.09 Kern} (otal)] def
/VoteRecorderMonkeyName (Monkey) def

/TastingNotesColumnHeadings [  (Times)  (Eye)  (Nose)  (Mouth)  (Score)  ] def
/TastingNotesPageNumCompoundString [(Page ) {TastingSheetNum 1 add 5 string cvs}] def

/DecantingNotesTopText (Decanting Notes) def
/DecantingNotesColumnHeadingTimes (Decant Time) def
/DecantingNotesColumnHeadingNotes (Cork condition, branding, etc) def

/AccountsTopText (The Accounts) def
/AccountsColumnGroupHeadings [
	[/emdash ( Bestowals ) /emdash]
	[/emdash ( Share of costs ) /emdash]
	[/emdash ( Settlement ) /emdash]
] def
/AccountsSubColumnHeadings [
	[  (Already paid)   (Wines)  ]
	[  (Wines)   (Food etc)  ]
	[  (Owes)   (Is owed)     [(P) {-0.02 Kern} (aid?)]  ]
] def  % Must be same length as AccountsColumnGroupHeadings

/CorkDisplayTopText (The Corks) def

/DecanterLabelsTopText (Decanter labels: cut; paste to business cards; allow to dry; punch holes; hang on clean decanters; fill decanters; wait; pour; drink; enjoy. Also drink plenty of water.) def

/EmptyPageString (Fewer pages than before, so this page now omitted.) def

/LicensingAgreementTextPlacemats (This work is licensed under a Creative Commons Attribution-ShareAlike 4.0 International Licence.) def  % To be consistent with LicensingAgreementLinkPlacemats
```

## German = Deutsche

To be translated: `TastingNotesPageNumCompoundString`, `VoteRecorderTotalColTitle` = `VoteRecorderTotalRowTitle`, `DecanterLabelsTopText`, `EmptyPageString`, and `LicensingAgreementTextPlacemats`. 
If you can, please translate and post in [an issue](http://github.com/jdaw1/placemat/issues).

```PostScript
/VoteRecorderTopTexts [
	[ [(W) {-0.06 Kern} (ein der Nacht?)]  /questiondown ]
	% [ (Was ist es?) ]  % If uncommenting this, insert a 'true' into the VoteRecorderShowTotalRow array.
] def  % Must be same length as GlassesClusteredOnVoteRecorders, each sub-array containing some number of TopTexts
/VoteRecorderInstruction {VoteRecorderShowTotalRow VoteRecorderSheetNum GetEU {()} {(Rekordpunkte, nicht Rang.)} ifelse} bind def
/VoteRecorderMonkeyName (Affe) def

/TastingNotesColumnHeadings [  (Zeiten)  (Auge)  (Nase) (Gaumen)  (Punkte)  ] def

/DecantingNotesTopText [(V) {-0.06 Kern} (erkostungsnotizen)] def
/DecantingNotesColumnHeadingTimes (Dekantierzeit) def
/DecantingNotesColumnHeadingNotes (Korken, branding, etc) def

/AccountsTopText (Die Accounts) def
/AccountsColumnGroupHeadings [
	[/emdash ( Geschenke ) /emdash]
	[/emdash ( Kosten wurden geteilt ) /emdash]
	[/emdash ( Einigung ) /emdash]
] def
/AccountsSubColumnHeadings [  % Maybe change AccountsColumnRelativeWidths
	[ (Bereits bezahlt)  [(W) {-0.06 Kern} (eine)] ]
	[ [(W) {-0.06 Kern} (eine)]  (Essen etc) ]
	[ (Schuldet)  (Ist geschuldet)  (Bezahlt?) ]
] def  % Must be same length as AccountsColumnGroupHeadings

/CorkDisplayTopText (Die Korken) def
```

## Danish = dansk

This little was done long ago, when there were fewer page types and fewer parameters. 
If you can translate the &lsquo;new&rsquo; parameters into Danish, please post them in [an issue](http://github.com/jdaw1/placemat/issues).

```PostScript
/TastingNotesColumnHeadings [  (Gange)  (Eye)  [(N) /ae (se)]  (Mund)  (Score)  ] def
```


## Dutch = Nederlands

This little was done long ago, when there were fewer page types and fewer parameters. 
If you can translate the &lsquo;new&rsquo; parameters into Dutch, please post them in [an issue](http://github.com/jdaw1/placemat/issues).

```PostScript
/TastingNotesColumnHeadings [  (Tijd)  (Kleur)  (Geur)  (Smaak)  (Punten)  ] def
```
