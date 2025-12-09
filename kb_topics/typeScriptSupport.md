# TypeScript Support

[← Back to API Index](../reference.md)

---

## KB Topic: TypeScript Support

### Description
Isomorphic ships a TypeScript descriptor file that provides code completion and inline documentation with modern IDEs. Modern versions of Eclipse, Visual Studio, IntelliJ and other IDEs can detect this file for you, or you may choose to add explicit descriptor references in a special comment at the top of your own .ts file. For example:
```
 /// <reference path="path/to/isomorphic/system/development/smartclient.d.ts"/>
 
```
As you can see above, the descriptor file resides in the isomorphic/system/development directory and is called smartclient.d.ts. You can copy this file to another location if you prefer (it is fully self contained), but note that new versions of SmartClient will ship with an up-to-date version of this file.

Some things to keep in mind:

*   This support generally works with .ts and .js files with IDEs that support descriptor references like the above.
*   The goal is to provide autocomplete, inline docs, and spelling/type checks for your code, not every TypeScript feature. This means, for example, that you generally cannot extends Isomorphic's classes using the typescript 'extends' syntax. Instead, you should use the standard [isc.defineClass](../classes/isc.md#staticmethod-iscdefineclass) call to create new class definitions. Isomorphic actually recommends using JavaScript to interact with SmartClient, negating the need for transpilation and allowing you to debug exactly what you've written.
*   There is specialized support for the instantiation [Class.create](../classes/Class.md#classmethod-classcreate) method. Generally, with SmartClient, you can pass as many object literals as you want to this method. The TypeScript descriptor currently supports only 2. The first one is a type-checked property block that supports only the methods and properties declared on the class you are attempting to create (or any of its superclasses or implemented interfaces). The second block does no type checking. The goal here is to make it easy for you to use auto-complete, type checking, and spell checking when you intend to reference actual API methods and properties, but to still allow you to pass arbitrary properties and custom methods that you may be using in your specific instance of the class (via that second constructor block).  
      
    For example:  
    ```
     isc.ListGrid.create({
         // this block will be type-checked and auto-complete enabled
    
         // the "false" value will be flagged as an error becuse a boolean, not a string is expected
         autoDraw: "false",
    
         // valid, no error
         width: 100, 
    
         // the typo in the property name "height" will be flagged as an error
         heght: 100 
     },{
         // this block will not be validated in any way
         myCustomMethod: function () { },
         myFoo: "bar"
     });
     
    ```
    
*   Using the static [_Class_.getById()](../classes/Canvas.md#classmethod-canvasgetbyid) methods allow developers to retrieve instances of specific classes by their [global ID](../classes/Canvas.md#attr-canvasid) in a type-aware manner. IDEs with TypeScript support can then offer appropriate auto-completion, type checking and documentation for attributes and methods on the returned object.
*   **FormItem Type Narrowing with editorType**: The TypeScript descriptor uses a discriminated union type called `FormItemConfig` that enables type-specific property checking based on the `editorType` property. This is particularly important for nested editor configurations like `editorProperties` and `filterEditorProperties` in [ListGrid](../classes/ListGrid_1.md#class-listgrid) field definitions.  
      
    For example:  
    ```
     // TypeScript knows this is a SelectItem configuration
     {name:"category", editorType:"SelectItem",
         editorProperties: {
             // addUnknownValues is a valid SelectItem property
             addUnknownValues: true,
             // TypeScript will flag errors for invalid SelectItem properties
             invalidProp: 123  // Error!
         }
     }
     
    ```
    **Using Custom FormItem Subclasses:** TypeScript's discriminated union types cannot be extended from application code, so custom FormItem types require workarounds to maintain type checking. Application developers have two options:  
      
    **Option 1: Cast to Partial Superclass** (simpler, recommended):
    ```
     {
         name: "myField",
         editorType: "MyCustomSelectItem",  // extends SelectItem
         valueMap: ["A", "B"],              // Type-checked as SelectItem property
         myCustomProp: true                 // No error due to cast
     } as Partial<SelectItem>
     
    ```
    **Option 2: Create Custom Type Definition** (more complete type checking):
    ```
     // In your .d.ts file:
     interface MyCustomSelectItem extends SelectItem {
         myCustomProp?: boolean;
     }
    
     // In your code:
     {
         name: "myField",
         editorType: "MyCustomSelectItem",
         valueMap: ["A", "B"],
         myCustomProp: true
     } as Partial<MyCustomSelectItem>
     
    ```
    **Framework Developers:** When adding a new [FormItem](../classes/FormItem.md#class-formitem) subclass to the SmartClient framework itself, update the `FormItemConfig` type in smartclient.d.ts:
    ```
     type FormItemConfig =
       | ({ editorType: "TextItem" } & Partial<TextItem>)
       | ({ editorType: "SelectItem" } & Partial<SelectItem>)
       | ({ editorType: "YourNewItem" } & Partial<YourNewItem>)  // Add here
       ...
     
    ```
    
*   **Suppressing Type Checking for Custom Properties and Methods**: When adding custom properties or methods to SmartClient component instances that are not part of the official API, TypeScript will flag these as errors. You can suppress these errors on a per-line basis using TypeScript's directive comments:  
      
    
    *   `// @ts-ignore` - Suppresses type checking for the next line. Simple and straightforward for one-off custom additions.
    *   `// @ts-expect-error` - Similar to @ts-ignore, but will warn if the error goes away (useful if you expect the property to be added to the official API later).
    
    Both directives only affect the single line immediately following them and do not disable type checking inside method bodies. For example:
    ```
     isc.ListGrid.create({
         autoDraw: true,
         // @ts-ignore Custom method - calculates special totals
         calculateCustomTotal: function() {
             // Type checking is still active here
             return this.data.getLength();  // 'data' and 'getLength' are checked
         }
     });
     
    ```
    
*   **Custom Classes via defineClass()**: When using TypeScript with ES module files (files containing `import` or `export`), you must declare custom classes for TypeScript after calling [isc.defineClass](../classes/isc.md#staticmethod-iscdefineclass). Use `declare global` to augment the isc namespace:
    ```
     isc.defineClass("MyListGrid", "ListGrid").addProperties({
         headerHeight: 40
     });
     declare global { namespace isc { const MyListGrid: typeof isc.ListGrid; } }
     
    ```
    To add custom properties, extend the parent's interface:
    ```
     isc.defineClass("MyListGrid", "ListGrid").addProperties({
         customProp: "default"
     });
     declare global {
         namespace isc {
             interface MyListGridProps extends ListGridProps { customProp?: string; }
             const MyListGrid: ListGridStatic & {
                 create(props?: Partial<MyListGridProps>): ListGrid & MyListGridProps;
             };
         }
     }
     
    ```
    For classes with classMethods (static methods), declare them on the const:
    ```
     declare global {
         namespace isc {
             const MyClass: typeof isc.ListGrid & {
                 myClassMethod(): void;
             };
         }
     }
     
    ```
    
*   **Anonymous Classes / Custom Instance Methods**: SmartClient instances behave like Java "anonymous classes": you can add custom properties, add custom methods, and even call [Super()](../classes/Class.md#method-classsuper) from custom methods, all without formally defining a new class via [isc.defineClass](../classes/isc.md#staticmethod-iscdefineclass).  
      
    To use this idiomatic pattern and retain full TypeScript type checking, declare an interface that extends the parent class and includes your custom methods, then pass the configuration as the second (unchecked) parameter to `create()` and use a type assertion on the result:
    ```
     // Declare the extended interface with custom methods
     interface SalesDataGrid extends isc.ListGrid {
         lastChart: isc.FacetChart;
         updateChart(chartType?: string): void;
     }
    
     // Pass config as second (unchecked) param, cast result to extended interface
     const salesDataGrid = isc.ListGrid.create(null, {
         updateChart: function(chartType) {
             if (this.lastChart) this.lastChart.destroy();
             this.lastChart = this.chartData("product");
         }
     }) as SalesDataGrid;
    
     // Now TypeScript knows about the custom methods
     salesDataGrid.updateChart();  // OK - no error
     
    ```
    See the *Grid as Chart Data Source* sample for a complete example.

---
