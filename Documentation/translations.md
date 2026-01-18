<a name="top"></a>
# Translations

**Link to the main program**: [placemat.ps](../PostScript/placemat.ps?raw=1)

**Links to documentation**: 
&#9654;&#xFE0E;&#8239;[Introduction,&nbsp;and&nbsp;a&nbsp;first&nbsp;placemat](introduction_first_placemat.md#readme)&nbsp; 
&#9654;&#xFE0E;&#8239;[Fonts&nbsp;and&nbsp;glass&nbsp;decoration](fonts_glasses_decoration.md#readme)&nbsp; 
&#9654;&#xFE0E;&#8239;[Compound&nbsp;Strings&nbsp;and&nbsp;non&#8209;ASCII&nbsp;characters](compound_strings_characters.md#readme)&nbsp; 
&#9654;&#xFE0E;&#8239;[Page&#8209;level&nbsp;controls](page_level.md#readme)&nbsp; 
&#9654;&#xFE0E;&#8239;[Arrangement&nbsp;of&nbsp;glasses&nbsp;on&nbsp;the&nbsp;page](PackingStyles.md#readme)&nbsp; 
&#9654;&#xFE0E;&#8239;[Non&#8209;Glasses&nbsp;Pages](not_glasses.md#readme)&nbsp; 
&#9654;&#xFE0E;&#8239;[Document&#8209;level&nbsp;controls](document.md#readme)&nbsp; 
&#9654;&#xFE0E;&#8239;[Type&nbsp;sizes](type_sizes.md#readme)&nbsp; 
&#9655;&#xFE0E;&#8239;*Translations*&nbsp; 
&#9654;&#xFE0E;&#8239;[Code&nbsp;injection](code_injection.md#readme)&nbsp; 
&#9654;&#xFE0E;&#8239;[Bitmap&nbsp;images](bitmap_images.md#readme)&nbsp; 
&#9654;&#xFE0E;&#8239;[Debugging](debugging.md#readme)

**Links, internal this page**:&nbsp; 
&starf;&#8239;[Top](#top)&nbsp; 
&starf;&#8239;[Introduction](#Introduction)&nbsp; 
&starf;&#8239;[English](#English)&nbsp; 
&starf;&#8239;[Portuguese&nbsp;=&nbsp;*portugu&ecirc;s*](#Portuguese)&nbsp; 
&starf;&#8239;[German&nbsp;=&nbsp;*Deutsche*](#German)&nbsp; 
&starf;&#8239;[French&nbsp;=&nbsp;*fran&ccedil;ais*](#French)&nbsp; 
&starf;&#8239;[Danish&nbsp;=&nbsp;*dansk*](#Danish)&nbsp; 
&starf;&#8239;[Dutch&nbsp;=&nbsp;*Nederlands*](#Dutch)&nbsp; 
&starf;&#8239;[English,&nbsp;plain&nbsp;text,&nbsp;for&nbsp;translators](#English_for_translators)

----

<a name="Introduction"></a>
## Introduction ##

Some of the parameters contain text in English. 
Of these, some belong to the wines or to the event and so will vary by tasting (e.g., `Circlearrays`, `HeadersLeft`, `ExternalLinks`, `CopyrightStatementPlacemats`, `BackgroundTextsGlassesTexts`). 
But others could have a more fixed translation, as suggested below.

