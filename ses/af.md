# `0xaf` SES Navigation Status

NAV `0x7f` → SES `0xb0`

Reports the navigation map-scale capability state used by SES.

The SES requests this status with `AA 07 00`.

### Related Commands

- `0xaa` [SES Navigation Control](aa.md)

### Example Frames

    7F 04 B0 AF 01 65
    7F 04 B0 AF 04 60

## Parameters

Fixed length. One byte.

| Value  | Function |
|:-------|:---------|
| `0x01` | Upper scale index is outside `12..14` |
| `0x04` | Upper scale index is `12..14` |

The navigation computer derives this value from the upper map-scale boundary reported by its map display controller.

`0x04` is sent when that internal upper scale index is `12`, `13` or `14`. All other values produce `0x01`.

The same internal boundary is used by the map scale window to limit how far the user can zoom out. It is not the currently selected map scale.
