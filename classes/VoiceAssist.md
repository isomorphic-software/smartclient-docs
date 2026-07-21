# VoiceAssist Documentation

[← Back to API Index](../reference.md)

---

## Class: VoiceAssist

### Description
The VoiceAssist class provides voice-interaction features by leveraging the browser’s speech recognition capabilities, typically through the SpeechRecognition or webkitSpeechRecognition interfaces. At the time of writing, full support is available in Chromium-based browsers like Chrome and Edge (on desktop). Safari provides partial support through the webkitSpeechRecognition API. Firefox does not support speech recognition due to privacy and security concerns, and some Chromium-based browsers like Brave also omit support due to their exclusion of Google’s proprietary services.

To enable VoiceAssist, call [VoiceAssist.enable](#classmethod-voiceassistenable), optionally passing the [keyName](#classattr-voiceassistvoicekey) you want to use for activation and recording - the default is `Control`. Once initialized, VoiceAssist can be activated or deactivated with a triple-tap of the [VoiceAssist.voiceKey](#classattr-voiceassistvoicekey).

When recognition is active, a user may double-tap the `voiceKey` to begin dictating a value for a focused input control. Text appears in the input control as the user speaks and the transcription is completed by a subsequent double-tap of the `voiceKey`, or by remaining silent for a number of seconds.

In addition to value-dictation, a user may dictate a command to be issued to the focused component, which may deal with the text itself or forward to an AI for action. If the focused component doesn't [support voice-commands](Canvas.md#method-canvassupportsvoicecommands) but one of its parents does, that parent will be the focus of your dictated command. To begin dictating a command, press and hold the `voiceKey` - while the key remains pressed, the [VoiceAssist.recordingProgress](#classmethod-voiceassistrecordingprogress) method is fired with interim text-results as the user speaks.

If the user speaks one of the [VoiceAssist.cancelPhrases](#classattr-voiceassistcancelphrases), the interim text is discarded and recording is canceled.

When the user releases the speech-key, recording is stopped and the final text of the recording is passed to the [target component](Canvas.md#method-canvasdovoicecommand) for action.

**Note:** On [handset](Browser.md#classattr-browserishandset) and [tablet](Browser.md#classattr-browseristablet) devices, the keyboard gestures described above (triple-tap, double-tap, press-and-hold) are not available because virtual keyboards do not fire physical key events for modifier keys. Call [VoiceAssist.setActive](#classmethod-voiceassistsetactive) from a button or other UI element, and use [VoiceAssist.startDictatingValue](#classmethod-voiceassiststartdictatingvalue) or [VoiceAssist.startDictatingCommand](#classmethod-voiceassiststartdictatingcommand) to initiate recording programmatically.

---
## ClassAttr: VoiceAssist.cancelPhrases

### Description
A list of phrases that, when spoken, will cancel an ongoing recording without completing normally. When dictating a command, the transcription is simply discarded. When dictating a value, the transcription is discarded and the value in the focused component is restored to its pre-recording value.

The default cancel-phrase is "never mind" (or "nevermind").

**Flags**: IRW

---
## ClassAttr: VoiceAssist.doubleTapValueHint

### Description
Hint shown in the activation notification explaining how to dictate a value. The `${voiceKey}` token is replaced with the current [VoiceAssist.voiceKey](#classattr-voiceassistvoicekey).

### Groups

- i18nMessages

**Flags**: IRW

---
## ClassAttr: VoiceAssist.checkingMessage

### Description
Message shown in a brief notification while [Browser.checkSpeechRecognition](Browser.md#classmethod-browsercheckspeechrecognition) probes mic access and speech-service connectivity on the first call to [VoiceAssist.setActive](#classmethod-voiceassistsetactive).

### Groups

- i18nMessages

**Flags**: IRW

---
## ClassAttr: VoiceAssist.speechBlockedMessage

### Description
Error message shown when the browser blocks connections to an external speech-to-text service (for example, Brave blocks Google's speech service). The `${title}` token is replaced with [VoiceAssist.title](#classattr-voiceassisttitle).

### Groups

- i18nMessages

**Flags**: IRW

---
## ClassAttr: VoiceAssist.longPressButtonPrompt

### Description
Tooltip for the [voice-assist button](#classmethod-voiceassistgetvoiceassistbutton) when [voiceAssist.longPressRecording](#voiceassistlongpressrecording) is enabled. The `${title}` token is replaced with [VoiceAssist.title](#classattr-voiceassisttitle).

### Groups

- i18nMessages

**Flags**: IRW

---
## ClassAttr: VoiceAssist.networkErrorMessage

### Description
Error message shown when a network error interrupts an active recording. The partial transcription captured before the error is applied to the target field.

### Groups

- i18nMessages

**Flags**: IRW

---
## ClassAttr: VoiceAssist.voiceAssistIcon

### Description
[FormItemIcon](../reference_2.md#object-formitemicon) shown inline on applicable [FormItems](FormItem.md#class-formitem) when VoiceAssist is [active](#classattr-voiceassistactive). Clicking the icon toggles value-dictation on and off.

This is not a true [AutoChild](../reference.md#type-autochild) since VoiceAssist is not a widget, but it follows the same defaults/properties customization pattern. To customize, use `voiceAssistIconDefaults` for skinning-level changes and `voiceAssistIconProperties` for per-application overrides:

```
   isc.VoiceAssist.addClassProperties({
       voiceAssistIconProperties: {
           showOnFocus: false
       }
   });
 
```
Use [VoiceAssist.getVoiceAssistIcon](#classmethod-voiceassistgetvoiceassisticon) to retrieve a copy of the icon configuration for manual inclusion in a custom item's [FormItem.icons](FormItem.md#attr-formitemicons) array.

### See Also

- [VoiceAssist.getVoiceAssistIcon](#classmethod-voiceassistgetvoiceassisticon)
- [FormItem.showVoiceAssistIcon](FormItem.md#attr-formitemshowvoiceassisticon)

**Flags**: IR

---
## ClassAttr: VoiceAssist.dictateValueIconPrompt

### Description
Tooltip for the [voice-assist icon](#classattr-voiceassistvoiceassisticon) shown on [FormItems](FormItem.md#class-formitem) when VoiceAssist is active. The `${title}` token is replaced with [VoiceAssist.title](#classattr-voiceassisttitle).

### Groups

- i18nMessages

**Flags**: IRW

---
## ClassAttr: VoiceAssist.noSpeechSupportMessage

### Description
Error message shown when the browser does not provide a SpeechRecognition API at all (for example, Firefox). The `${title}` token is replaced with [VoiceAssist.title](#classattr-voiceassisttitle).

### Groups

- i18nMessages

**Flags**: IRW

---
## ClassAttr: VoiceAssist.canDictateCommands

### Description
Whether VoiceAssist allows command-dictation, where the user's speech is transcribed and forwarded to a target component (or AI) for execution. When false, the long-press gesture is ignored and [VoiceAssist.startDictatingCommand](#classmethod-voiceassiststartdictatingcommand) is a no-op.

### See Also

- [VoiceAssist.canDictateValues](#classattr-voiceassistcandictatevalues)
- [VoiceAssist.startDictatingCommand](#classmethod-voiceassiststartdictatingcommand)

**Flags**: IRW

---
## ClassAttr: VoiceAssist.language

### Description
The BCP 47 language-tag for the language that VoiceAssist expects to interpret. These are in the format _"language-REGION"_, like "en-US" or "fr-FR". If unset, VoiceAssist uses the language provided by your browser or OS.

**Flags**: IRW

---
## ClassAttr: VoiceAssist.enabledMessage

### Description
Message shown in a notification when VoiceAssist is [activated](#classmethod-voiceassistsetactive). The `${title}` token is replaced with [VoiceAssist.title](#classattr-voiceassisttitle).

### Groups

- i18nMessages

**Flags**: IRW

---
## ClassAttr: VoiceAssist.title

### Description
The display title used in dialogs, notifications, and tooltips.

### Groups

- i18nMessages

**Flags**: IRW

---
## ClassAttr: VoiceAssist.clickToRecordButtonPrompt

### Description
Tooltip for the [voice-assist button](#classmethod-voiceassistgetvoiceassistbutton) when [voiceAssist.longPressRecording](#voiceassistlongpressrecording) is not enabled. The `${title}` token is replaced with [VoiceAssist.title](#classattr-voiceassisttitle).

### Groups

- i18nMessages

**Flags**: IRW

---
## ClassAttr: VoiceAssist.active

### Description
Whether VoiceAssist is currently active for end-user interaction. This is distinct from [VoiceAssist.enabled](#classattr-voiceassistenabled) - a developer enables VoiceAssist (via [VoiceAssist.enable](#classmethod-voiceassistenable)), and the end user activates it (via triple-tap of the [speech-key](#classattr-voiceassistvoicekey), a UI button, or a programmatic call to [VoiceAssist.setActive](#classmethod-voiceassistsetactive)). Use [VoiceAssist.setActive](#classmethod-voiceassistsetactive) to change.

When active, voice-assist icons appear on applicable [FormItems](FormItem.md#class-formitem) and the dictation methods ([VoiceAssist.startDictatingValue](#classmethod-voiceassiststartdictatingvalue), [VoiceAssist.startDictatingCommand](#classmethod-voiceassiststartdictatingcommand)) become operational.

### See Also

- [VoiceAssist.setActive](#classmethod-voiceassistsetactive)
- [VoiceAssist.enabled](#classattr-voiceassistenabled)

**Flags**: IRW

---
## ClassAttr: VoiceAssist.disabledMessage

### Description
Message shown in a notification when VoiceAssist is [deactivated](#classmethod-voiceassistsetactive). The `${title}` token is replaced with [VoiceAssist.title](#classattr-voiceassisttitle).

### Groups

- i18nMessages

**Flags**: IRW

---
## ClassAttr: VoiceAssist.pressAndHoldCommandHint

### Description
Hint shown in the activation notification explaining how to dictate a command. The `${voiceKey}` token is replaced with the current [VoiceAssist.voiceKey](#classattr-voiceassistvoicekey).

### Groups

- i18nMessages

**Flags**: IRW

---
## ClassAttr: VoiceAssist.canDictateValues

### Description
Whether VoiceAssist allows value-dictation, where the user's speech is transcribed into a focused text field. When false, the voice-assist inline icon is not shown on form items, the double-tap gesture is ignored, and [VoiceAssist.startDictatingValue](#classmethod-voiceassiststartdictatingvalue) is a no-op.

### See Also

- [VoiceAssist.canDictateCommands](#classattr-voiceassistcandictatecommands)
- [VoiceAssist.startDictatingValue](#classmethod-voiceassiststartdictatingvalue)

**Flags**: IRW

---
## ClassAttr: VoiceAssist.autoStopDelay

### Description
VoiceAssist will stop recording automatically if the user stops speaking for this length of time. The default is 2 seconds.

**Flags**: IRW

---
## ClassAttr: VoiceAssist.micDeniedMessage

### Description
Error message shown when microphone permission has been denied by the user or by browser policy. The `${title}` token is replaced with [VoiceAssist.title](#classattr-voiceassisttitle).

### Groups

- i18nMessages

**Flags**: IRW

---
## ClassAttr: VoiceAssist.enabled

### Description
Whether VoiceAssist has been enabled by the application developer via [VoiceAssist.enable](#classmethod-voiceassistenable). Enabling installs keyboard listeners (on non-mobile browsers) and initializes the speech-recognition engine, making VoiceAssist available for end-user activation via [setActive(true)](#classmethod-voiceassistsetactive). Use [VoiceAssist.disable](#classmethod-voiceassistdisable) to reverse.

### See Also

- [VoiceAssist.enable](#classmethod-voiceassistenable)
- [VoiceAssist.disable](#classmethod-voiceassistdisable)
- [VoiceAssist.active](#classattr-voiceassistactive)

**Flags**: IR

---
## ClassAttr: VoiceAssist.noMicMessage

### Description
Error message shown when no microphone hardware is detected or the microphone was disconnected during recording. The `${title}` token is replaced with [VoiceAssist.title](#classattr-voiceassisttitle).

### Groups

- i18nMessages

**Flags**: IRW

---
## ClassAttr: VoiceAssist.voiceKey

### Description
The key that activates and performs VoiceAssist features like value and command dictation.

**Flags**: IRW

---
## ClassAttr: VoiceAssist.noSpeechDelay

### Description
VoiceAssist will stop recording automatically if the user doesn't speak at all for this length of time. The default is 3 seconds.

**Flags**: IRW

---
## ClassMethod: VoiceAssist.stopDictatingCommand

### Description
Stops an ongoing command-dictation session normally, forwarding the transcribed text to the target component for execution. Has no effect if command-dictation is not currently in progress.

### See Also

- [VoiceAssist.startDictatingCommand](#classmethod-voiceassiststartdictatingcommand)
- [VoiceAssist.cancelRecording](#classmethod-voiceassistcancelrecording)

**Flags**: A

---
## ClassMethod: VoiceAssist.recordingProgress

### Description
Event fired with interim text-results as the user speaks.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| text | [String](#type-string) | false | — | the latest text-results for an on-going recording |

**Flags**: A

---
## ClassMethod: VoiceAssist.startDictatingValue

### Description
Begins value-dictation for the currently focused [FormItem](FormItem.md#class-formitem). VoiceAssist locates the focused item via [EventHandler](EventHandler.md#class-eventhandler); if the focused item supports value-dictation (currently [TextItem](TextItem.md#class-textitem) and [TextAreaItem](TextAreaItem.md#class-textareaitem)), the user's speech is transcribed and applied as the item's value.

Recording stops automatically after a period of silence (see [VoiceAssist.autoStopDelay](#classattr-voiceassistautostopdelay)), or can be stopped explicitly via [VoiceAssist.stopDictatingValue](#classmethod-voiceassiststopdictatingvalue). The user can also say a [cancel phrase](#classattr-voiceassistcancelphrases) to discard the transcription.

Has no effect if VoiceAssist is not [active](#classattr-voiceassistactive), if [VoiceAssist.canDictateValues](#classattr-voiceassistcandictatevalues) is false, if no focused item supports value-dictation, or if a recording is already in progress.

### See Also

- [VoiceAssist.stopDictatingValue](#classmethod-voiceassiststopdictatingvalue)
- [VoiceAssist.canDictateValues](#classattr-voiceassistcandictatevalues)
- [VoiceAssist.cancelRecording](#classmethod-voiceassistcancelrecording)

**Flags**: A

---
## ClassMethod: VoiceAssist.setCancelPhrases

### Description
Sets the list of [cancel phrases](#classattr-voiceassistcancelphrases) that will abort an ongoing recording when spoken.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| cancelPhrases | [Array of String](#type-array-of-string) | false | — | new cancel phrases |

### See Also

- [VoiceAssist.cancelPhrases](#classattr-voiceassistcancelphrases)

---
## ClassMethod: VoiceAssist.disable

### Description
Disables VoiceAssist completely, removing keyboard listeners, deactivating if currently [active](#classattr-voiceassistactive), and canceling any in-progress recording. After calling this method, [VoiceAssist.enable](#classmethod-voiceassistenable) must be called again before VoiceAssist can be reactivated.

### See Also

- [VoiceAssist.setActive](#classmethod-voiceassistsetactive)

**Flags**: A

---
## ClassMethod: VoiceAssist.getActive

### Description
Returns whether VoiceAssist is currently [active](#classattr-voiceassistactive) for end-user interaction.

### Returns

`[boolean](../reference.md#type-boolean)` — true if VoiceAssist is active

### See Also

- [VoiceAssist.setActive](#classmethod-voiceassistsetactive)

---
## ClassMethod: VoiceAssist.getEnabled

### Description
Returns whether VoiceAssist has been [enabled](#classattr-voiceassistenabled) by the application developer.

### Returns

`[boolean](../reference.md#type-boolean)` — true if VoiceAssist is enabled

### See Also

- [VoiceAssist.enable](#classmethod-voiceassistenable)
- [VoiceAssist.disable](#classmethod-voiceassistdisable)

---
## ClassMethod: VoiceAssist.stopRecording

### Description
Stops any ongoing recording session (value or command) normally, applying the transcribed text. For value-dictation, the text is set as the item's value; for command-dictation, the text is forwarded to the target component for execution.

### Returns

`[boolean](../reference.md#type-boolean)` — true if a recording was stopped, false if no recording was in progress

**Flags**: A

---
## ClassMethod: VoiceAssist.enable

### Description
Enables the VoiceAssist module by initializing the speech-recognition engine and, on non-mobile browsers, installing keyboard listeners for the [speech-key](#classattr-voiceassistvoicekey). Once enabled, a user may triple-tap the speech-key to [activate](#classmethod-voiceassistsetactive) VoiceAssist. On [handset](Browser.md#classattr-browserishandset) and [tablet](Browser.md#classattr-browseristablet) devices, keyboard listeners are skipped (virtual keyboards do not fire physical key events); call [VoiceAssist.setActive](#classmethod-voiceassistsetactive) directly from a button or other UI element instead.

No intrusive mic/speech probe is performed at enable time. The probe runs on the first call to [VoiceAssist.setActive](#classmethod-voiceassistsetactive).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| key | [String](#type-string) | true | — | optional different key to use for VoiceAssist - use with care |

### See Also

- [VoiceAssist.setActive](#classmethod-voiceassistsetactive)
- [Browser.checkSpeechRecognition](Browser.md#classmethod-browsercheckspeechrecognition)

**Flags**: A

---
## ClassMethod: VoiceAssist.stopDictatingValue

### Description
Stops an ongoing value-dictation session normally, applying the transcribed text to the target [FormItem](FormItem.md#class-formitem). Has no effect if value-dictation is not currently in progress.

### See Also

- [VoiceAssist.startDictatingValue](#classmethod-voiceassiststartdictatingvalue)
- [VoiceAssist.cancelRecording](#classmethod-voiceassistcancelrecording)

**Flags**: A

---
## ClassMethod: VoiceAssist.cancelRecording

### Description
Cancels any ongoing recording session (value or command) and discards the transcription. If value-dictation was in progress, the target item's value is restored to its pre-recording state.

### Returns

`[boolean](../reference.md#type-boolean)` — true if a recording was canceled, false if no recording was in progress

**Flags**: A

---
## ClassMethod: VoiceAssist.getVoiceAssistButton

### Description
Returns an [Img](Img.md#class-img) widget pre-configured to start and stop VoiceAssist recording. The button can be placed anywhere in the UI (toolbars, tab-bar controls, etc.) to give users a clickable entry point for voice interaction.

When clicked, the button determines the recording mode based on the currently focused component. If a [FormItem](FormItem.md#class-formitem) that supports value-dictation is focused, value-dictation begins; otherwise, command-dictation begins. Recording stops on a second click, or automatically after a period of silence (see [VoiceAssist.autoStopDelay](#classattr-voiceassistautostopdelay)).

If VoiceAssist is not yet [active](#classmethod-voiceassistsetactive) when clicked, the button calls [VoiceAssist.setActive](#classmethod-voiceassistsetactive) automatically. Note that [VoiceAssist.enable](#classmethod-voiceassistenable) must have been called first, otherwise setActive() will log a warning and return without activating.

The button is created with `canFocus: false` so that clicking it does not steal focus from the component whose value or commands are being dictated.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| properties | [Img Properties](#type-img-properties) | true | — | optional properties to apply to the returned Img widget, for example a title or ID |

### Returns

`[Img](#type-img)` — a live widget wired for VoiceAssist recording

---
## ClassMethod: VoiceAssist.getVoiceAssistIcon

### Description
Returns a [FormItemIcon](../reference_2.md#object-formitemicon) properties object configured for VoiceAssist value-dictation. The returned object merges [voiceAssistIcon](#classattr-voiceassistvoiceassisticon) defaults, then `voiceAssistIconProperties`, then any supplied `properties` argument, so all three customization levels are reflected.

This is the same icon configuration used internally when [FormItem.showVoiceAssistIcon](FormItem.md#attr-formitemshowvoiceassisticon) is enabled. Use this method to retrieve the config for manual inclusion in a custom item's [FormItem.icons](FormItem.md#attr-formitemicons) array.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| properties | [FormItemIcon Properties](#type-formitemicon-properties) | true | — | additional properties to apply to the icon, overriding both defaults and properties |

### Returns

`[FormItemIcon](#type-formitemicon)` — icon properties for VoiceAssist

### See Also

- [VoiceAssist.voiceAssistIcon](#classattr-voiceassistvoiceassisticon)

---
## ClassMethod: VoiceAssist.getCancelPhrases

### Description
Returns the current list of [cancel phrases](#classattr-voiceassistcancelphrases).

### Returns

`[Array of String](#type-array-of-string)` — current cancel phrases

### See Also

- [VoiceAssist.cancelPhrases](#classattr-voiceassistcancelphrases)

---
## ClassMethod: VoiceAssist.startDictatingCommand

### Description
Begins command-dictation. VoiceAssist locates a target component by walking up the parent chain from the currently focused widget, looking for one that supports voice commands (see `supportsVoiceCommands()`). The user's speech is transcribed and forwarded to the target for execution.

Recording stops automatically after a period of silence (see [VoiceAssist.autoStopDelay](#classattr-voiceassistautostopdelay)), or can be stopped explicitly via [VoiceAssist.stopDictatingCommand](#classmethod-voiceassiststopdictatingcommand). The user can also say a [cancel phrase](#classattr-voiceassistcancelphrases) to discard the transcription.

Has no effect if VoiceAssist is not [active](#classattr-voiceassistactive), if [VoiceAssist.canDictateCommands](#classattr-voiceassistcandictatecommands) is false, or if a recording is already in progress.

### See Also

- [VoiceAssist.stopDictatingCommand](#classmethod-voiceassiststopdictatingcommand)
- [VoiceAssist.canDictateCommands](#classattr-voiceassistcandictatecommands)
- [VoiceAssist.cancelRecording](#classmethod-voiceassistcancelrecording)

**Flags**: A

---
## ClassMethod: VoiceAssist.setActive

### Description
Sets whether VoiceAssist is active. When active, the dictation methods ([VoiceAssist.startDictatingValue](#classmethod-voiceassiststartdictatingvalue), [VoiceAssist.startDictatingCommand](#classmethod-voiceassiststartdictatingcommand)) become operational, subject to [VoiceAssist.canDictateValues](#classattr-voiceassistcandictatevalues) and [VoiceAssist.canDictateCommands](#classattr-voiceassistcandictatecommands). Voice-assist icons appear on applicable [FormItems](FormItem.md#class-formitem) if [VoiceAssist.canDictateValues](#classattr-voiceassistcandictatevalues) is true. When set to false, any in-progress recording is stopped and icons are hidden.

On the first call with `true`, [Browser.checkSpeechRecognition](Browser.md#classmethod-browsercheckspeechrecognition) runs a brief probe to verify mic access and speech-service connectivity. If the probe fails, VoiceAssist shows an explanatory message and does not become active. Subsequent calls skip the probe and use the cached result.

[VoiceAssist.enable](#classmethod-voiceassistenable) must be called before this method can activate VoiceAssist. If `enable()` has not been called, this method logs a warning and returns without activating.

On non-mobile devices, this method is called internally when the user triple-taps the [speech-key](#classattr-voiceassistvoicekey) (toggling the active state). On [handset](Browser.md#classattr-browserishandset) and [tablet](Browser.md#classattr-browseristablet) devices, call it directly from a button or other UI element.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| active | [boolean](../reference.md#type-boolean) | false | — | true to activate, false to deactivate |
| callback | [Callback](../reference.md#type-callback) | true | — | optional callback fired when the activation or deactivation is complete. Because the first activation involves an asynchronous speech-recognition probe, callers that need to know when VoiceAssist is actually ready should pass a callback rather than assuming synchronous completion. The callback receives a single boolean argument: true if VoiceAssist is now in the requested state, false if activation failed (mic denied, speech service blocked, etc.). |

### See Also

- [VoiceAssist.enable](#classmethod-voiceassistenable)

---
