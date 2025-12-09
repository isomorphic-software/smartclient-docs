# DSRequest data auto-converted to bean types

[← Back to API Index](../reference.md)

---

## KB Topic: DSRequest data auto-converted to bean types

### Description
For fields with numeric types, the [record data](../classes/DSRequest.md#attr-dsrequestdata) in DSRequests will automatically be converted to the type of the target field, before the request is received in a [DMI](../classes/DMI.md#class-dmi).

For example, if [your bean](../classes/DataSource.md#attr-datasourcebeanclassname) has a field "price" of type Float, an "update" DSRequest with a new value for this field will use the Java Float type for the new value, whereas in the absence of a bean, the Double type would ordinarily be used (see [RPCRequest.data](../classes/RPCRequest.md#attr-rpcrequestdata)).

This happens only for fields of type _integer_, _sequence_, _intEnum_ and _float_. Because the conversion is performed as part of server-side validation, it applies only to "update" or "add" requests, and does not apply to [DSRequest.oldValues](../classes/DSRequest.md#attr-dsrequestoldvalues), which will continue to use the generic types listed in [RPCRequest.data](../classes/RPCRequest.md#attr-rpcrequestdata).

Note that, while values for non-numeric fields will still use basic Java types (for example, values for Java Enum fields will arrive [as Strings by \\n default](../classes/DataSource.md#attr-datasourceenumtranslatestrategy)), manual conversion of the remaining data is not necessary; the server-side API `DataSource.setProperties()` does all remaining conversion necessary to populate a bean from the request data (see that API's docs for details), and this conversion will be performed automatically if your DMI logic calls `execute()` on the DSRequest.

You may need to explicitly define what Java type must be used during conversion for a given field. This can be achieved by setting [DataSourceField.javaClass](../classes/DataSourceField.md#attr-datasourcefieldjavaclass) property.

If conversion fails, because of target field using an abstract Java type or invalid class defined in DSField.javaClass property etc, conversion will fall back to its default behavior, i.e. Java type will be guessed from the actual field value. It would be Long for integer based types and Double for float type or, if the value would appear to exceed the ranges of these types, BigInteger and BigDecimal accordingly.

---
