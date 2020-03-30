The properties maintained by the cluster have a unique ID that is used by several commands.

The table below denotes which properties are applicable to which commands.

ID|Property|`0x24`|`0x2a`|`0x40`|`0x41`|`0x42`
:--|-------|------|------|------|------|------
`0x01`|Time|✅|❌|✅|✅|✅
`0x02`|Date|✅|❌|✅|✅|✅
`0x03`|Temperature|✅|❌|❌|✅|❌
`0x04`|Consump. 1|✅|❌|❌|✅|✅
`0x05`|Consump. 2|✅|❌|❌|✅|✅
`0x06`|Range|✅|❌|❌|✅|✅
`0x07`|Distance|✅|❌|✅|✅|✅
`0x08`|Arrival|✅|❌|❌|✅|✅
`0x09`|Limit|✅|✅|✅|✅|✅
`0x0a`|Avg. Speed|✅|❌|❌|✅|✅
`0x0b`|_PROG_|❌|❌|❌|❌|❌
`0x0c`|Memo|❌|✅|❌|✅|❌
`0x0d`|Code|✅|✅|✅|✅|❌
`0x0e`|Timer|✅|✅|❌|✅|✅
`0x0f`|Aux. Timer 1|✅|✅|✅|✅|✅
`0x10`|Aux. Timer 2|✅|✅|✅|✅|✅
`0x11`|Aux. Heat. (Off)|❌|✅|❌|✅|❌
`0x12`|Aux. Heat. (On)|❌|✅|❌|✅|❌
`0x13`|Aux. Vent. (Off)|❌|✅|❌|✅|❌
`0x14`|Aux. Vent. (On)|❌|✅|❌|✅|❌
`0x16`|Emergency Disarm|✅|❌|❌|❌|❌
`0x1a`|Timer (Lap)|✅|❌|❌|✅|❌
`0x1b`|Aux. Status|❌|❌|❌|✅|❌

# `0x24` Output String

Cluster `0x80` → Displays `0xe7`

## Properties

Variable length.

Property|Index|Length|Note
:---|:---|:---|:---
**Property**|`0`|`1`|_See table above_
**Unknown**|`1`|`1`|_Default `00`_
**String**|`2`|`-1`|_Length is fixed for given property_

### Examples

    80 0C E7 24 01 00 20 38 3A 33 31 50 4D 73           # Time
    80 0F E7 24 02 00 2D 2D 2F 2D 2D 2F 32 30 32 30 4E  # Date
    80 0A E7 24 03 00 2B 32 34 2E 35 7C                 # Temp.
    80 0F E7 24 04 00 32 30 2E 36 20 4C 2F 31 30 30 20  # Consump. 1
    80 0F E7 24 05 30 36 66 36 24 79 58 67 6C 2D 54 68  # Consump. 2
    80 0C E7 24 06 00 2D 2D 2D 20 4B 4D 20 62           # Range
    80 0D E7 24 07 00 33 34 33 38 20 4B 4D 20 43        # Distance
    80 0C E7 24 08 00 2D 2D 3A 2D 2D 20 20 7D           # Arrival
    80 0D E7 24 09 00 2D 2D 2D 20 4D 50 48 20 3F        # Limit
    80 0E E7 24 0A 00 20 30 2E 37 20 4B 4D 2F 48 0F     # Avg. Speed
    80 09 E7 24 0D 00 00 00 00 00 47                    # Code
    80 0F E7 24 0E 00 31 30 3A 31 30 20 4D 49 4E 20 32  # Timer
    80 0C E7 24 0F 00 31 30 3A 31 30 20 20 7A           # Aux. Timer 1
    80 0C E7 24 10 00 31 32 3A 30 36 41 4D 6C           # Aux. Timer 2
    80 0A E7 24 16 00 30 36 3A 30 30 63                 # Emer. Deact.
    80 0F E7 24 1A 00 32 34 2E 38 20 20 53 45 43 20 33  # Timer (Lap)

# `0x2A` Output Boolean

Cluster `0x80` → Displays `0xe7`

## Properties

