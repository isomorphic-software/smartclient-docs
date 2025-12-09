# Sound Documentation

[← Back to API Index](../reference.md)

---

## Class: Sound

*Inherits from:* [BaseWidget](BaseWidget.md#class-basewidget)

### Description
SmartClient class for loading and playing audio files using the HTML5 `<AUDIO>` element.

---
## Attr: Sound.src

### Description
URL of the audio file to be played by this sound instance. If multiple file URLs are supplied, the browser will make use of the first file type for which it has support.

**Flags**: IRW

---
## Attr: Sound.autoPlay

### Description
Should the specified [audio file](#attr-soundsrc) be played automatically?

If set to `false` developers may play the audio explicitly via [Sound.play](#method-soundplay).

**Flags**: IRW

---
## Attr: Sound.autoLoad

### Description
Should the specified [audio file](#attr-soundsrc) be loaded automatically.

If set to `false` developers may load the audio explicitly via [Sound.load](#method-soundload)

**Flags**: IRW

---
## ClassMethod: Sound.play

### Description
Convenience method to load and play a specified audio file.

For more explicit control over loading and playback of audio files, developers may create an instance of Sound and call methods directly on that object.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| src | [String](#type-string) | false | — | URL of the audio clip to play |
| playbackCompleteCallback | [PlaybackCompleteCallback](#type-playbackcompletecallback) | true | — | callback to execute when the clip playback completes |

---
## ClassMethod: Sound.isSupported

### Description
Returns true for browsers which natively support HTML5 Audio, used by the Sound class

### Returns

`[boolean](../reference.md#type-boolean)` — true if Audio is supported in this browser

---
## Method: Sound.setCurrentTime

### Description
Move playback to a particular time in a loaded audio file.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| time | [Float](../reference.md#type-float) | false | — | time to move to. This method will have no effect if the file has not been loaded or no [Sound.src](#attr-soundsrc) element is defined. |

---
## Method: Sound.setSrc

### Description
Update the [Sound.src](#attr-soundsrc) of this sound instance at runtime. Note that [Sound.autoLoad](#attr-soundautoload) and [Sound.autoPlay](#attr-soundautoplay) govern whether this media will be loaded or played immediately when the src value is changed.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| src | [String](#type-string)|[Array of String](#type-array-of-string) | false | — | URL of new audio file to be played by this sound instance. |

---
## Method: Sound.getCurrentTime

### Description
Retrieves the current playback time of a playing or paused audio file in seconds.

### Returns

`[Float](../reference.md#type-float)` — current playback time audio file in seconds. If the file has not been loaded, or no [Sound.src](#attr-soundsrc) is defined, this method will return zero.

---
## Method: Sound.reset

### Description
If playback is currently paused, reset the playback position to the start of the audio file so a call to [Sound.play](#method-soundplay) will play from the start, rather than resuming playback from the current position.

---
## Method: Sound.load

### Description
This method will cause the [specified audio file](#attr-soundsrc) to be loaded

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| canPlayCallback | [CanPlayCallback](#type-canplaycallback) | true | — | notification to fire when the file is ready to play |

---
## Method: Sound.getDuration

### Description
Retrieves the duration of the current audio file in seconds.

### Returns

`[Float](../reference.md#type-float)` — duration of the audio file in seconds. If the file has not been loaded, or no [Sound.src](#attr-soundsrc) is defined, this method will return null.

---
## Method: Sound.play

### Description
Play the audio file. If necessary the file will be loaded first.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| playbackCompleteCallback | [PlaybackCompleteCallback](#type-playbackcompletecallback) | true | — | notification fired when playback completes |

---
## Method: Sound.timeChanged

### Description
Notification method fired repeatedly to indicate a change in currentTime value while an audio file is playing.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| currentTime | [float](../reference.md#type-float) | false | — | Current playback position in seconds. |

---
## Method: Sound.pause

### Description
Pause playback of the audio file.

---
