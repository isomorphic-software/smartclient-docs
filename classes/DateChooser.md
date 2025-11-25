# DateChooser Documentation

[← Back to API Index](../main.md)

---

## Class: DateChooser

*Inherits from:* [VLayout](../main.md#class-vlayout)

### Description
Simple interactive calendar interface used to pick a date. Used by the [DateItem](DateItem.md#class-dateitem) class.

---
## Attr: DateChooser.navigationButtonHeight

### Description
Height of buttons in the [navigation area](#attr-datechoosernavigationlayout), used for navigating the [calendar view](#attr-datechooserdategrid). If unset, the default, buttons are sized by settings applied by the current skin.

If this attribute is set to a value greater than [DateChooser.navigationLayoutHeight](#attr-datechoosernavigationlayoutheight), it will cause the layout to expand to match the button height.

**Flags**: IR

---
## Attr: DateChooser.baseWeekdayStyle

### Description
Base CSS style applied to weekdays. Will have "Over", "Selected" and "Down" suffix appended as the user interacts with buttons. Defaults to [DateChooser.baseButtonStyle](#attr-datechooserbasebuttonstyle).

See [cellStyleSuffixes](../kb_topics/cellStyleSuffixes.md#kb-topic-cellstylesuffixes) for details on how stateful suffixes are combined with the base style to generate stateful cell styles in Grids.

**Flags**: IRW

---
## Attr: DateChooser.previousYearButton

### Description
A button shown in the [navigation layout](#attr-datechoosernavigationlayout) that shifts the calendar view backward by a year.

**Flags**: IR

---
## Attr: DateChooser.yearMenuStyle

### Description
Style for the pop-up year menu.

**Flags**: IR

---
## Attr: DateChooser.headerStyle

### Description
CSS style applied to the day-of-week headers. By default this applies to all days of the week. To apply a separate style to weekend headers, set [DateChooser.weekendHeaderStyle](#attr-datechooserweekendheaderstyle)

**Flags**: IRW

---
## Attr: DateChooser.baseWeekStyle

### Description
Base CSS style applied to cells in the [fiscal week column](#attr-datechoosershowweekchooser).

**Flags**: IRW

---
## Attr: DateChooser.showDoubleYearIcon

### Description
If this property is set to true the previous and next year buttons will render out the previous and next month button icons twice rather than using the [DateChooser.prevYearIcon](#attr-datechooserprevyearicon) and [DateChooser.nextYearIcon](#attr-datechoosernextyearicon).

Set to `true` by default as not all skins contain media for the year icons.

**Flags**: IRW

---
## Attr: DateChooser.prevMonthIcon

### Description
Icon for the previous month button

**Flags**: IR

---
## Attr: DateChooser.timeItem

### Description
[TimeItem](TimeItem.md#class-timeitem) for editing the time portion of dates. Visible by default for fields of type "datetime" and can be controlled by setting [DateChooser.showTimeItem](#attr-datechoosershowtimeitem).

**Flags**: R

---
## Attr: DateChooser.weekHeaderStyle

### Description
Base CSS style applied to the header of the [fiscal or calendar week column](#attr-datechoosershowweekchooser) in the [calendar view](#attr-datechooserdategrid).

**Flags**: IRW

---
## Attr: DateChooser.previousMonthButton

### Description
A button shown in the [navigation layout](#attr-datechoosernavigationlayout) that shifts the calendar view backward by a month.

**Flags**: IR

---
## Attr: DateChooser.headerHeight

### Description
Height of the header area (containing the navigation buttons) in pixels.

**Deprecated**

**Flags**: IR

---
## Attr: DateChooser.baseNavButtonStyle

### Description
CSS style to apply to navigation buttons and date display at the top of the component. If null, the CSS style specified in [DateChooser.baseButtonStyle](#attr-datechooserbasebuttonstyle) is used.

**Flags**: IRW

---
## Attr: DateChooser.endDate

### Description
Limits the selectable range of this DateChooser.

If unset, the chooser's range-end is dictated by [endYear](#attr-datechooserendyear).

### Groups

- appearance

**Flags**: IRW

---
## Attr: DateChooser.showTodayButton

### Description
Determines whether the "Today" button will be displayed, allowing the user to select the current date.

**Flags**: IRW

---
## Attr: DateChooser.alternateWeekStyles

### Description
Whether alternating weeks should be drawn in alternating styles. If enabled, the cell style for alternate rows will have [DateChooser.alternateStyleSuffix](#attr-datechooseralternatestylesuffix) appended to it.

**Flags**: IRW

---
## Attr: DateChooser.nextMonthIconRTL

### Description
Icon for the next month button

**Flags**: IRW

---
## Attr: DateChooser.weekFieldTitle

### Description
Title for the [week](#attr-datechoosershowweekchooser) field in the date grid.

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: DateChooser.timeItemProperties

### Description
Custom properties to apply to the [time field](#attr-datechoosertimeitem) used for editing the time portion of the date.

**Flags**: IRA

---
## Attr: DateChooser.fiscalYearChooserButton

### Description
A button shown in the [navigation layout](#attr-datechoosernavigationlayout) which, when clicked, shows a picker for selecting a specific fiscal year.

**Flags**: IR

---
## Attr: DateChooser.baseWeekendStyle

### Description
Base CSS style applied to weekends. Will have "Over", "Selected" and "Down" suffix appended as the user interacts with buttons. Defaults to [DateChooser.baseWeekdayStyle](#attr-datechooserbaseweekdaystyle).

See [cellStyleSuffixes](../kb_topics/cellStyleSuffixes.md#kb-topic-cellstylesuffixes) for details on how stateful suffixes are combined with the base style to generate stateful cell styles in Grids.

**Flags**: IRW

---
## Attr: DateChooser.baseButtonStyle

### Description
Base CSS style applied to this picker's buttons. Will have "Over", "Selected" and "Down" suffix appended as the user interacts with buttons.

See [cellStyleSuffixes](../kb_topics/cellStyleSuffixes.md#kb-topic-cellstylesuffixes) for details on how stateful suffixes are combined with the base style to generate stateful cell styles in Grids.

**Flags**: IRW

---
## Attr: DateChooser.nextMonthIconHeight

### Description
Height of the icon for the next month button

**Flags**: IRW

---
## Attr: DateChooser.weekendDays

### Description
An array of integer day-numbers that should be considered to be weekend days by this DateChooser instance. If unset, defaults to the set of days indicated [globally](DateUtil.md#classattr-dateutilweekenddays).

### Groups

- visibility

**Flags**: IRW

---
## Attr: DateChooser.prevYearIconRTL

### Description
Icon for the previous year button if [Page.isRTL](Page.md#classmethod-pageisrtl) is true. If not set, and the page is in RTL mode, the [DateChooser.nextYearIcon](#attr-datechoosernextyearicon) will be used in place of the [DateChooser.prevYearIcon](#attr-datechooserprevyearicon) and vice versa.

### See Also

- [DateChooser.showDoubleYearIcon](#attr-datechoosershowdoubleyearicon)

**Flags**: IRW

---
## Attr: DateChooser.dayNameLength

### Description
How long (how many characters) should be day names be. May be 1, 2 or 3 characters.

**Flags**: IR

---
## Attr: DateChooser.nextYearIconWidth

### Description
Width of the icon for the next year button

**Flags**: IR

---
## Attr: DateChooser.disabledWeekdayStyle

### Description
Base CSS style applied to weekday dates which have been [disabled](#attr-datechooserdisableddates).

**Flags**: IRW

---
## Attr: DateChooser.todayButtonTitle

### Description
Title for "Today" button.

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: DateChooser.buttonLayout

### Description
An [AutoChild](../main.md#type-autochild) [HLayout](../main.md#class-hlayout), rendered below the [date grid](../main.md#class-dategrid), and showing the [Today](#attr-datechoosertodaybutton), [Cancel](#attr-datechoosercancelbutton) and, when working with "datetime" values, [Apply](#attr-datechooserapplybutton) buttons.

**Flags**: IR

---
## Attr: DateChooser.showApplyButton

### Description
Determines whether the [DateChooser.applyButton](#attr-datechooserapplybutton) will be displayed.

**Flags**: IRW

---
## Attr: DateChooser.skinImgDir

### Description
Overridden directory where images for this widget (such as the month and year button icons) may be found.

**Flags**: IRWA

---
## Attr: DateChooser.dateGrid

### Description
A [ListGrid](ListGrid_1.md#class-listgrid) subclass, responsible for rendering the calendar view.

**Flags**: IR

---
## Attr: DateChooser.menuItemStyle

### Description
Base CSS style applied to cells in the Year, Week and Month popup-menus. In some skins, this attribute is set to _dateChooserMenuItem_ which provides custom styles for items in these menus.

**Flags**: IRW

---
## Attr: DateChooser.showCancelButton

### Description
Determines whether the "Cancel" button will be displayed.

**Flags**: IRW

---
## Attr: DateChooser.showTimeItem

### Description
Whether to show the [time field](#attr-datechoosertimeitem) for editing the time portion of the date. When unset, the time field is shown automatically if the field type is "datetime". Note that the item's [second chooser](#attr-datechoosershowseconditem) is not shown by default.

**Flags**: IRW

---
## Attr: DateChooser.navigationLayoutHeight

### Description
Height of the [navigation area](#attr-datechoosernavigationlayout), containing the various buttons for navigating the [calendar view](#attr-datechooserdategrid).

If [DateChooser.navigationButtonHeight](#attr-datechoosernavigationbuttonheight) or the navigation buttons themselves specify a height taller than _navigationLayoutHeight_, this setting acts as a minimum height and the layout will expand to fit the buttons.

**Flags**: IR

---
## Attr: DateChooser.previousMonthButtonAriaLabel

### Description
[Aria label](StatefulCanvas.md#attr-statefulcanvasarialabel) for the [DateChooser.previousMonthButton](#attr-datechooserpreviousmonthbutton).

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: DateChooser.prevMonthIconRTL

### Description
Icon for the previous month button if [Page.isRTL](Page.md#classmethod-pageisrtl) is true. If not set, and the page is in RTL mode, the [DateChooser.nextMonthIcon](#attr-datechoosernextmonthicon) will be used in place of the [DateChooser.prevMonthIcon](#attr-datechooserprevmonthicon) and vice versa.

**Flags**: IR

---
## Attr: DateChooser.nextYearIconHeight

### Description
Height of the icon for the next year button

**Flags**: IRW

---
## Attr: DateChooser.endYear

### Description
Latest year that may be selected.

If set to null, no minimum year is enforced.

If this chooser was opened by a [DateItem](DateItem.md#class-dateitem), the default is inherited from [DateItem.endDate](DateItem.md#attr-dateitemenddate). Otherwise, the default is 5 years after today.

When opened from a [RelativeDateItem](RelativeDateItem.md#class-relativedateitem), this property and [DateChooser.startYear](#attr-datechooserstartyear) are defaulted to null, and the year-picker shows years surrounding the current year, according to [startYearRange](#attr-datechooserstartyearrange) and [endYearRange](#attr-datechooserendyearrange).

**Flags**: IR

---
## Attr: DateChooser.nextYearIconRTL

### Description
Icon for the next year button if [Page.isRTL](Page.md#classmethod-pageisrtl) is true. If not set, and the page is in RTL mode, the [DateChooser.nextYearIcon](#attr-datechoosernextyearicon) will be used in place of the [DateChooser.prevYearIcon](#attr-datechooserprevyearicon) and vice versa.

### See Also

- [DateChooser.showDoubleYearIcon](#attr-datechoosershowdoubleyearicon)

**Flags**: IR

---
## Attr: DateChooser.showFiscalYearChooser

### Description
When set to true, show a button that allows the calendar to be navigated by fiscal year.

**Flags**: IRW

---
## Attr: DateChooser.showWeekChooser

### Description
When set to true, show a button that allows the calendar to be navigated by week or fiscal week, depending on the value of [DateChooser.showFiscalYearChooser](#attr-datechoosershowfiscalyearchooser).

**Flags**: IRW

---
## Attr: DateChooser.baseBottomButtonStyle

### Description
CSS style to apply to the buttons at the bottom of the DateChooser ("Today" and "Cancel"). If null, the CSS style specified in [DateChooser.baseButtonStyle](#attr-datechooserbasebuttonstyle) is used.

**Flags**: IRW

---
## Attr: DateChooser.prevYearIcon

### Description
Icon for the previous year button

### See Also

- [DateChooser.showDoubleYearIcon](#attr-datechoosershowdoubleyearicon)

**Flags**: IR

---
## Attr: DateChooser.applyButton

### Description
When a DateChooser is configured for [a "datetime" value](#attr-datechoosertimeitem), clicking on a date cell in the [grid](#attr-datechooserdategrid) will not automatically dismiss the DateChooser canvas. In this case, use the `Apply` button to accept the selected date and time and dismiss the chooser.

**Flags**: IR

---
## Attr: DateChooser.startDate

### Description
Limits the selectable range of this DateChooser.

If unset, the chooser's range-start is dictated by [startYear](#attr-datechooserstartyear).

### Groups

- appearance

**Flags**: IRW

---
## Attr: DateChooser.cancelButton

### Description
A button shown below the [calendar grid](../main.md#class-dategrid) which, when clicked, closes the DateChooser without selecting a value.

**Flags**: IR

---
## Attr: DateChooser.cancelButtonTitle

### Description
Title for the cancellation button.

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: DateChooser.fiscalYearFieldTitle

### Description
Title for the [fiscal year](#attr-datechoosershowfiscalyearchooser) field in the date grid.

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: DateChooser.prevMonthIconHeight

### Description
Height of the icon for the previous month button

**Flags**: IR

---
## Attr: DateChooser.navigationLayout

### Description
An [AutoChild](../main.md#type-autochild) [HLayout](../main.md#class-hlayout), rendered above the [date grid](../main.md#class-dategrid), and showing a number of widgets for navigating the DateChooser. These include buttons for moving to the previous [year](#attr-datechooserpreviousyearbutton) or [month](#attr-datechooserpreviousmonthbutton), the next [year](#attr-datechoosernextyearbutton) or [month](#attr-datechoosernextmonthbutton), and for selecting a specific [year](#attr-datechooseryearchooserbutton), [month](#attr-datechoosermonthchooserbutton) or [week](#attr-datechooserweekchooserbutton).

**Flags**: IR

---
## Attr: DateChooser.startYear

### Description
Earliest year that may be selected.

If set to null, no minimum year is enforced.

If this chooser was opened by a [DateItem](DateItem.md#class-dateitem), the default is inherited from [DateItem.startDate](DateItem.md#attr-dateitemstartdate). Otherwise, the default is 10 years before today.

When opened from a [RelativeDateItem](RelativeDateItem.md#class-relativedateitem), this property and [DateChooser.endYear](#attr-datechooserendyear) are defaulted to null, and the year-picker shows years surrounding the current year, according to [startYearRange](#attr-datechooserstartyearrange) and [endYearRange](#attr-datechooserendyearrange).

**Flags**: IR

---
## Attr: DateChooser.previousYearButtonAriaLabel

### Description
[Aria label](StatefulCanvas.md#attr-statefulcanvasarialabel) for the [DateChooser.previousYearButton](#attr-datechooserpreviousyearbutton).

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: DateChooser.startYearRange

### Description
When [startYear](#attr-datechooserstartyear) is unset, this is the years before today that will be available for selection in the year menu.

**Flags**: IR

---
## Attr: DateChooser.disabledWeekendStyle

### Description
Base CSS style applied to weekend dates which have been [disabled](#attr-datechooserdisableddates).

**Flags**: IRW

---
## Attr: DateChooser.weekChooserButton

### Description
A button shown in the [navigation layout](#attr-datechoosernavigationlayout) which shows a picker for selecting a specific week of the year. When [DateChooser.showFiscalYearChooser](#attr-datechoosershowfiscalyearchooser) is true, the week number represents a fiscal week number, one offset from the start of the fiscal year. Otherwise, it represents a week number offset from the start of the calendar year.

**Flags**: IR

---
## Attr: DateChooser.disabledDates

### Description
An array of Date instances that should be disabled if they appear in the calendar view.

**Flags**: IRW

---
## Attr: DateChooser.yearChooserButton

### Description
A button shown in the [navigation layout](#attr-datechoosernavigationlayout) that shows a picker for selecting a specific calendar year.

**Flags**: IR

---
## Attr: DateChooser.nextMonthButtonAriaLabel

### Description
[Aria label](StatefulCanvas.md#attr-statefulcanvasarialabel) for the [DateChooser.nextMonthButton](#attr-datechoosernextmonthbutton).

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: DateChooser.endYearRange

### Description
When [endYear](#attr-datechooserendyear) is unset, this is the years after today that will be available for selection in the year menu.

**Flags**: IR

---
## Attr: DateChooser.nextMonthButton

### Description
A button shown in the [navigation layout](#attr-datechoosernavigationlayout) that shifts the calendar view forward by a month.

**Flags**: IR

---
## Attr: DateChooser.styleWeekends

### Description
Whether weekend days should be styled differently from weekdays. If false, suppresses the custom [DateChooser.baseWeekendStyle](#attr-datechooserbaseweekendstyle) and [DateChooser.weekendHeaderStyle](#attr-datechooserweekendheaderstyle), instead using the [DateChooser.baseWeekdayStyle](#attr-datechooserbaseweekdaystyle) and [DateChooser.weekendHeaderStyle](#attr-datechooserweekendheaderstyle).

**Flags**: IR

---
## Attr: DateChooser.selectedWeekStyle

### Description
CSS style applied to the Fiscal Year and Week columns for the currently selected week (the one being displayed in the [week chooser](#attr-datechoosershowweekchooser)).

**Flags**: IRW

---
## Attr: DateChooser.closeOnDateClick

### Description
When editing a "date" value, with no time portion, clicking on a date-cell selects the date and closes the DateChooser. When a [time portion](#attr-datechoosershowtimeitem) is required, however, the [apply button](#attr-datechooserapplybutton) must be clicked to close the chooser, by default.

Set this attribute to true to have the DateChooser close when a user clicks in a date-cell, even if the [timeItem](#attr-datechoosertimeitem) is showing.

**Flags**: IRW

---
## Attr: DateChooser.buttonLayoutControls

### Description
Array of members to show in the [buttonLayout](#attr-datechooserbuttonlayout).

The default value of `buttonLayoutControls` is an Array of Strings listing the standard buttons in their default order:

```
    buttonLayoutControls : ["todayButton", "cancelButton", "applyButton"]
 
```
You can override `buttonLayoutControls` to change the order of the standard buttons. You can also omit standard buttons this way, although it's more efficient to use the related "show" property if available (eg [DateChooser.showTodayButton](#attr-datechoosershowtodaybutton)).

By embedding a Canvas directly in this list you can add arbitrary additional controls to the buttonLayout.

Note that having added controls to buttonLayoutControls, you can still call APIs directly on those controls to change their appearance, and you can also show() and hide() them if they should not be shown in some circumstances.

Tip: custom controls need to set layoutAlign:"center" to appear vertically centered.

**Flags**: IR

---
## Attr: DateChooser.alternateStyleSuffix

### Description
The text appended to the style name when using [DateChooser.alternateWeekStyles](#attr-datechooseralternateweekstyles).

**Flags**: IRW

---
## Attr: DateChooser.todayButton

### Description
A button shown below the [calendar grid](../main.md#class-dategrid) which, when clicked, navigates the calendar to today.

**Flags**: IR

---
## Attr: DateChooser.todayStyle

### Description
Additional styling for today's date.

**Flags**: IR

---
## Attr: DateChooser.monthChooserButton

### Description
A button shown in the [navigation layout](#attr-datechoosernavigationlayout) that shows a picker for selecting a specific month.

**Flags**: IR

---
## Attr: DateChooser.todayButtonHeight

### Description
If set specifies a fixed height for the Today and Cancel buttons.

**Flags**: IRW

---
## Attr: DateChooser.nextYearButton

### Description
A button shown in the [navigation layout](#attr-datechoosernavigationlayout) that shifts the calendar view forward by a year.

**Flags**: IR

---
## Attr: DateChooser.weekendHeaderStyle

### Description
Optional CSS style applied to the day-of-week headers for weekend days. If unset [DateChooser.headerStyle](#attr-datechooserheaderstyle) will be applied to both weekdays and weekend days.

**Flags**: IRW

---
## Attr: DateChooser.prevYearIconHeight

### Description
Height of the icon for the previous year button

**Flags**: IR

---
## Attr: DateChooser.monthMenuStyle

### Description
Style for the pop-up year menu.

**Flags**: IR

---
## Attr: DateChooser.nextYearButtonAriaLabel

### Description
[Aria label](StatefulCanvas.md#attr-statefulcanvasarialabel) for the [DateChooser.nextYearButton](#attr-datechoosernextyearbutton).

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: DateChooser.showWeekends

### Description
Whether weekend days should be shown. Which days are considered weekends is controlled by [DateChooser.weekendDays](#attr-datechooserweekenddays) if set or by [DateUtil.weekendDays](DateUtil.md#classattr-dateutilweekenddays) otherwise.

**Flags**: IR

---
## Attr: DateChooser.prevMonthIconWidth

### Description
Width of the icon for the previous month button

**Flags**: IR

---
## Attr: DateChooser.fiscalYearHeaderStyle

### Description
Base CSS style applied to the header of the [fiscal year column](#attr-datechoosershowfiscalyearchooser) in the [calendar view](#attr-datechooserdategrid).

**Flags**: IRW

---
## Attr: DateChooser.use24HourTime

### Description
When showing the [time field](#attr-datechoosershowtimeitem), whether the [TimeItem](TimeItem.md#class-timeitem) should be set to use 24-hour time. The default is true.

**Flags**: IRW

---
## Attr: DateChooser.nextMonthIconWidth

### Description
Width of the icon for the next month button if [Page.isRTL](Page.md#classmethod-pageisrtl) is true. If not set, and the page is in RTL mode, the [DateChooser.nextMonthIcon](#attr-datechoosernextmonthicon) will be used in place of the [DateChooser.prevMonthIcon](#attr-datechooserprevmonthicon) and vice versa.

**Flags**: IRW

---
## Attr: DateChooser.showSecondItem

### Description
When showing the [time field](#attr-datechoosertimeitem), whether to show the "second" picker. When unset, the second field is not shown.

**Flags**: IRW

---
## Attr: DateChooser.nextYearIcon

### Description
Icon for the next year button

### See Also

- [DateChooser.showDoubleYearIcon](#attr-datechoosershowdoubleyearicon)

**Flags**: IR

---
## Attr: DateChooser.closeOnEscapeKeypress

### Description
Should this dateChooser be dismissed if the user presses the Escape key?

**Flags**: IR

---
## Attr: DateChooser.weekMenuStyle

### Description
Style for the pop-up week menu.

**Flags**: IR

---
## Attr: DateChooser.disableWeekends

### Description
Whether it should be valid to pick a weekend day. If set to true, weekend days appear in disabled style and cannot be picked.

Which days are considered weekends is controlled by [DateChooser.weekendDays](#attr-datechooserweekenddays) if set or by [DateUtil.weekendDays](DateUtil.md#classattr-dateutilweekenddays) otherwise.

**Flags**: IR

---
## Attr: DateChooser.navButtonConstructor

### Description
Constructor for navigation buttons at the top of the component.

**Flags**: IRA

---
## Attr: DateChooser.useFirstDayOfFiscalWeek

### Description
When showing the [fiscal year chooser](#attr-datechoosershowfiscalyearchooser), should firstDayOfWeek be defaulted to the same day as the fiscal start date? If true and a fiscal year starts on a Tuesday, the calendar will display Tuesday to Monday from left to right.

**Flags**: IRW

---
## Attr: DateChooser.applyButtonTitle

### Description
Title for the [Apply](#attr-datechooserapplybutton) button.

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: DateChooser.firstDayOfWeek

### Description
Day of the week to show in the first column. 0=Sunday, 1=Monday, ..., 6=Saturday. The default value for this attribute is picked up from the current locale and can also be altered system-wide with the [global setter](DateUtil.md#classmethod-dateutilsetfirstdayofweek).

### Groups

- i18nMessages
- appearance

**Flags**: IR

---
## Attr: DateChooser.timeItemTitle

### Description
Title for the [time field](#attr-datechoosertimeitem).

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: DateChooser.prevYearIconWidth

### Description
Width of the icon for the previous year button

**Flags**: IR

---
## Attr: DateChooser.nextMonthIcon

### Description
Icon for the next month button

**Flags**: IRW

---
## Attr: DateChooser.baseFiscalYearStyle

### Description
Base CSS style applied to cells in the [fiscal year column](#attr-datechoosershowfiscalyearchooser).

See [cellStyleSuffixes](../kb_topics/cellStyleSuffixes.md#kb-topic-cellstylesuffixes) for details on how stateful suffixes are combined with the base style to generate stateful cell styles in Grids.

**Flags**: IRW

---
## Method: DateChooser.getData

### Description
Get the current value of the picker.

See [DateChooser.dataChanged](#method-datechooserdatachanged) for how to respond to the user picking a date.

### Returns

`[Date](#type-date)` — current date

---
## Method: DateChooser.getHeaderYearTitle

### Description
Override this method to alter the year representation shown in the DateChooser's header. The default implementation returns the full four-digit Gregorian year (ie, the same value that is passed in)

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| year | [Integer](../main_2.md#type-integer) | false | — | The Gregorian year number to derive a display value for |

### Returns

`[String](#type-string)` — the value to show for the parameter year

---
## Method: DateChooser.setFiscalCalendar

### Description
Sets the [FiscalCalendar](../main.md#object-fiscalcalendar) object that will be used by this DateChooser. If unset, the [global fiscal calendar](DateUtil.md#classmethod-dateutilgetfiscalcalendar) is used.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| fiscalCalendar | [FiscalCalendar](#type-fiscalcalendar) | true | — | the fiscal calendar for this chooser |

---
## Method: DateChooser.getFiscalCalendar

### Description
Returns the [FiscalCalendar](../main.md#object-fiscalcalendar) object that will be used by this DateChooser.

### Returns

`[FiscalCalendar](#type-fiscalcalendar)` — the fiscal calendar for this chooser, if set, or the global one otherwise

---
## Method: DateChooser.dataChanged

### Description
Method to override or observe in order to be notified when a user picks a date value.

Has no default behavior (so no need to call Super).

Use [DateChooser.getData](#method-datechoosergetdata) to get the current date value.

---
## Method: DateChooser.cancelClick

### Description
Fired when the user clicks the cancel button in this date chooser. Default implementation clears the date chooser.

---
## Method: DateChooser.setData

### Description
Set the picker to show the given date.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| date | [Date](#type-date) | false | — | new value |

---
## Method: DateChooser.todayClick

### Description
Fired when the user clicks the Today button. Default implementation will select the current date in the date chooser.

---
## Method: DateChooser.getYearTitle

### Description
Override this method to alter the year representations that are shown in the DateChooser's "Select a year" dropdown. The default implementation returns the full four-digit Gregorian year (ie, the same value that is passed in)

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| year | [Integer](../main_2.md#type-integer) | false | — | The Gregorian year number to derive a display value for |

### Returns

`[String](#type-string)` — the value to show for the parameter year

---