Fixed length. Two byte bitfield.

    # Basically, 1 = ON, 0 = OFF.
    
    # Byte 1

    MEMO            = 0b0010_0000 << 8
    TIMER           = 0b0000_1000 << 8
    LIMIT           = 0b0000_0010 << 8
    
    # Byte 2
    
    CODE            = 0b0100_0000 << 0
    AUX_HEATING     = 0b0010_0000 << 0
    AUX_TIMER_2     = 0b0001_0000 << 0
    AUX_VENTILATION = 0b0000_1000 << 0
    AUX_TIMER_1     = 0b0000_0100 << 0

# `0x40` Input String

GT `0x3b` → Cluster `0x80`

## Properties

Property|Index|Length|Note
:---|:---|:---|:---
**Property**|`0`|`1`|_See table above_
**String**|`1`|`-1`|_Fixed length for given property_

### Examples

    3B 07 80 40 01 8A 2B 2D 71  # Time
    3B 07 80 40 02 19 03 14 F0  # Date
    3B 06 80 40 07 00 00 FA     # Distance
    3B 06 80 40 09 00 14 E0     # Sped Limit
    3B 06 80 40 0D 27 0F D8     # Code "9999"
    3B 06 80 40 0F 8B 00 79     # Aux. Timer 1
    3B 06 80 40 10 02 36 D9     # Aux. Timer 2


# `0x41` Input Boolean

GT `0x3b` → Cluster `0x80`

## Properties

Fixed length. Two byte bitfield.
    
    # Byte 1
    
    PROPERTY                = 0b0001_1111   # See table above

    # Byte 2

    REQUEST_STRING          = 0b0000_0001
    REQUEST_BOOLEAN         = 0b0000_0010
    ON_START                = 0b0000_0100
    OFF_STOP                = 0b0000_1000
    RECALCULATE             = 0b0001_0000
    SET_AS_CURRENT_SPEED    = 0b0010_0000
    
## Request String `0b0000_0001`
A request for a given property to be writen to the display. The cluster will reply with `0x24`.

This is most frequently used by GT at ignition to request trip computer properties.

Other properties are lazy loaded when user requests a display that requires the selected property, i.e. aux. timers.

## Request Boolean `0b0000_0010`

A request for the status of a given property. The cluster will reply with `0x2a`.

## On/Start `0b0000_0100`

The nuances of verbiage aside, basically "activate" the given property. There will be an applicable "activated" UI state.

- Memo: On.
- Speed Limit: On
- Timer: Start
- Aux. Timer 1: On
- Aux. Timer 2: On

**Aux. vent., aux. heating do not use these flags!**

## Off/Stop `0b0000_1000`

You guessed it... the opposite of On/Start!

## Recalculate `0b0001_0000`

Does what it says on the tin.

- Consump. 1
- Consump. 2
- Avg. Speed

## Set As Current Speed `0b0010_0000`

- Limit: set limit to current vehicle speed

## Overview

ID|Property|String|Boolean|On|Off|Recalc.|Set.
:--|-------|------|------|------|------|------|------
`0x01`|Time|✅|||||
`0x02`|Date|✅|||||
`0x03`|Temperature|✅|||||
`0x04`|Consump. 1|✅||||✅|
`0x05`|Consump. 2|✅||||✅|
`0x06`|Range|✅|||||
`0x07`|Distance|✅|||||
`0x08`|Arrival|✅|||||
`0x09`|Limit|✅|✅|✅|✅||✅
`0x0a`|Avg. Speed|✅||||✅|
`0x0b`|_PROG_||||||
`0x0c`|Memo|✅|✅|✅|✅||
`0x0d`|Code||✅||||
`0x0e`|Timer|✅|✅|✅|✅||
`0x0f`|Aux. Timer 1|✅|✅|✅|✅||
`0x10`|Aux. Timer 2|✅|✅|✅|✅||
`0x11`|Aux. Heat. (Off)|||⚠️|⚠️||
`0x12`|Aux. Heat. (On)|||⚠️|⚠️||
`0x13`|Aux. Vent. (Off)|||⚠️|⚠️||
`0x14`|Aux. Vent. (On)|||⚠️|⚠️||
`0x16`|Emergency Disarm||||||
`0x1a`|Timer (Lap)|✅|||||
`0x1b`|Aux. Status|✅|✅||||