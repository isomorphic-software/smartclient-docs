# Registering Classes for Reflection

[← Back to API Index](../main.md)

---

## KB Topic: Registering Classes for Reflection

### Description
In order to specify a SmartGWT class as a constructor in [Component XML](componentXML.md#kb-topic-component-xml) or [Component Schema](componentSchema.md#kb-topic-component-schema), or for other purposes, such as for {@link com.smartgwt.client.docs.AutoChildUsage autoChildren} or for {@link com.smartgwt.client.data.DataSourceField#setEditorType(Class)}, you must first register the class with the {@link com.smartgwt.client.bean.BeanFactory} reflection mechanism.

If you want to register {@link com.smartgwt.client.widgets.Canvas} and all its subclasses found in the classpath (including your custom subclasses), you can use the {@link com.smartgwt.client.bean.BeanFactory.CanvasMetaFactory} interface to do this automatically:

> ```
>  GWT.create(BeanFactory.CanvasMetaFactory.class);
> ```

Similarly, to register {@link com.smartgwt.client.widgets.form.fields.FormItem} and all its subclasses found in the classpath (including your custom subclasses), you can use the {@link com.smartgwt.client.bean.BeanFactory.FormItemMetaFactory}.

> ```
>  GWT.create(BeanFactory.FormItemMetaFactory.class);
> ```

Alternatively, if only specific classes need to be instantiated and configured dynamically, you can register just those classes by annotating them with the {@link com.smartgwt.client.bean.BeanFactory.Generate} annotation instead. For instance:

> ```
>  {@literal @}BeanFactory.Generate
>  public class MyCanvas extends Canvas {
>      ...
>  }
> ```

For framework classes (where you cannot annotate the class directly), you can supply an array of Class literals to the annotation. For instance:

> ```
>  {@literal @}BeanFactory.Generate({Canvas.class, TreeGrid.class})
>  public interface EmptyInterface {
>      ...
>  }
> ```

When you supply an array of class literals, the class you annotate (here `EmptyInterface`) will **not** itself have a BeanFactory generated for it. Thus, you can use an empty inner interface for this purpose.

If there are only a limited number of classes which require dynamic configuration, it will save code size to use the {@link com.smartgwt.client.bean.BeanFactory.Generate} annotation to generate factories for those specific types, rather than using {@link com.smartgwt.client.bean.BeanFactory.CanvasMetaFactory} or {@link com.smartgwt.client.bean.BeanFactory.FormItemMetaFactory}. Once a factory is generated for a class, GWT's opportunities to prune dead code are more limited for that class, since it cannot know what properties will be set or retrieved at run-time.

---
