# FormItemEditProxy Documentation

[← Back to API Index](../reference.md)

---

## Class: FormItemEditProxy

*Inherits from:* [EditProxy](EditProxy.md#class-editproxy)

### Description
[EditProxy](EditProxy.md#class-editproxy) that handles [FormItem](FormItem.md#class-formitem)s when editMode is enabled.

### Groups

- devTools

---
## Attr: FormItemEditProxy.valueMapDisplaySeparatorChar

### Description
If [inline editing](../reference.md#type-inlineeditevent) for this FormItem edits the [FormItem.valueMap](FormItem.md#attr-formitemvaluemap), character that should be used as a separator for entering [ValueMap](../reference_2.md#type-valuemap)s that map from a stored value to a user-displayed value.

With the default of ":", the following input:

```
      1:Fixed, 2:Won't Fix, 3:Resolved
 
```
Would be assumed to be a mapping like this (expressed in JSON):
```
   {
      "1" : "Fixed",
      "2" : "Won't Fix",
      "3" : "Resolved"
   }
 
```

If the input has inconsistent use of the separator char, the input will be assumed to be stored-to-displayed mapping if the separator char is present in a majority of values, and any values that lack a separator will use the same value for storage and display. For example, for this input:

```
       Fixed:Reported Fixed, WontFix:Won't Fix, Resolved
 
```
The resulting `valueMap` would be:
```
   {
      "Fixed" : "Reported Fixed",
      "WontFix" : "Won't Fix",
      "Resolved" : "Resolved"
   }
 
```

The [valueMapEscapeChar](#attr-formitemeditproxyvaluemapescapechar) can be used to enter literal colon characters.

Set `valueMapDisplaySeparatorChar` to null to prevent entry of stored vs displayed values - user input will always be treated as just a list of legal values.

**Flags**: IR

---
## Attr: FormItemEditProxy.valueMapSelectedChar

### Description
If [inline editing](../reference.md#type-inlineeditevent) for this FormItem edits the [FormItem.valueMap](FormItem.md#attr-formitemvaluemap), character that can be used to mark the default selected option. Can appear before or after a value, for example, with this input:
```
     Fixed,Won't Fix,Resolved*
 
```
"Resolved" would be the default selected value.

If multiple values are marked selected for a SelectItem, [SelectItem.multiple](SelectItem.md#attr-selectitemmultiple) will automatically be set.

The [valueMapEscapeChar](#attr-formitemeditproxyvaluemapescapechar) can be used to allow the `valueMapSelectedChar` to appear at the beginning or end of a valueMap value.

**Flags**: IR

---
## Attr: FormItemEditProxy.valueMapEscapeChar

### Description
If [inline editing](../reference.md#type-inlineeditevent) for this FormItem edits the [FormItem.valueMap](FormItem.md#attr-formitemvaluemap), character that can be used to enter literal separator chars (such as the [valueMapSeparatorChar](#attr-formitemeditproxyvaluemapseparatorchar)) or literal leading or trailing whitespace.

Repeat this character twice to enter it literally. For example, with the default of "\\", inputting "\\\\" would result in a literal backslash in the value.

**Flags**: IR

---
## Attr: FormItemEditProxy.valueMapSeparatorChar

### Description
If [inline editing](../reference.md#type-inlineeditevent) for this FormItem edits the [FormItem.valueMap](FormItem.md#attr-formitemvaluemap), character that should be used as a separator between values, or between pairs of stored vs display values if the user is entering such a [ValueMap](../reference_2.md#type-valuemap) using the [valueMapDisplaySeparatorChar](#attr-formitemeditproxyvaluemapdisplayseparatorchar).

If [EditProxy.inlineEditMultiline](EditProxy.md#attr-editproxyinlineeditmultiline) is enabled, newlines will be used as value separators and the `valueMapSeparatorChar`

The [valueMapEscapeChar](#attr-formitemeditproxyvaluemapescapechar) can be used to enter the separator char as part of a valueMap value.

**Flags**: IR

---
