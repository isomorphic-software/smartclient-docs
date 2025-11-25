# String Template Functions

[← Back to API Index](../main.md)

---

## KB Topic: String Template Functions

### Description
Template functions provide a flexible way to generate dynamic text, such as AI prompts, email bodies, or custom messages shown in the UI. Templates are plain JavaScript functions that take a `state` object plus a shared support object `sc`, and optionally `j`, which is the default JSON formatter function. `sc` and `j` are described below.

Templates are registered on a class using [Class.registerTemplates](../classes/Class.md#classmethod-classregistertemplates) and later rendered with [Class.render](../classes/Class.md#classmethod-classrender).

#### Defining and using a template
Define templates on a class:
```
    OrderViewer.registerTemplates({
        orderSummaryHTML: function (s, sc, j) {
            return `<b>Order #${s.orderId}</b><br>
 Customer: ${sc.escapeHTML(sc.trim(s.customerName))}<br>
 Status: ${s.status}<br>
 Total: ${sc.toUSCurrencyString(s.totalAmount, 2)}<br>
 `;
        },

        lineItemsHTML: function (s, sc, j) {
            return sc.if(s.items && s.items.length > 0,
                "Line Items:<br>" + sc.for(s.items, function (item) {
                    return `&nbsp;- ${item.quantity} x ${sc.escapeHTML(item.description)} (${sc.NumberUtil.toUSCurrencyString(item.price, 2)})<br>`;
                }),
                "No items on this order."
            );
        }
    });
 
```

Render a template from an instance:

```
    const orderSummaryHTML = orderViewer.render("orderSummaryHTML", {
        orderId: 10234,
        customerName: "  Smith, John  ",
        status: "Pending",
        totalAmount: 259.99
    });

    const orderLineItemsHTML = orderViewer.render("lineItemsHTML", {
        items: [
            { quantity: 2, description: "Widget A", price: 49.95 },
            { quantity: 1, description: "Service Plan", price: 160.09 }
        ]
    });
 
```
#### Template Function Support Object (`sc`)
Each template receives an `sc` parameter providing shared utilities:

*   **sc.json(value, \[pretty\])**: Encode to JSON using SmartClient's [JSONEncoder](../classes/JSONEncoder.md#class-jsonencoder). If `pretty` is `true`, the output is formatted with indentation.
*   **sc.if(condition, thenVal, elseVal)**: Inline conditional expression returning `thenVal` if `true`, otherwise `elseVal`.
*   **sc.for(array, fn)**: Map an array with the given function and join the results into a single string.
*   **sc.trim(value)**: Trim leading and trailing whitespace from the given value converted to a string. If the value is `null`, returns an empty string.
*   **sc.escapeHTML(value)**: Escape HTML in an arbitrary value converted to a string. If the value is `null`, returns an empty string.

The `sc` object also inherits from the global [isc](../main.md#object-isc) object (through prototypal inheritance), so all SmartClient APIs are available (for example, `sc.NumberUtil` references the [NumberUtil](../classes/NumberUtil.md#class-numberutil) class).

### Related

- [Class.registerTemplates](../classes/Class.md#classmethod-classregistertemplates)
- [Class.getTemplate](../classes/Class.md#classmethod-classgettemplate)
- [Class.render](../classes/Class.md#classmethod-classrender)

---
