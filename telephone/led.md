# `0x2b` Telephone LEDs

The telephone indicator LEDs on the BMBT and MID are set with this command, which is sent to ANZV `0xe7`.

### Examples

    C8 04 E7 2B 00 00
    C8 04 E7 2B 10 10
    C8 04 E7 2B 14 14

## Properties

The message length is a fixed. The single data byte is a bitfield.
    
    LED_RED     = 0b0000_0011
    LED_YELLOW  = 0b0000_1100
    LED_GREEN   = 0b0011_0000
    
### Red `0b0000_0011`
    
    LED_RED_OFF         = 0b0000_0000
    LED_RED_ON          = 0b0000_0001
    LED_RED_BLINK       = 0b0000_0011

##### Example

    C8 04 E7 2B 01 01   # Red On
    C8 04 E7 2B 03 03   # Red Blink

### Yellow `0b0000_1100`

    LED_YELLOW_OFF      = 0b0000_0000
    LED_YELLOW_ON       = 0b0000_0100
    LED_YELLOW_BLINK    = 0b0000_1100

##### Example
    
    C8 04 E7 2B 04 04   # Yellow On
    C8 04 E7 2B 0C 0C   # Yellow Blink

### Green `0b0011_0000`

    LED_GREEN_OFF       = 0b0000_0000
    LED_GREEN_ON        = 0b0001_0000
    LED_GREEN_BLINK     = 0b0011_0000

##### Examples

    C8 04 E7 2B 10 10   # Green On
    C8 04 E7 2B 30 30   # Green Blink