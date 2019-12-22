# `0x4f` Monitor

This command is used to control the monitor integrated into the BMBT. It's used by both GT, and TV.

It's very helpful when debugging various navigation computers, and video modules on a testbench. The extra byte used by **TV** `0xed` to control *aspect ratio*, and *encoding*, can be included in commands issued by **GT** `0x3b`.

## Byte 1: Power, Source

Most **GT** messages will only have this byte.

Bit|7|6|5|4|3|2|1|0
:---|:---|:---|:----|:----|:---|:---|:---|:---
Use|-|-|-|Power|-|-| Source |Source

    # Power 
    POWER_OFF     = 0b0000_0000
    POWER_ON      = 0b0001_0000

    # Source
    SOURCE_NAV_GT = 0b0000_0000
    SOURCE_TV     = 0b0000_0001
    SOURCE_VID_GT = 0b0000_0010


### Power

The **GT** will switch the monitor on at ignition position 1 (KL-R).
   
### Source

The input source switching in handled by the video module, but each source has it's own brightness settings.

### GT `0x3b` Examples

    3B 04 F0 4F 10 90   # Monitor on at KL-R
    3B 04 F0 4F 00 80   # Select "Monitor Off"

## Byte 2 (Optional): Aspect Ratio, Encoding

**TV** `0xed` has both aspect ratio, and encoding settings available when TV is the selected source.


Bit|7|6|5|4|3|2|1|0
:---|:---|:---|:----|:----|:---|:---|:---|:---
Use|-|-|Aspect Ratio|Aspect Ratio|-|-|Encoding|Encoding

    # Aspect Ratio
    ASPECT_4_3    = 0b0000_0000
    ASPECT_16_9   = 0b0001_0000
    ASPECT_ZOOM   = 0b0011_0000

    # Encoding
    ENCODING_NTSC = 0b0000_0001
    ENCODING_PAL  = 0b0000_0010
    
### Aspect Radio

### Encoding

Encoding issues are commonly seen when switching between various navigation computers, or video modules as there did seem to be a transition between PAL and NTSC as the encoding for navigation computer video. Incorrect encoding is usually denoted by "scrolling" video image.

### TV `0xed` Examples

    ED 05 F0 4F 11 12 54 # Open "Television" (On, TV, 16x9, NTSC)
    ED 05 F0 4F 12 11 54 # Return to Main Menu (On, Nav. GT, 16x9, PAL)