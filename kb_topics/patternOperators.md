# patternOperators

[← Back to API Index](../main.md)

---

## KB Topic: patternOperators

### Description
The [search operators](../main.md#type-operatorid) use patterns like "foo\*txt" to match text values. The patterns are similar to the patterns you use to match names of files in a command-line interface, or to the pattern allowed for the SQL "LIKE" operator. The supported search operators are:

*   "matchesPattern" Basic GLOB matching using wildcards.
*   "iMatchesPattern" Basic GLOB matching using wildcards (case insensitive).
*   "containsPattern" GLOB matching using wildcards. Value is considered to meet the criterion if it contains the pattern.
*   "startsWithPattern" GLOB matching using wildcards. Value is considered to meet the criterion if it starts with the pattern.
*   "endsWithPattern" GLOB matching using wildcards. Value is considered to meet the criterion if it starts with the pattern.
*   "iContainsPattern" GLOB matching using wildcards. Value is considered to meet the criterion if it contains the pattern. Matching is case insensitive.
*   "iStartsWithPattern" GLOB matching using wildcards. Value is considered to meet the criterion if it starts with the pattern. Matching is case insensitive.
*   "iEndsWithPattern" GLOB matching using wildcards.Value is considered to meet the criterion if it ends with the pattern. Matching is case insensitive.

See [DataSource.translatePatternOperators](../classes/DataSource.md#attr-datasourcetranslatepatternoperators) for more information on available patterns)

---
