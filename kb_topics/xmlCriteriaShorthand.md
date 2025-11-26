# xmlCriteriaShorthand

[← Back to API Index](../reference.md)

---

## KB Topic: xmlCriteriaShorthand

### Description
_All rules described in this topic are applied any time a property is of type [AdvancedCriteria](../reference.md#object-advancedcriteria) (in both Component XML and JavaScript component creation) and any API declares an [AdvancedCriteria](../reference.md#object-advancedcriteria) param._

A shorthand format for [AdvancedCriteria](../reference.md#object-advancedcriteria) is supported for simple criteria where the outer criterion is assumed to be an "and" operator:

```
 <!-- Simple format -->
 <criteria fieldName="restrictAge" operator="equals" value="true"/>
 
```
This is equivalent to:
```
 <!-- Normal format -->
 <criteria _constructor="AdvancedCriteria operator="and">
   <criteria>
     <criterion fieldName="restrictAge" operator="equals" value="true"/>
   </criteria> 
 </criteria>
 
```
Additionally these defaults are used allowing to simplify AdvancedCriteria declaration:

*   _operator="and"_ default is used if _criteria_ is present at the same level
*   _operator="equals"_ default is used if _fieldName_ is present at the same level
*   _value="true"_ default is used if _operator="equals"_ default was applied

So, shorthand format above could be simplified even more, for example to [conditionally enable a form button](../classes/ButtonItem.md#attr-buttonitemenablewhen):
```
 <!-- Simple format -->
 <enableWhen fieldName="CustomerGrid.anySelected"/>
 
```
Full equivalent:
```
 <!-- Normal format -->
 <enableWhen _constructor="AdvancedCriteria operator="and">
   <criteria>
     <criterion fieldName="CustomerGrid.anySelected" operator="equals" value="true"/>
   </criteria>
 </enableWhen>
 
```
Another example shows all defaults usage, significantly shortening AdvancedCriteria declaration for [boolean dynamic property](../classes/Class.md#attr-classdynamicproperties) (see full setup in *Boolean Dynamic Properties* example):
```
 <!-- Simple format -->
 <trueWhen>
     <criteria fieldName="settingsForm/values/exportFieldWidths" />
     <criteria fieldName="settingsForm/values/exportAs" operator="inSet" >
         <value>xls</value>
         <value>ooxml</value>
     </criteria>
 </trueWhen>
 
```
Full equivalent:
```
 <!-- Normal format -->
 <trueWhen>
     <AdvancedCriteria operator="and">
         <criteria>
             <criterion fieldName="settingsForm/values/exportFieldWidths" operator="equals" value="true"/>
             <criterion fieldName="settingsForm/values/exportAs" operator="inSet" >
                 <value>xls</value>
                 <value>ooxml</value>
             </criterion>
         </criteria>
     </AdvancedCriteria>
 </trueWhen>
 
```
JS example:
```
 // Simple format
 {fieldName: "restrictAge"}

 // Normal format
 {
   _constructor: "AdvancedCriteria",
   operator: "and",
   criteria: [
     {fieldName: "restrictAge", operator: "equals", value: true}
   ]
 }
 
```

---
