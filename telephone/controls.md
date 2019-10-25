# Controls
## Onboard-Monitor (BMBT)

*Note: may vary between E39 and E46 BMBTs?*

### Buttons `0x48`

One byte bit field.

Bit|7-6|5-0
---|---|---|
Use|Button State|Button ID


    # Button ID
    PRESET_1    = 0b0001_0001
    PRESET_2    = 0b0000_0001
    PRESET_3    = 0b0001_0010
    PRESET_4    = 0b0000_0010
    PRESET_5    = 0b0001_0011
    PRESET_6    = 0b0000_0011
    FM          = 0b0011_0001
    AM          = 0b0010_0001
    MODE_PREV   = 0b0010_0011
    OVERLAY     = 0b0011_0000
    POWER       = 0b0000_0110 # Volume dial button
    
    TAPE_EJECT  = 0b0010_0100
    TELEPHONE   = 0b0000_1000
    TAPE_SIDE   = 0b0001_0100
    AUX_HEAT    = 0b0000_0111 # "Clock"
    TONE        = 0b0000_0100
    PREV        = 0b0001_0000
    NEXT        = 0b0000_0000
    MENU        = 0b0011_0100
    CONFIRM     = 0b0000_0101 # Navigation dial button

    # Note: only on legacy BMBT
    MODE_NEXT   = 0b0011_0011
    SELECT      = 0b0010_0000
    TP          = 0b0011_0010 # DOLBY C
    RDS         = 0b0010_0010 # DOLBY B
    
    # Button State
    PRESS       = 0b0000_0000
    HOLD        = 0b0100_0000
    RELEASE     = 0b1000_0000
    
#### Radio `0x68`
    
    # Only selected examples.
    # Press, hold, and release states.

    # Tape Side
    F0 04 68 48 14 C0 
    F0 04 68 48 54 80 
    F0 04 68 48 94 40

    # Preset 1
    F0 04 68 48 11 C5
    F0 04 68 48 51 85
    F0 04 68 48 91 45

    # Next
    F0 04 68 48 01 D5
    F0 04 68 48 41 95
    F0 04 68 48 81 55
    
    
#### GT `0x3b`

    # Confirm (Nav. dial button)
    F0 04 3B 48 05 82
    F0 04 3B 48 45 C2
    F0 04 3B 48 85 02
    

#### Global `0xff`
        
    # Telephone
    F0 04 FF 48 08 4B
    F0 04 FF 48 48 0B 
    F0 04 FF 48 88 CB
    
    # Aux Heat ("Clock")
    F0 04 FF 48 07 44 
    F0 04 FF 48 47 04
    F0 04 FF 48 87 C4
    
    # Menu
    F0 04 FF 48 34 F7
    F0 04 FF 48 74 37
    F0 04 FF 48 B4 F7

---

### "Soft" Buttons `0x47`

The Info button will open a new menu on the widescreen BMBT with radio options for RDS, and TP. Selecting these options will have the GT emulate legeacy BMBT button commands for TP and RDS.

One byte bit field.

Bit|7-6|5-0
---|---|---|
Use|Button State|Button ID
    
    # Button ID
    SELECT  = 0b0000_1111
    INFO    = 0b0011_1000
    
    # Button State
    PRESS       = 0b0000_0000
    HOLD        = 0b0100_0000
    RELEASE     = 0b1000_0000
    
    # Select    
    F0 05 FF 47 00 0F 42
    F0 05 FF 47 00 4F 02
    F0 05 FF 47 00 8F C2

    # Info
    F0 05 FF 47 00 38 75
    F0 05 FF 47 00 78 35
    F0 05 FF 47 00 B8 F5
    
---

### Volume Dial `0x32`

One byte bit field.

Bit|7-4|3-1|0
---|---|---|---
Use|Steps|--|Direction
        
    # Steps (variable)
    MIN     = 0b0001_0000
    MAX     = 0b1111_0000
    
    # Direction
    DOWN    = 0b0000_0000
    UP      = 0b0001_0000
    
#### Radio Volume
    
    # Volume Down
    F0 04 68 32 10 BE   # 1 step
    F0 04 68 32 20 8E   # 2 steps
    F0 04 68 32 30 9E   # 3 steps
    F0 04 68 32 40 EE   # 4 steps
    
    # Volume Up
    F0 04 68 32 11 BF   # 1 step
    F0 04 68 32 21 8F   # 2 steps
    F0 04 68 32 31 9F   # 3 steps
    F0 04 68 32 41 EF   # 4 steps

#### Telephone Volume

In order for BMBT to send volume commands to Telephone `0xc8`, [telephone status](../something.md) must have "active" and "handsfree" bits set.

    # Volume Down
    F0 04 C8 32 10 1E   # 1 step etc..
    
    # Volume Up
    F0 04 C8 32 11 1F   # 1 step etc..

---

### Navigation Dial `0x49` 

One byte bit field. Reversed fields as compared to volume control `0x32`, but otherwise the same in operation.

Always sent to GT `0x3b`.

Bit|7|6-4|3-0
---|---|---|---
Use|Direction|--| Steps

    # Direction
    LEFT    = 0b0000_0000
    RIGHT   = 0b1000_0000
        
    # Steps (variable)
    MIN     = 0b0000_0001
    MAX     = 0b0000_1111

    # Left
    F0 04 3B 49 01 87   # 1 step
    F0 04 3B 49 02 84   # 2 steps etc...
        
    # Right
    F0 04 3B 49 81 07   # 1 step
    F0 04 3B 49 82 04   # 2 steps etc...

## Multifunction Steering Wheel (MFL)


### Multifunction `0x3B`


Bit|7|6|5-4|3-0
---|---|---|----|----|---
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

The R/T button behaves like a toggle switch, thus negating the need for a momentary state like the Back, Forward, and Telephone buttons. Each time R/T it is pressed, a single bit `0b0100_0000` is flipped, thus allowing for only one of two messages:

    # Telephone Mode
    50 04 C8 3B 40 E7   # 0b0100_0000 => 0x40
    
    # Radio Mode
    50 04 C8 3B 00 A7   # 0b0000_0000 => 0x00
    
The toggle is only ever set when pressing R/T, and not with any other button presses. For example, if R/T is pressed (for telephone mode), and then Forward is pressed (for next contact), the bit will not be set in the subsequent messages:
    
    
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
    
    50 04 C8 3B 00 A7   # Press
    50 04 C8 3B 80 27   # Hold
    50 04 C8 3B A0 07   # Release

---

### Volume `0x32`

The **MFL** uses the same command as **BMBT** when the volume buttons are used.

The MFL's momentary buttons can only emulate the BMBT's rotary encoder output. They will emit a direction, but do not support velocity/rate of change. The "step" will always be `1` regardless of the rate at which the switch is used. 

Pushing the volume buttons at a higher frequency of use will simply send single step commands at a corresponding higher frequency. 

Holding the volume buttons down will continuously send the same command at a fixed rate.

The R/T mode has no effect.


Bit|7-5|4|3|2|1|0
:---|:---|:---|:----|:----|:---|:---|:---|:---
Use|--|Step|--|--|--|Direction|

    # Direction
    DOWN   = 0b0000_0000
    UP     = 0b0000_0001
    
    # Steps
	STEPS  = 0b0001_0000   # fixed value!

##### Default (Radio)
    
    50 04 68 32 10 1E   # Volume Down
    50 04 68 32 11 1F   # Volume Up


##### Telephone (handsfree/speaker)

    50 04 C8 32 10 BE   # Volume Down
    50 04 C8 32 11 BF   # Volume Up