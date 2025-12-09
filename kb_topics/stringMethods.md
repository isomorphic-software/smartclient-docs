# String Methods Overview

[← Back to API Index](../reference.md)

---

## KB Topic: String Methods Overview

### Description
A method flagged as a [StringMethod](../reference_2.md#type-stringmethod) can be specified as a String containing a valid JavaScript expression. This expression will automatically be converted to a function with a return value matching the value of the last statement. Providing a String is not required - you may use a real function instead.

For example - suppose you wanted to override the `leafClick()` method on the TreeGrid. Normally you would do so as follows:  

```
 TreeGrid.create({
     ...
     leafClick : function(viewer, leaf, recordNum) { 
         if(leaf.name == 'zoo') { 
             alert(1); 
         } else {
             alert(2);
         }
     }
 });
 
```
Since leafClick is a [StringMethod](../reference_2.md#type-stringmethod), however, you can shorten this to:  
```
 TreeGrid.create({
     ...
     leafClick : "if(leaf.name == 'zoo') { alert(1); } else { alert(2); }";
 });
 
```

**TypeScript Limitation**

When using SmartClient with TypeScript, string methods cannot be used because TypeScript's type system cannot express that a property accepts either a function OR a string in configuration objects, while still being callable as a function on component instances.

In TypeScript code, always use arrow functions instead of string methods:

```
 isc.TreeGrid.create({
     ...
     leafClick: (viewer, leaf, recordNum) => {
         if (leaf.name == 'zoo') { alert(1); } else { alert(2); }
     }
 });
 
```
Note that arrow functions capture the lexical `this`, so if your string method used `this` to reference the component, you should instead reference the component by its ID or via a variable.

### See Also

- [Class.registerStringMethods](../classes/Class.md#classmethod-classregisterstringmethods)

---
