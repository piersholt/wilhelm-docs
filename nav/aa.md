# `0xaa` GTF Navigation Control

GTF `0x43` → NAV `0x7f`

Focuses the navigation applet for the rear graphics stage.

### Related Commands

- `0xab` [GTF Remote Control Status](ab.md)
- `0xaa` [SES Navigation Control](../ses/aa.md)

### Example Frames

    43 04 7F AA 00 92

## Parameters

At least one data byte is required. The value itself is ignored.

Any non-empty payload focuses the navigation applet and continues with the current navigation view.
