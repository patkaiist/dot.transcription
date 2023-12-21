# dot.transcription

This is a system I use in my own data sets for simple, easily-readable concept IDs that include the potential for formatting information and notes, while still being quickly sortable and modifiable as needed. They are static concept names, as part of the multilingual _Sal Area Lexical Inventory for Sino-Tibetan_ (SALIST) word list.

The purpose of this system is so that I can quickly type out detailed concept IDs to keep things distinct in the database while also having readily formatted versions for both a concept name and a gloss. These dot-formatted IDs are used internally for cross-linguistic databases that I work with for documentation and typological purposes.

It is meant to allow like-concepts to be grouped together as part of the unique concept identifierr without cluttering a display name or gloss. 

For example, `bee` and `bee.:hornet` should reaonsably be connected semantically, but "bee" should not be part of a gloss or simple name for the concept. Likewise `bee::hive` includes a separator that still links it to a semantic "bee" region in the list, and `bee..general` flags the concept as the most general term for bees while not needing to include that as part of a gloss.

Verb stems are explicitly marked with `:to` in all cases, without exception, reducing ambiguity in the concept naming.

Outside of the formatting itself, but related to the form in which concept IDs exist, all ambiguous concepts require some form of additional information in the ID to prevent confusion. A concept `spicy` may be misinterpreted in elicitation based on one's dialect of English to mean "having a great amount of spices". This is resolved by appending `..of.chilis`. While many such ambiguities should also be clear in the corresponding definitions for each comment, by including such information in the concept ID itself, there is one less possible point of confusion for those conducting the elicitation and data coding.

## tags

```
:       swap items in the gloss or name
:.      display only items to the left in the gloss or name
.:      display only items to the right in the gloss or name
::      separator for semantic concept sorting
..      drop everything after in the display. used for notes, functionally the same as :.
:::     Linnean taxonomy formatting
```

The basic table looks like this:

| concept | name | gloss | conc_id | conc_name |
|--------------------------|------------------------|---------------|--------:|-----------|
| bed | bed | bed | 1663 | BED |
| bee::hive | beehive | beehive | 88 | BEEHIVE |
| bee.:hornet | hornet | hornet | 3261 | HORNET |
| bee..general | bee (general) | bee | 665 | BEE |
| big:to.be | to be big | big | 1202 | BIG |
| bind:to | to bind | bind | | |
| bite:to | to bite | bite | | |
| bitter:to.be | to be bitter | bitter | 887 | BITTER |
| blanket | blanket | blanket | 806 | BLANKET |
| blind:to.be | to be blind | blind | | |
| blood | blood | blood | 946 | BLOOD |
| blunt..of.edge:to.be | to be blunt (of edge) | blunt | 379 | BLUNT |
| bone | bone | bone | 1394 | BONE |
| bos.frontalis..mithun::: | _Bos frontalis (mithun)_ | bos.frontalis | – | – |
| bos.gaurus..gaur::: | _Bos gaurus (gaur)_ | bos.gaurus | – | – |

The easiest way to use this right now is in a spreadsheet. In a spreadsheet, the concept value is easily converted to the name with `=SUBSTITUTE(REGEXREPLACE(REGEXREPLACE(REGEXREPLACE(REGEXREPLACE(REGEXREPLACE(IF(RIGHT(D2,3)=":::", UPPER(LEFT(D2,1))&MID(D2,2,LEN(D2)-4), D2),"([0-9a-z.]+)\:\.([0-9a-z.]+)","$1"),"([0-9a-z.]+)\.\:([0-9a-z.]+)","$2"),"([a-z.]+)\:\:([a-z.]+)","$1$2"),"([a-z.]+)\:([a-z.]+)","$2.$1"),"([0-9a-z.]+)\.\.([0-9a-z.]+)","$1 ($2)"),"."," ")`.

The name can then be converted to the gloss with `=REGEXREPLACE(REGEXREPLACE(LOWER(SUBSTITUTE(SUBSTITUTE(REGEXREPLACE(REGEXREPLACE(E2,"^to.be.",""),"^to.have.",""),".of.bird","")," ",".")),"^to.",""), "\.\([^)]*\)", "")`.

## Reasonable questions to ask

Is this the best way to do this? Probably not.

Is it useful to anyone but me? Possibly not.