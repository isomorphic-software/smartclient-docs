# String Methods Overview

[← Back to API Index](../main.md)

---

## KB Topic: String Methods Overview

### Description
A method flagged as a [StringMethod](../main_2.md#type-stringmethod) can be specified as a String containing a valid JavaScript expression. This expression will automatically be converted to a function with a return value matching the value of the last statement. Providing a String is not required - you may use a real function instead.

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
Since leafClick is a [StringMethod](../main_2.md#type-stringmethod), however, you can shorten this to:  
```
 TreeGrid.create({
     ...
     leafClick : "if(leaf.name == 'zoo') { alert(1); } else { alert(2); }";
 });
 
```

### See Also

- [Class.registerStringMethods](../classes/Class.md#classmethod-classregisterstringmethods)

---
