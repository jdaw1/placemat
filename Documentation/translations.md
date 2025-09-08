# Translations

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
&#9655;&#xFE0E;&nbsp;*Translations*&nbsp; 
&#9654;&#xFE0E;&nbsp;[Code&nbsp;injection](code_injection.md#readme)&nbsp; 
&#9654;&#xFE0E;&nbsp;[Bitmap&nbsp;images](bitmap_images.md#readme)&nbsp; 
&#9654;&#xFE0E;&nbsp;[Debugging](debugging.md#readme)

----

## Introduction

Some of the parameters contain text in English. 
Of these, some belong to the wines or to the event and so will vary by tasting (e.g., `Circlearrays`, `HeadersLeft`, `ExternalLinks`, `CopyrightStatementPlacemats`, `BackgroundTextsGlassesTexts`). 
But others could have a more fixed translation, as suggested below.

Many languages are missing; most are incomplete; some are improvable. 
If you have the skills and enthusiasm to repair, please provide translations in [an issue](http://github.com/jdaw1/placemat/issues). 
For translators, at the end of this document is the English, in non-PostScript plain text. 
(Obviously the `/ParameterName` do not need translating.)

The only languages eligible for this page are those written in (extended) Latin. 
Alas, Asian languages are [too difficult in PostScript](http://groups.google.com/g/comp.lang.postscript/c/ktoR1NrLsEc/m/UjOyVOfyPKwJ).

The PostScript code contains some kerning, of the form `{-0.06 Kern}`. 
The optimal amount of kerning varies by font, even by version of font: do inspect output and if necessary adjust the kerning.



## English

```PostScript
/VoteRecorderTopTexts [
	[ (Wine Of The Night?)  /questiondown ]
	% [ (What is it?) ]  % If uncommenting this, insert a 'true' into the VoteRecorderShowTotalRow array.
] def  % Must be same length as GlassesClusteredOnVoteRecorders, each sub-array containing some number of TopTexts

/VoteRecorderInstruction {VoteRecorderShowTotalRow VoteRecorderSheetNum GetEU {()} {(Record points, not rank.)} ifelse} def
/VoteRecorderTotalColTitle [(T) {-0.06 Kern} (otal)] def
/VoteRecorderTotalRowTitle [(T) {-0.09 Kern} (otal)] def
/VoteRecorderMonkeyName (Monkey) def

/TastingNotesColumnHeadings [  (Times)  (Eye)  (Nose)  (Mouth)  (Score)  ] def
/TastingNotesPageNumCompoundString [(Page ) {TNSheetNum 1 add 5 string cvs}] def

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

/VoteRecorderInstruction {VoteRecorderShowTotalRow VoteRecorderSheetNum GetEU {()} {(Rekordpunkte, nicht Rang.)} ifelse} def
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



## French = fran&ccedil;ais

Derived from [issue 70](http://github.com/jdaw1/placemat/issues/70), and discussion with its author.

```PostScript
/VoteRecorderTopTexts [  % Must be same length as GlassesClusteredOnVoteRecorders, each sub-array containing some number of TopTexts
	[ [(Vin de la soir) /eacute (e ?)]  /questiondown ]
	% [ [(Qu) /quoteright {-0.06 Kern} (est-ce que c) /quoteright {-0.06 Kern} (est ?)] ]  % If uncommenting this, insert a 'true' into the VoteRecorderShowTotalRow array.
] def  % Must be same length as GlassesClusteredOnVoteRecorders

/VoteRecorderInstruction {VoteRecorderShowTotalRow VoteRecorderSheetNum GetEU {()} {(Noter les points, pas le classement.)} ifelse} def
/VoteRecorderTotalColTitle [(T) {-0.06 Kern} (otal)] def
/VoteRecorderTotalRowTitle [(T) {-0.09 Kern} (otal)] def
/VoteRecorderMonkeyName (Singe) def

/TastingNotesColumnHeadings [  (Heure)  [(V) {-0.06 Kern} (ue)]  (Odorat)  [(Go) /ucircumflex (t)]  (Points)  ] def
/TastingNotesPageNumCompoundString [(Page ) {TNSheetNum 1 add 5 string cvs}] def

/DecantingNotesTopText [(Notes de d) /eacute (cantation)] def
/DecantingNotesColumnHeadingTimes (Heure) def
/DecantingNotesColumnHeadingNotes [/Eacute (tat du li) /egrave (ge, marquage, etc)] def

/AccountsTopText (Les comptes) def
/AccountsColumnGroupHeadings [
	[/emdash ( Dons ) /emdash]
	[/emdash ( Partage des co) /ucircumflex (ts ) /emdash]
	[/emdash ( R) /egrave (glement ) /emdash]
] def
/AccountsSubColumnHeadings [
	[  [(D) /eacute (j) /agrave ( pay) /eacute]   (Vins)  ]
	[  (Vins)   (Aliments etc)  ]
	[  (Doit)   [(Est d) /ucircumflex]   [(P) {-0.02 Kern} (ay) /eacute {( ) stringwidth pop 2 div 0 rmoveto} (?)]  ]
] def  % Must be same length as AccountsColumnGroupHeadings

/CorkDisplayTopText [(Les Li) /egrave (ges)] def

/DecanterLabelsTopText [
	/Eacute (tiquettes de carafe: couper; coller sur des cartes de visite; laisser s) /eacute (cher; percer les trous; )
	(remplir les carafes; attendre; verser; boire; d) /eacute (guster. Boire beaucoup d) /quoteright {-0.06 Kern} (eau.)
] def

/EmptyPageString [(Moins de pages qu) /quoteright (avant, donc cette page est d) /eacute (sormais supprim) /eacute (e.)] def

% Alas no accents. To be consistent with LicensingAgreementLinkPlacemats
/LicensingAgreementTextPlacemats (Ce travail est concede sous une licence Creative Commons Attribution-ShareAlike 4.0 International Licence.) def
```



## Danish = dansk

This little was done long ago, when there were fewer page types and fewer parameters. 

```PostScript
/TastingNotesColumnHeadings [  (Gange)  (Eye)  [(N) /ae (se)]  (Mund)  (Score)  ] def
```



## Dutch = Nederlands

This little was done long ago, when there were fewer page types and fewer parameters. 

```PostScript
/TastingNotesColumnHeadings [  (Tijd)  (Kleur)  (Geur)  (Smaak)  (Punten)  ] def
```



## English, plain text, for translators

Finally, to help non-programmers translating into other langages, the English to be translated follows in non-PostScript *italic* text. 
It should be possible to copy this into a text file, for ease of editing. 
Please do post translations as [an issue](http://github.com/jdaw1/placemat/issues).

* `VoteRecorderTopTexts`:
	- *Wine Of The Night?*
	- *What is it?*
* `VoteRecorderInstruction`: *Record points, not rank.*
* `VoteRecorderTotalColTitle` = `VoteRecorderTotalRowTitle`: *Total*
* `VoteRecorderMonkeyName`: *Monkey*
* `TastingNotesColumnHeadings`:
	- *Times* (i.e., time at which wine decanted)
	- *Eye*
	- *Nose*
	- *Mouth*
	- *Score*
* `TastingNotesPageNumCompoundString`: *Page*
* `DecantingNotesTopText`: *Decanting Notes*
* `DecantingNotesColumnHeadingTimes`: *Decant Time*
* `DecantingNotesColumnHeadingNotes`: *Cork condition, branding, etc*
* `AccountsTopText`: *The Accounts*
* `AccountsColumnGroupHeadings`, `AccountsSubColumnHeadings`:
	- *Bestowals*
		* *Already paid*
		* *Wines*
	- *Share of costs*
		* *Wines*
		* *Food etc*
	- *Settlement*
		* *Owes*
		* *Is owed*
		* *Paid?*
* `CorkDisplayTopText`: *The Corks*
* `DecanterLabelsTopText`: *Decanter labels: cut; paste to business cards; allow to dry; punch holes; hang on clean decanters; fill decanters; wait; pour; drink; enjoy. Also drink plenty of water.*
* `LicensingAgreementTextPlacemats`: *This work is licensed under a* 
