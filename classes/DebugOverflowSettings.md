# DebugOverflowSettings Documentation

[← Back to API Index](../reference.md)

---

## Attr: DebugOverflowSettings.loggingTimeout

### Description
How often to log the [overflow threshold](#attr-debugoverflowsettingsselfoverflowthreshold) being crossed, expressed in milliseconds. A setting of null or zero disable the limitation.

If this property is a positive number, and fewer than that many milliseconds have elapsed since the last time we logged an overflow problem for a canvas, then logging will be skipped for that canvas.

**Flags**: IRW

---
## Attr: DebugOverflowSettings.maxTrackedOverflows

### Description
Maximum number of overflows to track for each canvas when debugging overflow.

**Flags**: IRW

---
## Attr: DebugOverflowSettings.trackingDuration

### Description
Maximum time interval past which overflow data will be discarded when debugging overflow, measured in milliseconds.

**Flags**: IRW

---
## Attr: DebugOverflowSettings.selfOverflowThreshold

### Description
At what threshold should excessive self-overflows be reported? This value must not exceed [DebugOverflowSettings.maxTrackedOverflows](#attr-debugoverflowsettingsmaxtrackedoverflows).

**Flags**: IRW

---
## Attr: DebugOverflowSettings.loggingLevel

### Description
Logging level to use when reporting that the [overflow threshold](#attr-debugoverflowsettingsselfoverflowthreshold) was exceeded.

**Flags**: IRW

---
