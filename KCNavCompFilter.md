# The Compositions Filter
   ![KCNav Compositions filter screeenshot](/KCNavCompFilter/CompFilter.png)

The Compositions filter is one of the most important and often least-understood elements of KCNav's filtering system. It allows you to specify criteria to match against the fleet compositions used in sorties. Using this filter, you can specify ships and classes to be included or excluded, and even place restrictions upon how many of each ship class the fleets should have.

## Search terms
The basic terms used within the Compositions filter are *ships* and *classes*, and they may be written in either English (e.g. `Akebono Kai Ni` and `DD`) or Japanese[^1] (e.g. `曙改二` and `駆逐`).

[^1]: The Ship Classes filter always shows the English names for these classes, but localized names for them can be viewed by hovering your mouse over the class in question.

### Ship names
Ship names are always interpreted literally. For instance, if you specify `Nelson`, it will assume you mean *base* Nelson, *not* remodeled Nelson Kai. If you wish to search for a remodel, you must specify the *exact* remodel you're searching for, e.g. `Nelson Kai`.

If you misspell a ship name, KCNav will usually be able figure out what you intended, as long as it's still fairly close.

KCNav also supports a set of aliases/nicknames commonly used among the western community. You can use these aliases in place of the actual ship names, for convenience.

Examples:

`bono` → Akebono

`whale` → Taigei

`kamo` → Akitsushima

`abruzzi` → Duca degli Abruzzi

`sushi k2` → Musashi Kai Ni

`shoukek k2a` → Shoukaku Kai Ni A

## Filter syntax
The Compositions filter generally follows the English community's conventions for specifying fleet compositions. This is typically written as ship and class names, with a separator character between each entry. The separator character is typically a dash (`-`), but may alternatively be a comma (`,`), semicolon (`;`), or simply whitespace (` `).

For example, these are all equivalent:

`BB BB CVL CL DD DD`

`BB-BB-CVL-CL-DD-DD`

`BB,BB,CVL,CL,DD,DD`

`BB;BB;CVL;CL;DD;DD`

## Filter logic
Typically, the Compositions filter operates in an *explicit* inclusion mode. This means that the query is executed exactly as written, and applies to the fleet as a whole. The user must ensure that their query accounts for the number of ships they're intending to match against. E.g. if you search for `DD DD`, this will *only* produce results with *exactly* two Destroyers, and *no other ships* -- because the query only provided criteria for those two ships.

In order to match a subset of the fleet while still returning full fleets of six ships, you *must* account for the remaining ships. There are ways to perform more open-ended queries, as seen in the following sections.

## Wildcards
If you wish to only specify explicit values for *part* of a fleet's composition, while not caring so much about the rest, you can use wildcard syntax. There are two types of wildcards: *explicit* and *open-ended*.

### Explicit wildcard: `XX`
The 'Explicit' wildcard allows you to specify a placeholder for a ship not already accounted for by the rest of the query. It will match any ship, as long as it does not conflict with the other query criteria.

Example: `DD XX` will match all fleets with one Destroyer, one additional ship of any type (which may *also* be a Destroyer), and *no other ships*.

### Open-ended wildcard: `*`
The 'Open-ended' wildcard allows you to specify a placeholder for *any number of ships* not already accounted for by the rest of the query. It will match any number (zero or more) of any type of ship, as long as they do not conflict with the other query criteria.

Example 1: `DD *` will match all fleets with at least one Destroyer, and any number (including zero) of *any other ships*.

Example 2: `Taigei SS *` will match all fleets with Taigei, at least one Submarine, and any number (including zero) of *any other ships*.

### Combining wildcards
You may combine wildcards as desired.

Example: `BB CVL XX XX *` will match all fleets with at least one Battleship, one Light Carrier, and having *at least* four ships in total.

### Exclusion: `!`
If you wish to *exclude* a ship or class from the results, you may include it within your query, and prefix it with an exclamation mark (`!`). This tells the system that it should ensure that its results *do not* include the specified ship or class.

Example: `!Nelson Kai *` will match all fleets, with any number of ships, that *do not* include Nelson Kai.

## Class counts
If you wish to specify that a fleet should include more than one of a specific class, you can do this either by specifying the class multiple times (e.g. `DD DD`) or by specifying the desired number as a prefixed value (e.g. `2DD`).

### Strict count: `=`
Normally, wildcards (`XX` and `*`) can match additional ships of classes you've already specified in the query. For instance, in an example above, `DD XX` can potentially match fleets with two Destroyers.

If you want greater control over the exact quantities matched of a given class, you can use the 'strict' prefix (`=`). This will force the query to *only* match *exactly* the number you specify, and the wildcard will no longer be allowed to match that class.