Many languages are missing; most are incomplete; some are improvable. 
If you have the skills and enthusiasm to repair, please provide translations in [an issue](http://github.com/jdaw1/placemat/issues). 
For translators, at the end of this document is [the English, in non&#8209;PostScript plain text](#English_for_translators). 
(Obviously,  do not translate the `/ParameterName`s.)

The only languages eligible for this page are those written in (extended) Latin. 
Alas, in PostScript, or at least in this alphabet-assuming PostScript software, [it&nbsp;is&nbsp;too&nbsp;difficult](http://groups.google.com/g/comp.lang.postscript/c/ktoR1NrLsEc/m/UjOyVOfyPKwJ) to use a logography or syllabary or abugida.

The PostScript code contains some kerning, of the form `{-0.06 Kern}`. 
The optimal amount of kerning varies by font, even by version of font: do inspect output and if necessary adjust the kerning.



<a name="English"></a>
## English ##

```PostScript
/VoteRecorderTopTexts
[
	[ % This block's element of VoteRecorderShowTotalRow defaults to false
		(Wine Of The Night?)
		% /questiondown  % Commented out as used approximately never.
	]
	VoteRecorderIncludeGuessing {[
		(What is it?)  % (Vintage?)   [(Y) {-0.12 Kern} (ear?)]  (Age?)  (Shipper?)  (Quinta?)  (Distillery?)  (Vineyard?)  [(Ch) /acircumflex (teau?)]
	]} if
] def
/VoteRecorderMonkeyName (Monkey) def
/VoteRecorderInstruction {VoteRecorderShowTotalRow VoteRecorderSheetNum GetEU {()} {(Record points, not rank.)} ifelse} bind def
/VoteRecorderTotalRowTitle [(T) {-0.09 Kern} (otal)] def
/VoteRecorderColTitlesEarly [  [ ]  VoteRecorderIncludeGuessing {[ (Reveal) [(T) {-0.06 Kern} (otal)] ]} if  ] def
/VoteRecorderColTitlesAfter [  [ [(T) {-0.06 Kern} (otal)] ]   VoteRecorderIncludeGuessing {[ ]} if  ] def

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
] def

/CorkDisplayTopText (The Corks) def

/DecanterLabelsTopText [
	(Decanter labels: cut; paste to business cards; allow to dry; )
	(punch holes; hang on clean decanters; fill decanters; )
	(wait; pour; drink; enjoy. Also drink plenty of water.)
] def

/EmptyPageString (Fewer pages than before, so this page now omitted.) def

/LicensingAgreementTextPlacemats (This work is licensed under a Creative Commons Attribution-ShareAlike 4.0 International Licence.) def
```



<a name="Portuguese"></a>
## Portuguese = *portugu&ecirc;s* ##

Help was received on [ThePortForum&rsquo;s thread 175](https://www.theportforum.com/viewtopic.php?t=175&start=1295#p139593) from [MigSU](https://www.theportforum.com/memberlist.php?mode=viewprofile&u=11877), [Glenn&nbsp;E.](https://www.theportforum.com/memberlist.php?mode=viewprofile&u=168), and [Alex&nbsp;Bridgeman](https://www.theportforum.com/memberlist.php?mode=viewprofile&u=15).

```
/VoteRecorderTopTexts  % Each sub-array contains some TopTexts. Must be same length as GlassesClusteredOnVoteRecorders and as VoteRecorderShowTotalRow
[
	[ % This block's element of VoteRecorderShowTotalRow defaults to false
		(Vinho da Noite?)
		% /questiondown  % Commented out as used approximately never.
	]
	VoteRecorderIncludeGuessing {[
		[(Qual ) /eacute (?)]
	]} if  % VoteRecorderIncludeGuessing
] def  % /VoteRecorderTopTexts, Must be same length as GlassesClusteredOnVoteRecorders and VoteRecorderShowTotalRow

/VoteRecorderMonkeyName (Macaco) def
/VoteRecorderInstruction {VoteRecorderShowTotalRow VoteRecorderSheetNum GetEU {()} {[(Registar os pontos, n) /atilde (o a posi) /ccedilla /atilde (o.)]} ifelse} bind def
/VoteRecorderTotalRowTitle [(T) {-0.09 Kern} (otal)] def
/VoteRecorderColTitlesEarly [  [ ]  VoteRecorderIncludeGuessing {[ (Divulgar) [(T) {-0.06 Kern} (otal)] ]} if  ] def
/VoteRecorderColTitlesAfter [  [ [(T) {-0.06 Kern} (otal)] ]   VoteRecorderIncludeGuessing {[ ]} if  ] def

/TastingNotesColumnHeadings [  (Horas)  (Visual)  (Nariz)  (Boca)  [(Pontua) /ccedilla /atilde (o)]  ] def
/TastingNotesPageNumCompoundString [(P) /aacute (gina ) {TNSheetNum 1 add 5 string cvs}] def

/DecantingNotesTopText [(Notas sobre a decanta) /ccedilla /atilde (o)] def
/DecantingNotesColumnHeadingTimes [(Hora da decanta) /ccedilla /atilde (o)] def
/DecantingNotesColumnHeadingNotes [(Condi) /ccedilla /atilde (o da rolha, marcas, etc)] def

/AccountsTopText (The Accounts) def
/AccountsColumnGroupHeadings [
	[/emdash ( Ofertas ) /emdash]
	[/emdash ( Parte dos custos ) /emdash]
	[/emdash ( Contas finais ) /emdash]
] def
/AccountsSubColumnHeadings [
	[  (Pago)   (Vinhos)  ]
	[  (Vinhos)   (Comida, etc)  ]
	[  (Deve)   (Tem a receber)     [(P) {-0.02 Kern} (ago?)]  ]
] def  % Must be same length as AccountsColumnGroupHeadings

/CorkDisplayTopText (As Rolhas) def

/DecanterLabelsTopText [
	(Etiquetas para decanter: cortar; colar em cart) /otilde (es de neg) /oacute (cios; )
	(deixar secar; fazer buracos; pendurar em decanters limpos; )
	(encher os decanters; esperar; servir; beber; aproveitar. )
	(Beber tamb) /eacute (m muita ) /aacute (gua.)
] def

/EmptyPageString (Fewer pages than before, so this page now omitted.) def

/LicensingAgreementTextPlacemats (This work is licensed under a Creative Commons Attribution-ShareAlike 4.0 International Licence.) def  % To be consistent with LicensingAgreementLinkPlacemats
```


<a name="German"></a>
## German = Deutsche ##

To be translated: `TastingNotesPageNumCompoundString`, `VoteRecorderColTitlesEarly`, `DecanterLabelsTopText`, `EmptyPageString`, and `LicensingAgreementTextPlacemats`. 
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



<a name="French"></a>
## French = fran&ccedil;ais ##

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


<a name="Danish"></a>
## Danish = dansk ##

This little was done long ago, when there were fewer page types and fewer parameters. 

```PostScript
/TastingNotesColumnHeadings [  (Gange)  (Eye)  [(N) /ae (se)]  (Mund)  (Score)  ] def
```



<a name="Dutch"></a>
## Dutch = Nederlands ##

This little was done long ago, when there were fewer page types and fewer parameters. 

```PostScript
/TastingNotesColumnHeadings [  (Tijd)  (Kleur)  (Geur)  (Smaak)  (Punten)  ] def
```



---

<a name="English_for_translators"></a>
## English, plain text, for translators ##

Finally, to help non-programmers translating into other langages, the English to be translated follows in non-PostScript *italic* text. 
It should be possible to copy this into a text file, for ease of editing. 
Please do post translations as [an issue](http://github.com/jdaw1/placemat/issues).

* `VoteRecorderTopTexts`:
	- *Wine Of The Night?*
	- *What is it?*
* `VoteRecorderInstruction`: *Record points, not rank.*
* `VoteRecorderColTitlesAfter`, `VoteRecorderColTitlesEarly`:
	- *Total* (a total of scores)
	- *Reveal* (in the sense of a revelation or publication of what was a wine served blind)
* `VoteRecorderMonkeyName`: *Monkey* (mischievous term for somebody not present who guesses, to set a standard for those present)
* `TastingNotesColumnHeadings`:
	- *Times* (i.e., time at which wine decanted)
	- *Eye*
	- *Nose* (in the sense of &lsquo;of what does it smell&rsquo;)
	- *Mouth* (in the sense of &lsquo;of what does it taste&rsquo;)
	- *Score*
* `TastingNotesPageNumCompoundString`: *Page*
* `DecantingNotesTopText`: *Decanting Notes*
* `DecantingNotesColumnHeadingTimes`: *Decant Time* (in the sense of 14:00, rather than for how long)
* `DecantingNotesColumnHeadingNotes`: *Cork condition, branding, etc*
* `AccountsTopText`: *The Accounts*
* `AccountsColumnGroupHeadings`, `AccountsSubColumnHeadings`:
	- *Bestowals*
		* *Already paid*
		* *Wines* (wines donated)
	- *Share of costs*
		* *Wines* (wines drunk, usually the same for most people)
		* *Food etc*
	- *Settlement*
		* *Owes*
		* *Is owed*
		* *Paid?*
* `CorkDisplayTopText`: *The Corks*
* `DecanterLabelsTopText`: *Decanter labels: cut; paste to business cards; allow to dry; punch holes; hang on clean decanters; fill decanters; wait; pour; drink; enjoy. Also drink plenty of water.*
* `LicensingAgreementTextPlacemats`: *This work is licensed under a* 
* `EmptyPageString`: *Fewer pages than before, so this page now omitted.*
