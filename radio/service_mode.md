# Radio: Service Mode

## Parameters
    
    SOURCE  = 0b1110_0000
    CONFIG  = 0b0001_1111

### Source `0b1110_0000`

    SOURCE_SERVICE    = 0b000 << 5  # 0x00

### Config `0b0001_1111`
    
    CONFIG_SERIAL_NUMBER    =  0b0_0010
    CONFIG_SOFTWARE_VERSION =  0b0_0011
    CONFIG_GAL              =  0b0_0100
    CONFIG_FQ               =  0b0_0101
    CONFIG_DSP              =  0b0_0110
    CONFIG_SEEK_LEVEL       =  0b0_0111
    CONFIG_TP_VOLUME        =  0b0_1000
    CONFIG_AF               =  0b0_1001
    CONFIG_REGION           =  0b0_1010

## Use Cases

The MK1 GT has support for service mode despite C23 not using it?

Parameters           |Description
:--------------------|:----------
**Serial Number**    | Displays the radio serial number. (PN?)
**Software Version** | Displays the radio software version in format (mm/yy?)
**GAL**              | Speed dependent volume control
**F & Q**            | Field Strength (F) & Quality (Q)
**DSP**              | DSP
**Seek Level**       | ???
**TP Volume**        | Provides adjustment for traffic report minimum value.
**AF**               | Alternative-frequency radio setting
**Region**           | View/edit radio region.