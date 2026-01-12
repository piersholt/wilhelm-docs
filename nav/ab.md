# `0xab` Navigation View Status
 
NAV `0x7f` → GTF `0x43`

The GTF gets informed by this command about the current navigation view state.

### Related Commands

- `0xaa` [Navigation Control](aa.md)

### Example Frames
    7F 04 43 AB 01 92  # Navigation focused    
    7F 04 43 AB 20 B3  # Switched to radio
    7F 04 43 AB 21 B2  # Main menu rendered

## Parameters

Fixed length. One byte bitfield.


    UNKNOWN               = 0b0000_0001
    NAV_NOT_FOCUSED       = 0b0010_0000

### Unknown `0b0000_0001`
    
I could not figure out the use case.\
The bit is set when focusing the navigation view and when the main menu is rendered.

It's not set when switching directly from navigation to another screen that is not the main menu.\
But this happens only if the GTF is the one who focused the navigation view.\
Else, there will be no message at all.

### Nav Not Focused `0b0010_0000`

Only set when the navigation view is **not** focused.

## Use Cases

The GTF uses this to determine if it should pass the GT/NAV video through to the FMBT (Rear Screen).