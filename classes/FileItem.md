# FileItem Documentation

[← Back to API Index](../reference.md)

---

## Class: FileItem

*Inherits from:* [CanvasItem](CanvasItem.md#class-canvasitem)

### Description
Binary data interface for use in DynamicForms. Allows users to select a single file for upload. In read-only mode (canEdit:false), can display the contents of "imageFile" fields.

**Editable mode**

The [FileItem.editForm](#attr-fileitemeditform) will be automatically generated and displayed as [this.canvas](CanvasItem.md#attr-canvasitemcanvas), allowing the user to select file(s) to upload.

See the [Upload Overview](../kb_topics/upload.md#kb-topic-uploading-files) for information on using this control.

**Read-only mode**

For fields of type `"binary"` the raw data value will be displayed in the generated [FileItem.displayForm](#attr-fileitemdisplayform).

For other fields, the [FileItem.displayCanvas](#attr-fileitemdisplaycanvas) will be displayed.

For `"imageFile"` fields with [showFileInline](#attr-fileitemshowfileinline) set to true, the image-file will be streamed and displayed inline within the displayCanvas.

Otherwise, the displayCanvas will render out [View](#attr-fileitemviewiconsrc) and [Download](#attr-fileitemdownloadiconsrc) icons and the fileName.

### Groups

- upload

---
## Attr: FileItem.uploadItem

### Description
The [UploadItem](UploadItem.md#class-uploaditem) created automatically and displayed in the [FileItem.editForm](#attr-fileitemeditform) when [canEdit](FormItem.md#attr-formitemcanedit) is true.

This component is an [AutoChild](../reference.md#type-autochild) and as such may be customized via `fileItem.uploadItemDefaults` and `fileItem.uploadItemProperties`.

### Groups

- upload

**Flags**: RA

---
## Attr: FileItem.editForm

### Description
The [DynamicForm](DynamicForm.md#class-dynamicform) created automatically when [canEdit](FormItem.md#attr-formitemcanedit) is true. Displays a single [item](#attr-fileitemuploaditem) for manipulating a file.

This component is an [AutoChild](../reference.md#type-autochild) and as such may be customized via `fileItem.editFormDefaults` and `fileItem.editFormProperties`.

### Groups

- upload

**Flags**: RA

---
## Attr: FileItem.shouldSaveValue

### Description
Should this item's value be saved in the form's values and hence returned from [form.getValues()](DynamicForm.md#method-dynamicformgetvalues)?

`shouldSaveValue:false` is used to mark formItems which do not correspond to the underlying data model and should not save a value into the form's [values](DynamicForm.md#attr-dynamicformvalues). Example includes visual separators, password re-type fields, or checkboxes used to show/hide other form items.

A `shouldSaveValue:false` item should be given a value either via [FormItem.defaultValue](FormItem.md#attr-formitemdefaultvalue) or by calling [form.setValue(item, value)](DynamicForm.md#method-dynamicformsetvalue) or [formItem.setValue(value)](FormItem.md#method-formitemsetvalue). Providing a value via [form.values](DynamicForm.md#attr-dynamicformvalues) or [form.setValues()](DynamicForm.md#method-dynamicformsetvalues) will automatically switch the item to `shouldSaveValue:true`.

Note that

*   if an item is shouldSaveValue true, but has no name, a warning is logged, and shouldSaveValue will be set to false.

### Groups

- formValues

**Flags**: IR

---
## Attr: FileItem.capture

### Description
This attribute enables camera capture functionality for mobile devices, accepting the following values:

*   Set it to "user" to capture using the front-facing camera.
*   Set it to "environment" to capture using the rear-facing camera.

Please note that in the latest versions of Android and iOS, utilizing this attribute will consistently load the rear camera. This behavior is due to the direct camera software's ability to switch between the two cameras seamlessly.

When working with the capture functionality of iPhones and Android devices, it's important to consider the supported DataSourceField.mimeTypes for audio, video, and image files that can be used with the fileItem.accept attribute. Here's a list of commonly supported mime types for capturing on these devices:

Supported Image Mime Types:

*   image/jpeg: JPEG image format (.jpg, .jpeg)
*   image/png: Portable Network Graphics format (.png)

Supported Audio Mime Types:

*   audio/3gpp: 3GPP format, commonly used for audio capture.
*   audio/mp4: MP4 format, widely supported for audio capture.

Supported Video Mime Types:

*   video/3gpp: 3GPP format, commonly used for video capture.
*   video/mp4: MP4 format, widely supported for video capture.

**Behavior Based on 'accept' Attribute**

The behavior of using the capture attribute depends on the value used in the accept attribute. For example:

*   _accept="image/\*"_ will load the camera ready to take pictures.
*   _accept="audio/\*"_ will load the default audio recorder, not the camera.
*   _accept="video/\*"_ will load the camera in video mode, ready to capture videos.

Please note that the SmartClient framework does not control the native device behavior beyond these attribute settings.

Lastly, keep in mind that these settings have no effect on desktop browsers; they apply exclusively to mobile devices.

This information is "circa 2023" and may not apply to all devices.

**Flags**: IR

---
## Attr: FileItem.displayItem

### Description
The [StaticTextItem](StaticTextItem.md#class-statictextitem) created automatically and displayed in the [FileItem.displayForm](#attr-fileitemdisplayform) when [canEdit](FormItem.md#attr-formitemcanedit) is false and the field type is "binary".

This component is an [AutoChild](../reference.md#type-autochild) and as such may be customized via `fileItem.displayItemDefaults` and `fileItem.displayItemProperties`.

### Groups

- upload

**Flags**: RA

---
## Attr: FileItem.viewIconSrc

### Description
Returns the name of the icon to use for the view functionality.

### Groups

- images

**Flags**: IR

---
## Attr: FileItem.accept

### Description
A comma-separated list of valid MIME types, used as a filter for the file picker window.

Note that this property makes use of the HTML `accept` attribute, and so relies on the browser to perform the desired filtering. For further study, see:

*   [HTML `<input>` accept Attribute](https://www.w3schools.com/TAGS/att_input_accept.asp)
*   [The Input (Form Input) element](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/Input)
*   [File input 'accept' attribute - is it useful?](https://stackoverflow.com/questions/181214/file-input-accept-attribute-is-it-useful)

**Flags**: IR

---
## Attr: FileItem.editProxyConstructor

### Description
Default class used to construct the [EditProxy](EditProxy.md#class-editproxy) for this component when the component is [first placed into edit mode](Canvas.md#method-canvasseteditmode).

**Flags**: IR

---
## Attr: FileItem.downloadIconSrc

### Description
Returns the name of the icon to use for the download functionality.

### Groups

- images

**Flags**: IR

---
## Attr: FileItem.displayCanvas

### Description
The [Canvas](Canvas.md#class-canvas) created automatically when [canEdit](FormItem.md#attr-formitemcanedit) is false and the field is of any type other than "binary".

If the field is of type "imageFile", and [showFileInline](#attr-fileitemshowfileinline) is true, the contents of the canvas are set to HTML that streams the image file for display. Otherwise, the item renders icons that allow the file to be [viewed](#attr-fileitemviewiconsrc) or [downloaded](#attr-fileitemdownloadiconsrc).

This component is an [AutoChild](../reference.md#type-autochild) and as such may be customized via `fileItem.displayCanvasDefaults` and `fileItem.displayCanvasProperties`.

### Groups

- upload

**Flags**: RA

---
## Attr: FileItem.showFileInline

### Description
Indicates whether to stream the image and display it inline or to display the View and Download icons.

**Flags**: IR

---
## Attr: FileItem.multiple

### Description
When true, allow the file-selection dialog shelled by the browser to select multiple files.

Support is not full-cycle at the server - that is, there are server APIs for retrieving each file that was uploaded, but no built-in support for storing multiple files against a single DataSource field. However, you can write custom server DMI code to do something with the files - for instance, you could create multiple new DataSource records for each file via a server DMI like this below:

```
    String fileNameStr = (String)dsRequest.getValues().get("image_filename").toString();

    String[] fileNames = fileNameStr.split(", ");
    List files = dsRequest.getUploadedFiles();

    for (int i = 0; i < files.size(); i++) {
        ISCFileItem file = (ISCFileItem)files.get(i);
        InputStream fileData = file.getInputStream();
        DSRequest inner = new DSRequest("mediaLibrary", "add");
        Map values = new HashMap();
        values.put("title", dsRequest.getValues().get("title"));
        values.put("image", fileData);
        values.put("image_filename", fileNames[i]);
        values.put("image_filesize", file.getSize());
        values.put("image_date_created", new Date());
        
        inner.setValues(values);
        inner.execute();
    }
    
    DSResponse dsResponse = new DSResponse();
    
    dsResponse.setStatus(0);

    return dsResponse;
 
```

**Flags**: IR

---
## Attr: FileItem.displayForm

### Description
The [DynamicForm](DynamicForm.md#class-dynamicform) created automatically when [canEdit](FormItem.md#attr-formitemcanedit) is false and the field is of type "binary". Displays a single [item](#attr-fileitemdisplayitem) for viewing the content of a binary file.

This component is an [AutoChild](../reference.md#type-autochild) and as such may be customized via `fileItem.displayFormDefaults` and `fileItem.displayFormProperties`.

### Groups

- upload

**Flags**: RA

---
## Method: FileItem.setMultiple

### Description
Updates the [FileItem.multiple](#attr-fileitemmultiple) setting at runtime, propagating it to the Browser's file dialog. Causes a redraw.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| multiple | [boolean](../reference.md#type-boolean) | false | — | the HTML of the view link |

---
