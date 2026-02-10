# VoiceAssist Documentation

[← Back to API Index](../reference.md)

---

## Class: VoiceAssist

### Description
The VoiceAssist class provides voice-interaction features by leveraging the browser’s speech recognition capabilities, typically through the SpeechRecognition or webkitSpeechRecognition interfaces. At the time of writing, full support is available in Chromium-based browsers like Chrome and Edge (on desktop). Safari provides partial support through the webkitSpeechRecognition API. Firefox does not support speech recognition due to privacy and security concerns, and some Chromium-based browsers like Brave also omit support due to their exclusion of Google’s proprietary services.

To enable VoiceAssist, call [VoiceAssist.enable](#classmethod-voiceassistenable), optionally passing the [keyName](#attr-voiceassistvoicekey) you want to use for activation and recording - the default is `Control`. Once initialized, VoiceAssist can be activated or deactivated with three quick taps of the [VoiceAssist.voiceKey](#attr-voiceassistvoicekey).

When recognition is active, a user may double-tap the `voiceKey` to begin dictating a value for a focused input control. Text appears in the input control as the user speaks and the transcription is completed by a subsequent double-tap of the `voiceKey`, or by remaining silent for a number of seconds.

In addition to value-dictation, a user may dictate a command to be issued to the focused component, which may deal with the text itself or forward to an AI for action. If the focused component doesn't [support voice-commands](Canvas.md#method-canvassupportsvoicecommands) but one of its parents does, that parent will be the focus of your dictated command. To begin dictating a command, press and hold the `voiceKey` - while the key remains pressed, the [VoiceAssist.recordingProgress](#classmethod-voiceassistrecordingprogress) method is fired with interim text-results as the user speaks.

If the user speaks one of the [VoiceAssist.cancelPhrases](#attr-voiceassistcancelphrases), the interim text is discarded and recording is canceled.

When the user releases the speech-key, recording is stopped and the final text of the recording is passed to the [target component](Canvas.md#method-canvasdovoicecommand) for action.

---
## Attr: VoiceAssist.autoStopDelay

### Description
VoiceAssist will stop recording automatically if the user stops speaking for this length of time. The default is 2 seconds.

**Flags**: IRW

---
## Attr: VoiceAssist.cancelPhrases

### Description
A list of phrases that, when spoken, will cancel an ongoing recording without completing normally. When dictating a command, the transcription is simply discarded. When dictating a value, the transcription is discarded and the value in the focused component is restored to its pre-recording value.

The default cancel-phrase is "never mind" (or "nevermind").

**Flags**: IRW

---
## Attr: VoiceAssist.noSpeechDelay

### Description
VoiceAssist will stop recording automatically if the user doesn't speak at all for this length of time. The default is 3 seconds.

**Flags**: IRW

---
## Attr: VoiceAssist.waitForNetworkErrorDelay

### Description
The time to wait for the browser to issue a "network" error when [VoiceAssist.enable()](#classmethod-voiceassistenable) runs.

Some browsers provide a SpeechRecognition implementation but prevent it from contacting an external speech-to-text service, instead issuing an immediate "network" error once the mic is activated. To detect this, enabling VoiceAssist starts a test-session and waits `waitForNetworkErrorDelay` for a "network" error.

If there's an error, a log is made and subsequent user-attempts to start VoiceAssist by triple-tapping the [VoiceAssist.voiceKey](#attr-voiceassistvoicekey) will show the log in a popup.

**Flags**: IRW

---
## Attr: VoiceAssist.voiceKey

### Description
The key that activates and performs VoiceAssist features like value and command dictation.

**Flags**: IRW

---
## Attr: VoiceAssist.language

### Description
The BCP 47 language-tag for the language that VoiceAssist expects to interpret. These are in the format _"language-REGION"_, like "en-US" or "fr-FR". If unset, VoiceAssist uses the language provided by your browser or OS.

**Flags**: IRW

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
## ClassMethod: VoiceAssist.disable

### Description
Disables the VoiceAssist module, canceling any current dictation and deactivating the ability to dictate values and commands for components in the UI.

**Flags**: A

---
## ClassMethod: VoiceAssist.enable

### Description
Enables the VoiceAssist module - once enabled, a user may triple-tap the [speech-key](#attr-voiceassistvoicekey) to activate VoiceAssist, allowing them to dictate values and commands for components in the UI.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| doPermissionChecks | [Boolean](#type-boolean) | true | — | when true, performs permissions checks as part of this call - otherwise, checks are performed when user starts VoiceAssist, by triple-tapping the [VoiceAssist.voiceKey](#attr-voiceassistvoicekey) |
| key | [String](#type-string) | true | — | optional different key to use for VoiceAssist - use with care |

**Flags**: A

---