Example: `BB =2DD *` will match fleets with *one or more* Battleships, *exactly two* Destroyers, and any number (including zero) of any *other* ship classes. the `=2DD` tells it that the count is *strict*, and it shouldn't attempt to match additional Destroyers using the `*` wildcard.

## Variable counts
In more complex queries, you might have more specific requirements for the counts of specific classes. There are a number of ways to build more dynamic searches, as outlined in the following sections.

### Ranges
If you want to specify a varying number of a given class to match against, you can use a range value. This is similar to specifying the count normally, except you specify the minimum and maximum counts you're looking for, with a dash (`-`) separating the min/max values.

Example: `2-4DD *` will match all fleets with at least two, and at most four Destroyers.

### Comparators: `>`, `>=`, `<`, `<=`
Another option for specifying varying numbers of a given class is via comparators. The logic is similar to how you might do numeric comparisons in mathematics, using 'greater than' (`>`), 'greater than or equal to' (`>=`), 'less than' (`<`), and 'less than or equal to' (`<=`).

Example 1: `BB CVL CL <2DD *` will match fleets with at least one Battleship, at least one Light Carrier, at least one Light Cruiser, *zero or one* (less than two) Destroyers, and any number of other ships.

Example 2: `>=3DD` will match fleets with three or more ships, all of which must be Destroyers.

### Limiting fleet size
By prefixing the open-ended wildcard `*` with a numeric constraint, you can place a limit upon the total number of ships in the matched fleets. This can be handy when using numeric constraints on other classes in maps like 1-5 where full fleets may not always be desired.

Example: `>=2DD <=4*` will match all fleets with *four or less* ships total, where *two or more* of those ships are Destroyers.

## Multi-class selectors
Frequently, being forced to provide the exact set of classes is inadequate. For instance, you might want to see runs that include all battleship variants, including fast and aviation battleships. Or you might not care about the distinction between standard carriers and armored carriers. With the multi-class syntax, it's possible to achieve this by specifying multiple classes for any given entry in the query.

### Delimited class lists
The standard way of doing this is by using a delimiter to provide a list of classes the query should try to match.

By separating the classes with the `|` or `/` symbol, it will attempt to match against any class within the specified list. It does not matter which of the two symbols you use.

Example 1: `CL/DD` will match either a light cruiser or destroyer. This can also be written as `CL|DD`.

Example 2: `BB|BBV|FBB` will match any battleship variant.

### Multi-class shorthand
In addition to manually specifying the list of classes to match against, KCNav also supports the following shorthand syntax:

`(F)BB`, `BB(V)`, `(F)BB(V)`, `BB*`: Battleship variants (BB, FBB, BBV)

`CV(L)`, `CV(B)`, `CV(B/L)`, `CV(L/B)`, `CV*`: Carrier variants (CV, CVB, CVL)

`CA(V)`, `CA*`: Heavy cruiser variants (CA|CAV)

`CL(T)`: Light/torpedo cruisers (CL|CLT)

`CL*`: Light/torpedo/training cruisers (CL|CLT|CT)

`SS(V)`, `SS*`: Submarine variants (SS|SSV)

`DD(E)`, `DD*`: Destroyers and coastal defense ships (DD|DE)

`AUX`: Seaplane tenders, repair ships, submarine tenders, fleet oilers, amphibious assault ships (AV|AR|AS|AO|LHA)

`HEAVY`: Heavy ships (BB|FBB|BBV|CV|CVB)

`MEDIUM`, `MED`: Medium ships (CA|CAV|CL|CT|CLT)

`LIGHT`: Light ships (DD|DE|SS|SSV)

`SUB`: Submarine fleet ships (AS|SS|SSV)

`AVIATION`, `VV`: Aviation ships (BBV|CV|CVL|CVB|CAV|AV)

`TORP`, `TS`: Torpedo squadron ships (CL|CLT|DD)

### Class counts
The multi-class syntax can be used in the same ways as single-class syntax, including the use of class counts, ranges, and explicit markers.

Note that when you specify a count for a multi-class entry, it will allow for any combination of the specified classes that meets the counts specified.

Example 1: `2DD|DE` will match DD+DD, or DE+DE, or DD+DE.

Example 2: `(F)BB =2HEAVY 1-2DD|DE *` will match against one BB or FBB, exactly two 'heavy' ships (battleship variants and standard/armored carriers), one or two destroyers or coastal defense ships, and any number of ships of any class that are *not* 'heavy' ships, destroyers, or coastal defense ships (due to the `=` prefix on the HEAVY entry and the range constraint on the DD|DE entry).
