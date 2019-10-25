# Controls
## Multifunction Steering Wheel (MFL)


### Multifunction `0x3B`

One byte bit field.

Bit|7|6|5-4|3-0
:---|:---|:---|:---|:---
Use|Telephone|R/T|State|Back/Forward


    FORWARD = 0b0000_0001
    BACK    = 0b0000_1000
    
    PRESS   = 0b0000_0000
    HOLD    = 0b0001_0000
    RELEASE = 0b0010_0000
    
    R_T     = 0b0100_0000
    
    TEL     = 0b1000_0000

#### R/T (Radio/Telephone)

The R/T button will determine if the Radio `0x68` or Telephone `0xc8` is the recipient of various messages.

It's use is dependent on a Telephone being present, and MFL will periodically check for it's presence:

    # MFL Telephone presence check
    50 03 C8 01 9A

The R/T button behaves like a toggle switch, and does not have press, hold, or release states. Each time R/T it is pressed, a single bit `0b0100_0000` is flipped, thus allowing for only one of two messages:

    # Telephone Mode
    50 04 C8 3B 40 E7   # 0b0100_0000 => 0x40
    
    # Radio Mode
    50 04 C8 3B 00 A7   # 0b0000_0000 => 0x00
    
The bit will only be set for the R/T button press, and not with any other button presses. For example, if R/T is pressed (for telephone mode), and then Forward is pressed (for next contact), the bit will not be set in the subsequent messages:
    
    
    50 04 C8 3B 40 E7   # Select "Telephone Mode"
    50 04 C8 3B 01 A6   # Next contact press (R/T bit not set!)
    50 04 C8 3B 21 86   # Next contact release (R/T bit not set!)


The variation in commands is covered below.


#### Buttons: Back & Forward

##### Radio Mode

    # Forward
    50 04 68 3B 01 06   # Press
    50 04 68 3B 11 16   # Hold
    50 04 68 3B 21 26   # Release
    
    # Back
    50 04 68 3B 08 0F   # Press
    50 04 68 3B 18 1F   # Hold
    50 04 68 3B 28 2F   # Release

##### Telephone Mode
    
    # Forward (Next Contact)
    50 04 C8 3B 01 A6   # Press
    50 04 C8 3B 11 B6   # Hold
    50 04 C8 3B 21 86   # Release
    
    # Back (Previous Contact)
    50 04 C8 3B 08 AF   # Press
    50 04 C8 3B 18 BF   # Hold
    50 04 C8 3B 28 8F   # Release
    
#### Button: Telephone

Note: depending on year, and options, the button icon may be either a "telephone", or "speaking".
    
    # Telephone
    50 04 C8 3B 00 A7   # Press
    50 04 C8 3B 80 27   # Hold
    50 04 C8 3B A0 07   # Release

---

### Volume `0x32`

The **MFL** uses the same command as **BMBT** when the volume buttons are used.

The MFL's momentary buttons can only emulate the BMBT's rotary encoder output. They will emit a direction, but do not support velocity/rate of change. The "step" will always be `1` regardless of the rate at which the switch is used. 

Pushing the volume buttons at a higher frequency of use will simply send single step commands at a corresponding higher frequency. Holding the volume buttons down will continuously send the same command at a fixed rate.

The R/T mode has no effect on volume. Whether radio or telephone is the recipient of volume commands is based on [telephone status](../status.md); specifically the the "active", and "handsfree" bits being set (as per an active call on speakerphone).

Bit|7-5|4|3|2|1|0
:---|:---|:---|:---|:---|:---|:---
Use|--|Step|--|--|--|Direction|

    # Direction
    DOWN   = 0b0000_0000
    UP     = 0b0000_0001
    
    # Steps
	STEPS  = 0b0001_0000   # fixed value!

##### Radio (Default)
    
    50 04 68 32 10 1E   # Volume Down
    50 04 68 32 11 1F   # Volume Up


##### Telephone (handsfree call)

    50 04 C8 32 10 BE   # Volume Down
    50 04 C8 32 11 BF   # Volume Up