**Note: this document will predominately reference the orignal UI.**
While the updated navigation UI is backwards compatible with earlier radios, it was designed to operate with the NG radios which were shipped prior to the update. There should be very few users with an MKIII navigation computer, and legacy radio.

## Overview

With respect to the UI, the earlier board monitor (BM) radios aren't all too different from those paired with a MID (and I would guess are probably backwards compatible with a MID). They behave as if writing to a MID, with strings formatted as such, but the GT will simply discard the string.

The radio relies upon two commands for the UI.

- `0x23` which is used to write the primary header/title, e.g.:
    - `FM 105.1 ST`
    - `CD 1-01`
    - `TAPE A <<R`
- `0x21` which adds supplemental information, e.g.:
    - `FMA`, `FM2`, `AM` selected analogue radio band
    - `TP` traffic program
    - `RND` CD shuffle

There is a common bitfield used by both commands to specify the source. 

    # Source bitmasks (3 bits)
    SOURCE_SERVICE  = 0x00 # 0b000 << 5
    SOURCE_WEATHER  = 0x20 # 0b001 << 5
    SOURCE_ANALOGUE = 0x40 # 0b010 << 5
    SOURCE_DIGITAL  = 0x60 # 0b011 << 5
    SOURCE_TAPE     = 0x80 # 0b100 << 5
    SOURCE_TRAFFIC  = 0xa0 # 0b101 << 5
    SOURCE_CDC      = 0xc0 # 0b110 << 5

Examples of common source bitmask:
    
    # Source: Analogue (0x40)
    68 <LEN> 3B 23 40 20 "FM 105.1" <CS>
    68 <LEN> 3B 21 41 06 60 " 1 \x05 2 \x05 3 \x05 4 \x05 5 \x05 6*" <CS>
    
    # Source: Tape (0x80)
    68 <LEN> 3B 23 80 <ARGS> <CHARS> <CS>
    68 <LEN> 3B 21 80 <ARGS> <CHARS> <CS>

However, be aware that the lower 5 bits are a bitfield for source specific options, so the byte value will not always equal the value of the above bitmasks.

    # Analogue radio with sensitive search "II"
    # 0b0100_0000   (0x40)   Source: Analogue
    # 0b0000_0011   (0x03)   Option: Search (sensitive) "II"
    
    # 0b0100_0000 OR 0b0000_0011 => 0x43
    # 68 <LENGTH> 3B 23 43 20 "AM 774" <CS>


### Service Mode

I've not seen reference to the service mode prior to MKII, however the UI was available with the MKI.

    SERIAL_NUMBER     = 0x02
    SOFTWARE_VERSION  = 0x03
    GAL               = 0x04
    F_Q               = 0x05
    DSP               = 0x06
    SEEK_LEVEL        = 0x07
    TP_VOLUME         = 0x08
    AF                = 0x09
    REGION            = 0x0a

##### Serial Number `0x02`
##### Software Version `0x03`
##### GAL `0x04`
##### F & Q `0x05`
##### DSP `0x06`
##### Seek Level `0x07`
##### TP Volume `0x08`
##### AF `0x09`
##### Region `0x0a`

### Weather Band
### Analogue Radio

#### Select Modes
    ANALOGUE_PRESET   = 0b0000_0001 # 0x41
    ANALOGUE_RDS      = 0b0000_0011 # 0x43

### Digital Radio

The later NG radio would come to use the digital radio layout for all sources.

### Tape
### Traffic
### CD