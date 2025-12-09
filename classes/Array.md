# Array Documentation

[← Back to API Index](../reference.md)

---

## ClassAttr: Array.DATE_VALUES

### Description
This is a built-in comparator for the [find](#method-arrayfind) and [findIndex](#method-arrayfindindex) methods of Array. Passing this comparator to those methods will find instances where Dates in the search criteria match Dates in the array members (ordinarily, Javascript only regards Dates as equal if they refer to the exact same object). This comparator compares _logical_ dates; the time elements of the values being compared are ignored, so two Dates representing different times on the same day will be considered equal.

### See Also

- [Array.DATETIME_VALUES](#classattr-arraydatetime_values)

**Flags**: R

---
## ClassAttr: Array.LOADING

### Description
Marker value returned by Lists that manage remote datasets, indicating the requested data is being loaded. Note that the recommended test for loading data is to call [Array.isLoading](#classmethod-arrayisloading) rather than compare to this value directly.

**Flags**: IRA

---
## ClassAttr: Array.DATETIME_VALUES

### Description
This is a built-in comparator for the [find](#method-arrayfind) and [findIndex](#method-arrayfindindex) methods of Array. Passing this comparator to those methods will find instances where Dates in the search criteria match Dates in the array members (ordinarily, Javascript only regards Dates as equal if they refer to the exact same object). This comparator compares entire date values, including the time elements of the values being compared, so two Dates representing different times on the same day (even if they are only a millisecond apart) will not be considered equal.

### See Also

- [Array.DATE_VALUES](#classattr-arraydate_values)

**Flags**: R

---
## ClassAttr: Array.CASE_INSENSITIVE

### Description
This is a built-in comparator for the [find](#method-arrayfind) and [findIndex](#method-arrayfindindex) methods of Array. Passing this comparator to those methods will find case-insensitively, so, eg, `find("foo", "bar")` would find objects with a "foo" property set to "Bar", "BAR" or "bar"

**Flags**: R

---
## ClassMethod: Array.isLoading

### Description
Is the object passed in a loading marker value? For use with Lists that manage remote datasets, to indicate that a record has not yet been retrieved from the server. A typical use case might be to check if a row has been loaded in a ListGrid - for example:

`if (Array.isLoading(myList.getRecord(0))) isc.warn("Please wait for the data to load.");`

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| value | [Any](#type-any) | false | — | data to test. |

**Flags**: A

---
## ClassMethod: Array.compareAscending

### Description
Compare two values for an ascending order sort, using locale-sensitive comparison.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| a | [Any](#type-any) | false | — | first value to compare |
| b | [Any](#type-any) | false | — | second value to compare |

### Returns

`[number](#type-number)` — negative == second is larger, 0 == same value, positive == first is larger

### Groups

- sorting

**Flags**: A

---
## ClassMethod: Array.compareDescending

### Description
Compare two values for a descending order sort, using locale-sensitive comparison.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| first | [Any](#type-any) | false | — | first value to compare |
| second | [Any](#type-any) | false | — | second value to compare |

### Returns

`[number](#type-number)` — negative == first is larger, 0 == same value, positive == second is larger

### Groups

- sorting

**Flags**: A

---
## Method: Array.find

### Description
Like [Array.findIndex](#method-arrayfindindex), but returns the object itself instead of its index.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| propertyName | [String](#type-string)|[Object](../reference.md#type-object)|[AdvancedCriteria](#type-advancedcriteria) | false | — | property to match, or if an Object is passed, set of properties and values to match |
| value | [Any](#type-any) | true | — | value to compare against (if propertyName is a string) |

### Returns

`[Object](../reference.md#type-object)` — first matching object or null if not found

### Groups

- access
- find

---
## Method: Array.equals

### Description
Return whether this list is equal to another list.

Two lists are equal only if they have the same length and all contained items are in the same order and are also equal.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| list | [List](#type-list) | false | — | list to check for equality |

### Returns

`[boolean](../reference.md#type-boolean)` — whether the specified list is equal to this list

### Groups

- access

---
## Method: Array.setSort

### Description
Sort this Array by a list of [SortSpecifier](../reference_2.md#object-sortspecifier)s.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| sortSpecifiers | [Array of SortSpecifier](#type-array-of-sortspecifier) | false | — | the list of [SortSpecifier](../reference_2.md#object-sortspecifier)s to sort by |

### Returns

`[Array](#type-array)` — the array itself

---
## Method: Array.slide

### Description
Slide element at position start to position destination, moving all the other elements to cover the gap.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| start | [number](#type-number) | false | — | start position |
| destination | [number](#type-number) | false | — | destination position for the value at start |

**Flags**: A

---
## Method: Array.unsort

### Description
Turn sorting off for this array, indicating that the current sort order should be preserved. Return true if this is supported in this List. Some implementations may not support this -- they should return false to indicate to the caller that sort order must be maintained (eg: in the case where sort order is derived from the server, etc).

### Returns

`[boolean](../reference.md#type-boolean)` — true == list supports unsorting, false == not supported.

### Groups

- sorting

**Flags**: A

---
## Method: Array.add

### Description
Add an object to this list, at the end

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| object | [Any](#type-any) | false | — | object to add |

### Returns

`[Any](#type-any)` — pointer to the object passed in

### Groups

- modification

---
## Method: Array.getRange

### Description
Return the items between position start and end, non-inclusive at the end.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| start | [number](#type-number) | false | — | start position |
| end | [number](#type-number) | false | — | end position |

### Returns

`[Array](#type-array)` — subset of the array from start -> end-1

### Groups

- access

---
## Method: Array.getValueMap

### Description
Get a map of the form `{ item[idField] -> item[displayField] }`, for all items in the list. Note that if more than one item has the same value for the `idField`, the value for the later item in the list will clobber the value for the earlier item.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| idField | [String](#type-string) | false | — | Property to use as ID (data value) in the valueMap |
| displayField | [String](#type-string) | false | — | Property to use a display value in the valueMap |

### Returns

`[Object](../reference.md#type-object)` — valueMap object

---
## Method: Array.findNextIndex

### Description
Like [Array.findIndex](#method-arrayfindindex), but inspects a range from `startIndex` to `endIndex`.

For convenience, findNextIndex() may also be called with a function (called the predicate function) for the `propertyName` parameter. In this usage pattern, the predicate function is invoked for each value of the list until the predicate returns a true value. The predicate function is passed three parameters: the current value, the current index, and the list. The value of `this` when the predicate function is called is the `value` parameter. For example:

```
var currentUserRecord = recordList.findNextIndex(0, function (record, i, recordList) {
    if (record.username == currentUsername && !record.accountDisabled) {
        return true;
    }
});
```

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| startIndex | [int](../reference.md#type-int) | false | — | first index to consider. |
| propertyName | [String](#type-string)|[Function](#type-function)|[Object](../reference.md#type-object)|[AdvancedCriteria](#type-advancedcriteria) | false | — | property to match; or, if a function is passed, the predicate function to call; or, if an object is passed, set of properties and values to match. |
| value | [Any](#type-any) | true | — | value to compare against (if `propertyName` is a string) or the value of `this` when the predicate function is invoked (if `propertyName` is a function) |
| endIndex | [int](../reference.md#type-int) | true | — | last index to consider (inclusive). |

### Returns

`[int](../reference.md#type-int)` — index of the first matching value or -1 if not found.

### Groups

- access
- find

---
## Method: Array.setLength

### Description
Set the length of this list.

If the length of the list is shortened, any elements past the new length of the list are removed. If the length is increased, all positions past the old length have the value `undefined`.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| length | [number](#type-number) | false | — | new length |

### Groups

- modification

---
## Method: Array.addList

### Description
Add a list of items to this array.

Note: you can specify that a subset range be added by passing start and end indices

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| list | [Array](#type-array) | false | — | list of items to add |
| listStartRow | [number](#type-number) | true | — | optional start index in list |
| listEndRow | [number](#type-number) | true | — | optional end index in list (non-inclusive) |

### Returns

`[List](#type-list)` — this list, to allow chaining of calls

### Groups

- modification

---
## Method: Array.slideRange

### Description
Slide a range of elements from start to end to position destination, moving all the other elements to cover the gap.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| start | [number](#type-number) | false | — | start position |
| end | [number](#type-number) | false | — | end position (exclusive, like substring() and slice()) |
| destination | [number](#type-number) | false | — | destination position for the range |

**Flags**: A

---
## Method: Array.makeIndex

### Description
Make an index for the items in this Array by a particular property of each item.

Returns an Object with keys for each distinct listItem\[property\] value. Each key will point to an array of items that share that property value. The sub-array will be in the same order that they are in this list.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| property | [String](#type-string) | false | — | names of the property to index by |
| alwaysMakeArray | [boolean](../reference.md#type-boolean) | false | false | if true, we always make an array for every index. if false, we make an Array only when more than one item has the same value for the index property |

### Returns

`[Object](../reference.md#type-object)` — index object

**Flags**: A

---
## Method: Array.max

### Description
Returns the largest number in the array, skipping non-numeric values. If the start and/or end are given, searches the specified subset of the list.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| start | [number](#type-number) | true | — | optional start index (default is 0) |
| end | [number](#type-number) | true | — | optional end index (default is list.length) |

### Returns

`[number](#type-number)` — maximum of all items in the list, or null if all values are non-numeric

### Groups

- arrayMath

---
## Method: Array.getItems

### Description
Return the items at a list of specified positions.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| itemList | [List of Number](#type-list-of-number) | false | — | array of positions |

### Returns

`[Array](#type-array)` — subset of the array, in the same order as itemList

### Groups

- access

---
## Method: Array.sortByProperty

### Description
Sort a list of objects by a given property of each item.

The optional normalizer, if passed as a function, is called for each item in the List, and should return whatever value should be used for sorting, which does not have to agree with the property value. By passing a normalizer function you can achieve any kind of sorting you'd like, including sorting by multiple properties.

NOTE: string sort is case INsensitive by default

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| property | [String](#type-string) | false | — | name of the property to sort by |
| up | [boolean](../reference.md#type-boolean) | false | — | true == sort ascending, false == sort descending |
| normalizer | [Function](#type-function)|[ValueMap](../reference_2.md#type-valuemap) | true | — | May be specified as a function, with signature `normalize(item, propertyName, context)`, where `item` is a pointer to the item in the array, `propertyName` is the property by which the array is being sorted, and `context` is the arbitrary context passed into this method. Normalizer function should return the value normalized for sorting.  
May also be specified as a ValueMap which maps property values to sortable values. |
| context | [Any](#type-any) | true | — | Callers may pass an arbitrary context into the sort method, which will then be made available to the normalizer function |

### Returns

`[List](#type-list)` — the list itself

### Groups

- sorting

---
## Method: Array.or

### Description
Returns true if at least one value between the start and end indices is true.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| start | [number](#type-number) | true | — | optional start index (default is 0) |
| end | [number](#type-number) | true | — | optional end index (default is list.length) |

### Returns

`[boolean](../reference.md#type-boolean)` — at least one of the items is true

### Groups

- arrayMath

---
## Method: Array.containsProperty

### Description
Determine whether this array contains any members where the property passed in matches the value passed in.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| property | [String](#type-string) | false | — | property to look for (object) key:value pairs to look for |
| value | [Any](#type-any) | true | — | value to compare against (if property is a string) |

### Returns

`[boolean](../reference.md#type-boolean)` — true if this array contains an object with the appropriate property value

### Groups

- find

---
## Method: Array.clearProperty

### Description
Delete property in each item in this array.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| property | [String](#type-string) | false | — | name of the property to clear |

### Returns

`[boolean](../reference.md#type-boolean)` — returns true if any of the properties in the array had a value for the specified property.

### Groups

- iteration

---
## Method: Array.isEmpty

### Description
Return whether or not this array is empty

### Returns

`[boolean](../reference.md#type-boolean)` — true == this array is empty, false == some items in the array

### Groups

- access

---
## Method: Array.findIndex

### Description
Find the index of the first Object where property == value in the object.

Pass an Object instead to match multiple properties.

Note: for string values, matches are case sensitive.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| propertyName | [String](#type-string)|[Object](../reference.md#type-object)|[AdvancedCriteria](#type-advancedcriteria) | false | — | property to match, or if an Object is passed, set of properties and values to match |
| value | [Any](#type-any) | true | — | value to compare against (if propertyName is a string) |

### Returns

`[int](../reference.md#type-int)` — index of the first matching Object or -1 if not found

### Groups

- access
- find

---
## Method: Array.map

### Description
Calls a function for each member of an array, passing in the member, its index and the array itself as arguments. Returns a new array containing the resulting values.

This behavior is part of the [ECMA-262 specification](http://www.ecma-international.org/ecma-262/6.0/#sec-array.prototype.map).

**Backwards compatibility note:** Historically SmartClient provided a version of array.map() which differed from the native behavior in a couple of ways:

*   If passed a string as the function argument, it would invoke a same-named method on each member of the array. This is now deprecated in favor of calling [Array.callMethod](#method-arraycallmethod) directly
*   If additional arguments other than the `function` were passed to this method, when the function was invoked for each member, these additional arguments would be passed in when the function was invoked. This is also deprecated as it conflicts with the default native implementation

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| method | [Function](#type-function) | false | — | function to execute for each item |

### Returns

`[Array](#type-array)` — array of returned values

### Groups

- iteration

---
## Method: Array.min

### Description
Returns the smallest number in the array, skipping non-numeric values. If the start and/or end are given, searches the specified subset of the list.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| start | [number](#type-number) | true | — | optional start index (default is 0) |
| end | [number](#type-number) | true | — | optional end index (default is list.length) |

### Returns

`[number](#type-number)` — minimum of all items in the list, or null if all values are non-numeric

### Groups

- arrayMath

---
## Method: Array.lastIndexOf

### Description
Return the position in the list of the last instance of the specified object.

If pos is specified, starts looking before that position.

Returns -1 if not found.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| obj | [Any](#type-any) | false | — | object to look for |
| pos | [number](#type-number) | true | — | last index to consider |
| endPos | [number](#type-number) | true | — | earliest index to consider |

### Returns

`[number](#type-number)` — position of the item, if found, -1 if not found

### Groups

- access

---
## Method: Array.addAt

### Description
Add a single item to this array at a specific position in the list, sliding other items over to fit.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| obj | [Object](../reference.md#type-object) | false | — | object to add |
| pos | [number](#type-number) | false | — | position in the list to add at |

### Returns

`[Object](../reference.md#type-object)` — object that was added

### Groups

- modification

---
## Method: Array.contains

### Description
Return if this list contains the specified object.

If pos is specified, starts looking after that position.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| obj | [Any](#type-any) | false | — | item to look for |
| pos | [number](#type-number) | true | — | optional position in the list to look after |

### Returns

`[boolean](../reference.md#type-boolean)` — true == item was found, false == not found

### Groups

- access

---
## Method: Array.findAll

### Description
Find all objects where property == value in the object.

Pass an Object as the `propertyName` argument to match multiple properties.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| propertyName | [String](#type-string)|[Object](../reference.md#type-object)|[AdvancedCriteria](#type-advancedcriteria) | false | — | property to match, or if an Object is passed, set of properties and values to match |
| value | [Any](#type-any) | true | — | value to compare against (if propertyName is a string) |

### Returns

`[Array](#type-array)` — all matching Objects or null if none found

### Groups

- access
- find

---
## Method: Array.containsAll

### Description
Return whether this list contains all the item in the specified list.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| list | [List](#type-list) | false | — | items to look for |

### Returns

`[boolean](../reference.md#type-boolean)` — whether all items were found

### Groups

- access

---
## Method: Array.last

### Description
Return the last item in this list

### Returns

`[Any](#type-any)` — last item in the list

### Groups

- access

---
## Method: Array.sum

### Description
Returns the sum of the numbers in the array, skipping non-numeric values. If the start and/or end are given, uses only the specified subset of the list.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| start | [number](#type-number) | true | — | optional start index (default is 0) |
| end | [number](#type-number) | true | — | optional end index (default is list.length) |

### Returns

`[number](#type-number)` — sum of all items in the list

### Groups

- arrayMath

---
## Method: Array.indexOf

### Description
Return the position in the list of the first instance of the specified object.

If pos is specified, starts looking after that position.

Returns -1 if not found.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| obj | [Any](#type-any) | false | — | object to look for |
| pos | [number](#type-number) | true | — | earliest index to consider |
| endPos | [number](#type-number) | true | — | last index to consider |

### Returns

`[number](#type-number)` — position of the item, if found, -1 if not found

### Groups

- access

---
## Method: Array.getUniqueItems

### Description
Return a list of each unique item in this list exactly once.

Returns in the same order they were found in the list.

Usage example:  
    uniqueList = myArray.getProperty("foo").getUniqueItems();

### Returns

`[Array](#type-array)` — list of each unique item in the list

### Groups

- subset

---
## Method: Array.dataChanged

### Description
Method called when this array changes in some way. Observe the method to react to changes in this list.

Note: dataChanged() will only fire when items are added, removed or rearranged. If a list contains objects, dataChanged() will not fire if changes are made to objects within the list without changing their position within the list. If an observer of dataChanged() needs to react to such a change, you can manually fire dataChanged() by simply calling it.

Note: may be called multiple times as the result of a multi-item add or remove, etc.

### Groups

- modification

**Flags**: A

---
## Method: Array.set

### Description
Change the array element at a particular position.

set() can be used to expand the length of the list.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| pos | [number](#type-number) | false | — | position in the list to change |
| obj | [Object](../reference.md#type-object) | false | — | new value for that position |

### Returns

`[Object](../reference.md#type-object)` — previous value at that position, or `undefined` if not found

### Groups

- modification

---
## Method: Array.and

### Description
Returns true if all values between the start and end indices are true.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| start | [number](#type-number) | true | — | optional start index (default is 0) |
| end | [number](#type-number) | true | — | optional end index (default is list.length) |

### Returns

`[boolean](../reference.md#type-boolean)` — all of the items in the array are true

### Groups

- arrayMath

---
## Method: Array.intersect

### Description
Return the list of non-`null` items that are contained in this list and each of the argument list(s).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| lists | [All List Arguments](#type-all-list-arguments) | false | — | Lists to intersect with. |

### Returns

`[List](#type-list)` — A new list containing only the non-`null` items that are contained in this list and each of the argument list(s).

### Groups

- arrayMath

---
## Method: Array.first

### Description
Return the first item in this list

### Returns

`[Any](#type-any)` — first item in the list

### Groups

- access

---
## Method: Array.getProperty

### Description
Return a new Array where the value of item i is the value of "property" of item i in this array. If an item doesn't have that property or is null, return item will be null.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| property | [String](#type-string) | false | — | name of the property to look for |

### Returns

`[Array](#type-array)` — array of the values of property in each item of this list

### Groups

- iteration

---
## Method: Array.duplicate

### Description
Return an Array that is a shallow copy of the list, that is, containing the same items.

### Returns

`[Array](#type-array)` — new array, pointing to the same items

### Groups

- access

**Flags**: A

---
## Method: Array.removeList

### Description
Remove all instances of objects in the specified list from this list, sliding the remaining objects around to fill gaps.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| list | [Array](#type-array) | false | — | list of items to remove |

### Returns

`[List](#type-list)` — this list, to allow chaining of calls

### Groups

- modification

---
## Method: Array.removeAt

### Description
Remove the item at the specified position, rearranging all subsequent items to fill the gap

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| pos | [number](#type-number) | false | — | position to remove |

### Returns

`[Any](#type-any)` — item that was removed

### Groups

- modification

---
## Method: Array.callMethod

### Description
Calls a method on each member of an array and returns a new array containing the resulting values.

The `method` argument should be the String name of a method present on each item, which will be invoked. If any item is null or lacks the named method, null will be returned for that item.

Examples:

```
    // line up widgets at 20 pixels from page edge
    [widget1, widget2].callMethod("setPageLeft", 20);

    // find furthest right widget
    [widget1, widget2].callMethod("getPageRight").max();
 
```

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| method | [String](#type-string) | false | — | Name of method to execute for on item |
| arguments 1-N | [Any](#type-any) | true | — | arguments to pass to the method invoked on each item |

### Returns

`[Array](#type-array)` — array of returned values

### Groups

- iteration

---
## Method: Array.getLength

### Description
Return the number of items in this list

### Returns

`[Number](#type-number)` — number of items in the list

### Groups

- access

---
## Method: Array.remove

### Description
Remove first instance of the passed object from this array, sliding other items around to fill gaps.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| obj | [Any](#type-any) | false | — | item to remove |

### Returns

`[boolean](../reference.md#type-boolean)` — true if a matching object was found and removed, false if no matching object was found and the list remains unchanged.

### Groups

- modification

---
## Method: Array.addListAt

### Description
Add list of items list to this array at item pos. All items after array\[pos\] will slide down to fit new items.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| list | [Array](#type-array) | false | — | new array of items |
| pos | [number](#type-number) | false | — | position in this list to put the new items |

### Returns

`[List](#type-list)` — this list, to allow chaining of calls

### Groups

- modification

---
## Method: Array.get

### Description
Return the item at a particular position

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| pos | [Number](#type-number) | false | — | position of the element to get |

### Returns

`[Object](../reference.md#type-object)` — whatever's at that position, or `undefined` if not found

### Groups

- access

---
## Method: Array.setProperty

### Description
Set item\[property\] = value for each item in this array.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| property | [String](#type-string) | false | — | name of the property to set |
| value | [Any](#type-any) | false | — | value to set to |

### Groups

- iteration

---
