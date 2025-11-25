# List Documentation

[← Back to API Index](../main.md)

---

## Method: List.getItems

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
## Method: List.indexOf

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
## Method: List.getLength

### Description
Return the number of items in this list

### Returns

`[Number](#type-number)` — number of items in the list

### Groups

- access

---
## Method: List.addAt

### Description
Add a single item to this array at a specific position in the list, sliding other items over to fit.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| obj | [Object](../main.md#type-object) | false | — | object to add |
| pos | [number](#type-number) | false | — | position in the list to add at |

### Returns

`[Object](../main.md#type-object)` — object that was added

### Groups

- modification

---
## Method: List.sort

### Description
Sorts the elements of the List in place.

The optional comparator function should take two parameters "a" and "b" which are the two list items to compare, and should return:

*   a value less than zero, if "a" is less than "b" such that "a" should appear earlier in the list
*   zero, if "a" and "b" are equal
*   a value greater than zero, if "a" is greater than "b" such that "b" should appear earlier in the list

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| comparator | [Function](#type-function) | true | — | comparator function to use |

### Returns

`[List](#type-list)` — the list itself

---
## Method: List.addListAt

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
## Method: List.removeList

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
## Method: List.getRange

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
## Method: List.get

### Description
Return the item at a particular position

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| pos | [Number](#type-number) | false | — | position of the element to get |

### Returns

`[Object](../main.md#type-object)` — whatever's at that position, or `undefined` if not found

### Groups

- access

---
## Method: List.containsAll

### Description
Return whether this list contains all the item in the specified list.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| list | [List](#type-list) | false | — | items to look for |

### Returns

`[boolean](../main.md#type-boolean)` — whether all items were found

### Groups

- access

---
## Method: List.findIndex

### Description
Find the index of the first Object where property == value in the object.

Pass an Object instead to match multiple properties.

Note: for string values, matches are case sensitive.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| propertyName | [String](#type-string)|[Object](../main.md#type-object)|[AdvancedCriteria](#type-advancedcriteria) | false | — | property to match, or if an Object is passed, set of properties and values to match |
| value | [Any](#type-any) | true | — | value to compare against (if propertyName is a string) |

### Returns

`[int](../main.md#type-int)` — index of the first matching Object or -1 if not found

### Groups

- access
- find

---
## Method: List.duplicate

### Description
Return an Array that is a shallow copy of the list, that is, containing the same items.

### Returns

`[Array](#type-array)` — new array, pointing to the same items

### Groups

- access

**Flags**: A

---
## Method: List.removeAt

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
## Method: List.contains

### Description
Return if this list contains the specified object.

If pos is specified, starts looking after that position.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| obj | [Any](#type-any) | false | — | item to look for |
| pos | [number](#type-number) | true | — | optional position in the list to look after |

### Returns

`[boolean](../main.md#type-boolean)` — true == item was found, false == not found

### Groups

- access

---
## Method: List.equals

### Description
Return whether this list is equal to another list.

Two lists are equal only if they have the same length and all contained items are in the same order and are also equal.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| list | [List](#type-list) | false | — | list to check for equality |

### Returns

`[boolean](../main.md#type-boolean)` — whether the specified list is equal to this list

### Groups

- access

---
## Method: List.findAll

### Description
Find all objects where property == value in the object.

Pass an Object as the `propertyName` argument to match multiple properties.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| propertyName | [String](#type-string)|[Object](../main.md#type-object)|[AdvancedCriteria](#type-advancedcriteria) | false | — | property to match, or if an Object is passed, set of properties and values to match |
| value | [Any](#type-any) | true | — | value to compare against (if propertyName is a string) |

### Returns

`[Array](#type-array)` — all matching Objects or null if none found

### Groups

- access
- find

---
## Method: List.addList

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
## Method: List.sortByProperty

### Description
Sort a list of objects by a given property of each item.

The optional normalizer, if passed as a function, is called for each item in the List, and should return whatever value should be used for sorting, which does not have to agree with the property value. By passing a normalizer function you can achieve any kind of sorting you'd like, including sorting by multiple properties.

NOTE: string sort is case INsensitive by default

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| property | [String](#type-string) | false | — | name of the property to sort by |
| up | [boolean](../main.md#type-boolean) | false | — | true == sort ascending, false == sort descending |
| normalizer | [Function](#type-function)|[ValueMap](../main_2.md#type-valuemap) | true | — | May be specified as a function, with signature `normalize(item, propertyName, context)`, where `item` is a pointer to the item in the array, `propertyName` is the property by which the array is being sorted, and `context` is the arbitrary context passed into this method. Normalizer function should return the value normalized for sorting.  
May also be specified as a ValueMap which maps property values to sortable values. |
| context | [Any](#type-any) | true | — | Callers may pass an arbitrary context into the sort method, which will then be made available to the normalizer function |

### Returns

`[List](#type-list)` — the list itself

### Groups

- sorting

---
## Method: List.add

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
## Method: List.findNextIndex

### Description
Like [List.findIndex](#method-listfindindex), but inspects a range from `startIndex` to `endIndex`.

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
| startIndex | [int](../main.md#type-int) | false | — | first index to consider. |
| propertyName | [String](#type-string)|[Function](#type-function)|[Object](../main.md#type-object)|[AdvancedCriteria](#type-advancedcriteria) | false | — | property to match; or, if a function is passed, the predicate function to call; or, if an object is passed, set of properties and values to match. |
| value | [Any](#type-any) | true | — | value to compare against (if `propertyName` is a string) or the value of `this` when the predicate function is invoked (if `propertyName` is a function) |
| endIndex | [int](../main.md#type-int) | true | — | last index to consider (inclusive). |

### Returns

`[int](../main.md#type-int)` — index of the first matching value or -1 if not found.

### Groups

- access
- find

---
## Method: List.lastIndexOf

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
## Method: List.last

### Description
Return the last item in this list

### Returns

`[Any](#type-any)` — last item in the list

### Groups

- access

---
## Method: List.find

### Description
Like [List.findIndex](#method-listfindindex), but returns the object itself instead of its index.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| propertyName | [String](#type-string)|[Object](../main.md#type-object)|[AdvancedCriteria](#type-advancedcriteria) | false | — | property to match, or if an Object is passed, set of properties and values to match |
| value | [Any](#type-any) | true | — | value to compare against (if propertyName is a string) |

### Returns

`[Object](../main.md#type-object)` — first matching object or null if not found

### Groups

- access
- find

---
## Method: List.dataChanged

### Description
Method called when this array changes in some way. Observe the method to react to changes in this list.

Note: dataChanged() will only fire when items are added, removed or rearranged. If a list contains objects, dataChanged() will not fire if changes are made to objects within the list without changing their position within the list. If an observer of dataChanged() needs to react to such a change, you can manually fire dataChanged() by simply calling it.

Note: may be called multiple times as the result of a multi-item add or remove, etc.

### Groups

- modification

**Flags**: A

---
## Method: List.remove

### Description
Remove first instance of the passed object from this array, sliding other items around to fill gaps.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| obj | [Any](#type-any) | false | — | item to remove |

### Returns

`[boolean](../main.md#type-boolean)` — true if a matching object was found and removed, false if no matching object was found and the list remains unchanged.

### Groups

- modification

---
## Method: List.setLength

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
## Method: List.intersect

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
## Method: List.getValueMap

### Description
Get a map of the form `{ item[idField] -> item[displayField] }`, for all items in the list. Note that if more than one item has the same value for the `idField`, the value for the later item in the list will clobber the value for the earlier item.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| idField | [String](#type-string) | false | — | Property to use as ID (data value) in the valueMap |
| displayField | [String](#type-string) | false | — | Property to use a display value in the valueMap |

### Returns

`[Object](../main.md#type-object)` — valueMap object

---
## Method: List.getProperty

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
## Method: List.first

### Description
Return the first item in this list

### Returns

`[Any](#type-any)` — first item in the list

### Groups

- access

---
## Method: List.isEmpty

### Description
Return whether or not this array is empty

### Returns

`[boolean](../main.md#type-boolean)` — true == this array is empty, false == some items in the array

### Groups

- access

---
## Method: List.set

### Description
Change the array element at a particular position.

set() can be used to expand the length of the list.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| pos | [number](#type-number) | false | — | position in the list to change |
| obj | [Object](../main.md#type-object) | false | — | new value for that position |

### Returns

`[Object](../main.md#type-object)` — previous value at that position, or `undefined` if not found

### Groups

- modification

---
