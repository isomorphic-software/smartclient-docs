# UploadItem Documentation

[← Back to API Index](../main.md)

---

## Class: UploadItem

*Inherits from:* [TextItem](TextItem.md#class-textitem)

### Description
FormItem that creates an HTML `<input type="file">` control, with an interface that allows a user to pick a file from his machine to upload to the server.

**NOTE:** use [FileItem](FileItem.md#class-fileitem), **not** UploadItem, if you are using the SmartClient Server framework. FileItem is much easier to use and addresses all the limitations of UploadItem discussed below. See the [Uploading Files](../kb_topics/upload.md#kb-topic-uploading-files) overview for details.

If a form containing an UploadItem is [redrawn](Canvas.md#method-canvasredraw) (which may happen if other form items are shown or hidden, the form is [resized](Canvas.md#attr-canvasredrawonresize), or this or other items show validation errors) then the value in the upload item is lost (because an HTML upload field may not be created with a value). For this reason, if you are building a form that combines an UploadItem with other FormItems that could trigger redraw()s, recommended practice is to place each UploadItem in a distinct DynamicForm instance and create the visual appearance of a single logical form via combining the DynamicForms in a [Layout](Layout.md#class-layout). For the same reason, do not apply [validators](Validator.md#class-validator) to UploadItems: if such a validator fails, it will cause the form to be redrawn and the UploadItem's value to be lost.

**NOTE: Browser-specific behaviors:**

*   while getDisplayValue() can be used to retrieve the filesystem path of the uploaded file on some browsers, different browsers will return either just the file name without path or the full path. It is plausible that some browsers may switch behavior in the future to not supply this value at all. Do not rely on this value.
*   the appearance of the UploadItem is not consistent across browsers and we do not recommend trying to make it consistent or trying to apply styling to the upload control at all. It is a potential security problem if an end user is unable to reliably recognize the upload control, hence, all browsers limit what styling can be applied. Various hacks exists to get further control of styling, but it is likely these hacks will be broken by browser upgrades in the future.

### Groups

- upload

---
## Attr: UploadItem.textBoxStyle

### Description
Base CSS class name for this `UploadItem`'s native file input element.

Note that the customization via CSS of a native file input element allowable by the browser varies widely; in some browsers on certain platforms, it may be possible to customize certain CSS properties, but not in others; or, it may be that the CSS property (e.g. border) is applied differently in some browsers.

If the textBoxStyle is changed at runtime, [FormItem.updateState](FormItem.md#method-formitemupdatestate) must be called to update the visual state. However, calling updateState() will clear any file selected by the user to be uploaded.

### Groups

- formItemStyling

### See Also

- [FormItem.cellStyle](FormItem.md#attr-formitemcellstyle)

**Flags**: IRW

---
## Attr: UploadItem.capture

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
## Attr: UploadItem.editProxyConstructor

### Description
Default class used to construct the [EditProxy](EditProxy.md#class-editproxy) for this component when the component is [first placed into edit mode](Canvas.md#method-canvasseteditmode).

**Flags**: IR

---
## Attr: UploadItem.height

### Description
Height for this uploadItem. Note that SmartClient will not apply this size to the native HTML `<input ...>` element written out by this formItem as this leads to inconsistent appearance across different browsers. The specified height acts as a minimum cell width for the item.

**Flags**: IRW

---
## Attr: UploadItem.width

### Description
Width for this uploadItem. Note that SmartClient will not apply this size to the native HTML `<input ...>` element written out by this formItem as this leads to inconsistent appearance across different browsers. The specified width acts as a minimum cell width for the item.

**Flags**: IRW

---
## Attr: UploadItem.multiple

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
## Attr: UploadItem.accept

### Description
A comma-separated list of valid MIME types, used as a filter for the file picker window.

Note that this property makes use of the HTML `accept` attribute, and so relies on the browser to perform the desired filtering. For further study, see:

*   [HTML `<input>` accept Attribute](https://www.w3schools.com/TAGS/att_input_accept.asp)
*   [The Input (Form Input) element](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/Input)
*   [File input 'accept' attribute - is it useful?](https://stackoverflow.com/questions/181214/file-input-accept-attribute-is-it-useful)

**Flags**: IR

---
## Method: UploadItem.setSelectionRange

### Description
**This method is not supported** by `UploadItem`.

---
## Method: UploadItem.selectValue

### Description
**This method is not supported** by `UploadItem`.

---
## Method: UploadItem.setValue

### Description
Attempting to set the value for an upload form item is disallowed for security reasons. Therefore this method will just log a warning, and not modify the value of the item.

---
## Method: UploadItem.deselectValue

### Description
**This method is not supported** by `UploadItem`.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| start | [Boolean](#type-boolean) | true | — | By default the text insertion cursor will be moved to the end of the current value - pass in this parameter to move to the start instead |

---
## Method: UploadItem.getSelectionRange

### Description
**This method is not supported** by `UploadItem`.

### Returns

`[Array of int](#type-array-of-int)` — `null`

---
