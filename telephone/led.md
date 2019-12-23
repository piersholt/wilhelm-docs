# `0x2b` Telephone LEDs

The telephone sends LED settings to ANZV `0xe7` via command `0x2b`. The data is a fixed length of one byte, and is a bit field.

    # Telephone Status LEDs
    C8 04 E7 2B 00 00


Bit|7|6|5|4|3|2|1|0
:---|:---|:---|:----|:----|:---|:---|:---|:---
Use|-|-|Green|Green|Yellow|Yellow|Red|Red


    C8 04 E7 2B 00 <CS>   # 0b0000_0000 # All off

    C8 04 E7 2B 01 <CS>   # 0b0000_0001 # Red ON
    C8 04 E7 2B 03 <CS>   # 0b0000_0011 # Red BLINK

    C8 04 E7 2B 04 <CS>   # 0b0000_0100 # Yellow ON
    C8 04 E7 2B 0c <CS>   # 0b0000_1100 # Yellow BLINK

    C8 04 E7 2B 10 <CS>   # 0b0001_0000 # Green ON
    C8 04 E7 2B 30 <CS>   # 0b0011_0000 # Green BLINK

    # For any combination, apply bitwise OR.
    # Example: Red BLINK and Green ON
    # 0b0000_0011 | 0b0001_0000 = 0b0001_0011 (0x13)
    C8 04 E7 2B 13 <CS>
