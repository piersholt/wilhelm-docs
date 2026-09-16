# `0xab` GTF Remote Control Status
 
NAV `0x7f` → GTF `0x43`

Reports navigation control transitions to the GTF.

The payload is one enumerated status byte. Six values are defined: `0x00`, `0x01`, `0x10`, `0x11`, `0x20` and `0x21`. They are not independent bit flags.

### Related Commands

- `0xaa` [Navigation Control](aa.md)
- `0x9e` [FMBT Rear Monitor Control](../fmbt/9e.md)
- `0x9f` [FMBT Rear Monitor Status](../fmbt/9f.md)

### Example Frames

    7F 04 43 AB 00 93
    7F 04 43 AB 01 92
    7F 04 43 AB 10 83
    7F 04 43 AB 11 82
    7F 04 43 AB 20 B3
    7F 04 43 AB 21 B2  # Main menu

## Parameters

Fixed length. One byte.

| Value  | Meaning |
|:-------|:--------|
| `0x00` | GTF navigation session entered outside the GTF navigation view group |
| `0x01` | GTF navigation session entered inside the GTF navigation view group |
| `0x10` | GTF navigation control context inactive |
| `0x11` | GTF navigation control context active |
| `0x20` | Latched GTF navigation view state released |
| `0x21` | Main menu |

### `0x00` / `0x01` Session Entry

When the GTF navigation control context is active, entering the session reports whether the current navigation view belongs to the GTF navigation view group:

    0x00 = outside the view group
    0x01 = inside the view group

`0x01` also latches that state so leaving the view group can be reported later with `0x20`.

If the GTF navigation control context is not active when the session starts, `0x10` is sent instead.

### `0x10` / `0x11` Control Context

`0x11` reports that the navigation control context used by the GTF is active.

`0x10` reports the inactive state. If a latched GTF navigation view state was active when the control context becomes inactive, the navigation computer sends:

    0x20
    0x10

### `0x20` View-State Exit

`0x20` releases the latched GTF navigation view state.

It is sent when the active view leaves the GTF navigation view group or when the GTF navigation control context becomes inactive while that view state is latched.

### `0x21` Main Menu

`0x21` is sent when the navigation UI enters the main menu.

## Use Cases

The GTF uses these transitions to follow the navigation session for the rear display.

The related FMBT rear monitor state is controlled with `0x9e` / `0x9f`.
