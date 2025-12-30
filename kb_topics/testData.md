# Test Data

[← Back to API Index](../reference.md)

---

## KB Topic: Test Data

### Description
You can create a test file that contains a sample dataset which can be imported into your database table with the Admin Console.

Test data can come in a variety of flavours based on your personal preference.

*   CSV - Comma Separated Values
*   JSON - An array of JSON objects
*   XML - Extensible Markup Language

#### CSV

The test file to use with your DataSource is specified in the `testFileName` DataSource configuration property and will have the `.data.csv` extension.

The CSV file can contain an optional header line as the example below will show you. The headline names can be either DataSource title or field name and are not case sensitive. If the header line is missing it will be assumed that the data/columns are the same order as the field declaration in the DataSource file. This sample represents some moon landing data and you can also use double quotes around more complex values.

```
 mission, duration, launchDate, commander, rover
 "Apollo 11", "195.31", 1969-07-16, "Neil Armstrong", false
 "Apollo 12", "244.61", 1969-11-14, "Charles Conard", false
 "Apollo 13", 142.91, "1970-04-11", "Jim Lovell", false
 "Apollo 14", 216.03, "1971-01-31", "Alan Shepard", false
 "Apollo 15", 295.20, "1971-07-26", "David Scott", true
 "Apollo 16", 265.85, "1972-04-16", "John W. Young", true
 "Apollo 17", "301.87", 1972-12-07, "Eugene Cernan", true
 
```

#### JSON

The test file to use with your DataSource is specified in the `testFileName` DataSource configuration property and will have the `.data.js` extension.

The JSON file needs to contain an array of objects. Each object represents a new record and will contain the properties in a JSON fashion. The names can be either DataSource title or field name and are not case senstive.

```
 [
   {
     category: "Adding Machine/calculator Roll",
     itemName: "Adding Machine Roll 57x57mm Lint Free",
     sku: "226500",
     unitCost: 0.52,
     units: "Roll"
   },
   {
     category: "Pastes and Gum",
     itemName: "Glue UHU Clear Gum 250ml",
     sku: "724800",
     unitCost: 2.26,
     description: "Ideal for paper and card. Dries clear. Easy to use. Washable & Non-Toxic."
   },
   ...
 ]
 
```

#### XML

The test file to use with your DataSource is specified in the `testFileName` DataSource configuration property and will have the `.data.xml` extension.

The test data file should consist of a top-level element containing a series of XML elements, each of which creates one DataSource record. Values for each field are given within tags named after the field name or in the parent tag as an attribute.

For example, the following XML represents a list of supply items.

```
 <records>
  <record>
      <description>A revolutionary cushion-grip ballpoint pen that reduces
          required gripping power, relieving stress and alleviating writing
          fatigue. Excellent for people who suffer from arthritis or carpal
          tunnel syndrome. Medium point, black ink. Refillable.</description>
      <category>1</category>
      <itemRef>ODC 204-502-153</itemRef>
      <maxQuantity>5</maxQuantity>
      <requiresJustification>0</requiresJustification>
      <itemName>Dr. Grip Pens -- Blue Barrel</itemName>
      <itemID>1</itemID>
      <unitCost>4.99</unitCost>
  </record>
  <record>
      <description>A revolutionary cushion-grip ballpoint pen that reduces
          required gripping power, relieving stress and alleviating writing
          fatigue. Excellent for people who suffer from arthritis or carpal
          tunnel syndrome. Medium point, black ink. Refillable.</description>
      <category>1</category>
      <itemRef>ODC 204-708-834</itemRef>
      <maxQuantity>5</maxQuantity>
      <requiresJustification>0</requiresJustification>
      <itemName>Dr. Grip Pens -- Black Barrel</itemName>
      <itemID>2</itemID>
      <unitCost>4.99</unitCost>
  </record>
  <record>
      <description>Personalized business cards for all your networking
          needs.</description>
      <category>2</category>
      <itemRef></itemRef>
      <maxQuantity>500</maxQuantity>
      <requiresJustification>1</requiresJustification>
      <itemName>Personalized business cards -- 500 count</itemName>
      <itemID>3</itemID>
      <unitCost>25.00</unitCost>
  </record>
  ...
 <records/>
 
```
Data for a tree-like DataSource can be specified with the same format. The following code example is for supply categories. This will make use of attribute values instead of separate tags for each property on the supply category. The attribues are not case sensitive and can be named after either the DataSource title or field name.
```
 <categories>
     <category itemName="Office Paper Products" parentID="root" />
     <category itemName="Calculator Rolls" parentID="Office Paper Products" />
     <category itemName="Adding Machine/calculator Roll" parentID="Calculator Rolls" />
     ...
 </categories>
 
```
Note that all records must define values for the itemName primary key field and for the parentID field that establishes the tree relationship.

#### Date, Time and DateTime considerations

When you have date, time or datetime fields these need to be formatted the same way they are expected to be formatted in REST responses. If data for a field does not match the expected format it will be parsed using JDK built-in DataFormat parsers, in lenient mode, in the server's default locale. Examples of date, time and datetime formats.

```
    // date - YYYY-MM-DD
    2014-12-06

    // time - hh:mm:ss
    22:01:45

    // datetime - YYYY-MM-DDThh:mm:ssZ
    2014-12-06T22:01:45-04:00
 
```

### See Also

- [dateFormatAndStorage](dateFormatAndStorage.md#kb-topic-date-and-time-format-and-storage)

---
