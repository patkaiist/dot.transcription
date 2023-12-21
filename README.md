# dot.transcription

This is a system I use in my own data sets for simple, easily-readable concept IDs that include the potential for formatting information and notes, while still being quickly sortable and modifiable as needed. They are static concept names, as part of the multilingual _Sal Area Lexical Inventory for Sino-Tibetan_ (SALIST) word list.

The purpose of this system is so that I can quickly type out detailed concept IDs to keep things distinct in the database while also having readily formatted versions for both a concept name and a gloss. These dot-formatted IDs are used internally for cross-linguistic databases that I work with for documentation and typological purposes.

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