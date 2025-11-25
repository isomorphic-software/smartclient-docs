# Integration with Titanium

[← Back to API Index](../main.md)

---

## KB Topic: Integration with Titanium

### Description
Titanium provides an extensive Javascript API to access a native device's UI, phone, camera, geolocation, etc. Documentation, getting started, programming guides are [here](http://developer.appcelerator.com/documentation). Titanium provides a consistent API across devices including the ability to mix webviews with native controls.

The Titanium sample application provides an example of accessing a device's Contacts db using SmartClient. The application presents 2 tabs 'Customers' and 'Contacts' and allows the user to import Customer contacts into his/her contacts db resident on the device. Selecting a Customer's Contact address will show a map of the contact. Selecting a Customer's phone number will call the customer or prompt to import the contact into the user's contacts. The latter option is default behavior on the iPad. Calling the customer contact is default behavior for devices such as the iPhone or Android.

The Titanium Contact object holds the following properties:

*   URL
*   address
*   birthday
*   created
*   date
*   department
*   email
*   firstName
*   firstPhonetic
*   fullName
*   image
*   instantMessage
*   jobTitle
*   kind
*   lastName
*   lastPhonetic
*   middleName
*   middlePhonetic
*   modified
*   nickname
*   note
*   organization
*   phone
*   prefix
*   relatedNames
*   suffix

The following Titanium API's are used:

*   Titanium.App.addEventListener
*   Titanium.App.fireEvent
*   Titanium.Contacts.getAllPeople
*   Titanium.Geolocation.forwardGeocoder
*   Titanium.Map.STANDARD\_TYPE,
*   Titanium.Map.createView
*   Titanium.UI.createTab
*   Titanium.UI.createTabGroup
*   Titanium.UI.createWebView
*   Titanium.UI.createWindow
*   Titanium.UI.setBackgroundColor

The following SmartClient Components are used

*   isc.DataSource
*   isc.ListGrid

The following SmartClient Resources are bundled in the Titanium application

*   ISC\_Containers.js
*   ISC\_Core.js
*   ISC\_DataBinding.js
*   ISC\_Foundation.js
*   ISC\_Grids.js
*   load\_skin.js
*   skins/Mobile/images/black.gif
*   skins/Mobile/images/blank.gif
*   skins/Mobile/images/checked.png
*   skins/Mobile/images/formula\_menuItem.png
*   skins/Mobile/images/grid.gif
*   skins/Mobile/images/group\_closed.gif
*   skins/Mobile/images/group\_opened.gif
*   skins/Mobile/images/headerMenuButton\_icon.gif
*   skins/Mobile/images/loading.gif
*   skins/Mobile/images/loadingSmall.gif
*   skins/Mobile/images/opacity.png
*   skins/Mobile/images/pinstripes.png
*   skins/Mobile/images/row\_collapsed.gif
*   skins/Mobile/images/row\_expanded.gif
*   skins/Mobile/images/sort\_ascending.gif
*   skins/Mobile/images/sort\_descending.gif
*   skins/Mobile/skin\_styles.css

---
