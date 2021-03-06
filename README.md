# FFRGS-Specification
FFRGS (Fair Formatted Reference Genome Standard): a simple FAIR enough metadata structure for genomes that you can TRUST
[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.6762549.svg)](https://doi.org/10.5281/zenodo.6762549)

Part of what FFRGS sets off to do is make sure that we can map back to Schema.org as much as possible, this will be useful for microdata and rdfa conversions for users that want to embed data into genome webpages. We also want to be able to split out the header if we have to, we can make the coding easy on ourselves if we throw yaml into the header itself. or something that is a regex away from yaml. I think it's important that the header has a secondary character after the comment delineator to indicate that this is part of the header, otherwise a simple mistake in a regex for the header could easily grab regular comments in the fasta file. I also think that the secondary header delineating character should be on the keyboard, and not a yaml special character, this leaves the tilde as the best option. I could imagine it would look something like this:
 
```
;~schema: https://raw.githubusercontent.com/FFRGS/FFRGS-Specification/main/ffrgs.json
;~schemaVersion: 1
;~genome: Bombas huntii
;~version: 0.0.1
;~author:
;~  name: Adam Wright
;~  url: https://wormbase.org/resource/person/WBPerson30813
;~assembler:
;~  name: David Molik
;~  url: https:/david.molik.co/person
;~dateCreated: '2022-03-21'
;~taxa: Bombas huntii
;~place:
;~  name: PBARC
;~  url: https://www.ars.usda.gov/pacific-west-area/hilo-hi/daniel-k-inouye-us-pacific-basin-agricultural-research-center/
;~instrument:
;~- Sequel IIe
;~- Nanopore
;~physicalSample: Located in Freezer 33, Drawer 137
;~scholarlyArticle: https://doi.org/10.1371/journal.pntd.0008755
;~documentation: 'Built assembly from... '
;~identifier:
;~- gkx10242566416842
;~relatedLink:
;~- https/david.molik.co/genome
;~funding: 'some'
;~licence: 'public domain'
>Contig 1
AAAATCGATCGGCATA
``` 
 
## Metadata Draft v0.2 (fasta yaml header with easy microdata conversions)
FFRGS utilizes schema.org as much as possible for later integration

---
Specialised instances of Schema.org (we want as few of these as possible):
 
- `schemaVersion` (String) - Version of FFRGS (Currently always "1.0")
- `genome` (String) - ( Schema.org name )
- `version` (String) - ( Schema.org version ) Version of the Genome
- `license` (String) - ( Schema.org license ) License used (url or name of common license) 
- `funding` (String) - ( Schema.org funding ) Name of Grant used in the creation of the genome
 
These will always be remaps of properties, so:

``` 
Genome: <name>
```

---
Instances of Schema.org entities, where we just want a name and url because we???re not storing that data here: 
 
- `author` - ( Schema.org author ) (URL and String)
- `assembler` - creator of the genome ( Schema.org Person or Organisation ) (URL and String)
- `place` (URL) (Schema.org Place)  (URL and String)
- `assemblySoftware` (Schema.org SoftwareApplication) (URL and String) [Optional]
- `physicalSample` (String) - ( Schema.org Thing ) (URL and String)

These will be names, and urls:

``` 
author: 
 name: Name
 url: https://link 
```

---
Direct use of Schema.org entities:
 
- `dateCreated` (DataTime) (Schema.org dateCreated) (date)
- `instrument` (Schema.org instrument) (URL or String) [Optional]
- `scholarlyArticle` (Schema.org ScholarlyArticle) (URL) [Optional]
- `documentation` (Schema.org documentation) (URL or String) [Optional]
- `identifier` (Schema.org identifier ) (String) [Optional]
- `relatedLink` (Schema.org relatedLink) (URL) [Optional]

``` 
These are all direct use:
 
- `dateCreated`: <date>
```

Another benefit of having this easy conversion is that we can submit the spec to say bioschema without much work after publishing. 

