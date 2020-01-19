# `0x15` Language & Region

This command is analogous to language and region settings found in desktop operating systems.

## User Configuration

![Settings](region/settings.jpg)

There are five configurable language/region settings available.

Setting|1|2|3|4|5|6|7|8|9
:---|:---|:---|:---|:---|:---|:---|:---|:---|:---
**Language**|DE|GB|US|IT|ES|JP|FR|CA|AR
**Distance**|km|miles|||||||
**Consumption**|l/100km|MPG|km/l||||||
**Temperature**|℃|℉|||||||
**Clock**|24h|12h|||||||
_Date_*|dd.mm|mm/dd|||||||

While each setting is global, each applicable property maintained by the IKE needs to be configured to use the selected unit/format. For example, selecting 24 hour time affects the *clock*, *navigation arrival time*, and *aux. timers*. This is outlined below:

Property|Clock|Distance|Temp.|Consump.
:---|:---|:---|:----|:----
Time|✅|||
Temperature|||✅|
Avg. Speed||✅||
Limit||✅||
Distance||✅||
Arrival|✅|||
Consump. 1||||✅
Consump. 2||||✅
Range||✅||
Aux. Timer 1|✅|||
Aux. Timer 2|✅|||

When a unit/format is selected, the GT will set the bits for _all_ applicable fields. However, it's possible to set the desired format/unit for individual properties if desired.

**Note on _Date_**
This is a meta setting; selecting *12h* will default to *mm.dd*. Similarly, selecting *dd/mm* will default to *24h*.

## Bitmasks
    
    # Byte 1
    LANGUAGE              = 0b0000_1111 << 32

    UNALLOCATED           = 0b1111_0000 << 32   # Unallocated
    
    # Byte 2
    FORMAT_TIME           = 0b0000_0001 << 16
    UNIT_TEMPERATURE      = 0b0000_0010 << 16
    CODING_OBC_RESUME     = 0b0000_0100 << 16
    CODING_OBC_SPEED      = 0b0000_1000 << 16

    UNIT_AVG_SPEED        = 0b0001_0000 << 16
    UNIT_LIMIT            = 0b0010_0000 << 16
    UNIT_DISTANCE         = 0b0100_0000 << 16
    FORMAT_ARRIVAL        = 0b1000_0000 << 16
    
    # Byte 3
    UNIT_CONSUMP_1        = 0b0000_0011 << 8
    UNIT_CONSUMP_2        = 0b0000_1100 << 8

    UNIT_RANGE            = 0b0001_0000 << 8
    FORMAT_AUX_TIMER_1    = 0b0010_0000 << 8
    FORMAT_AUX_TIMER_2    = 0b0100_0000 << 8
    CODING_MEMO_TYPE      = 0b1000_0000 << 8

    # Byte 4
    EQUIPPED_AUX_HEATING  = 0b0000_0001 << 0
    EQUIPPED_AUX_VENT     = 0b0000_0010 << 0
    UNALLOCATED           = 0b0000_0100 << 0    # Unallocated
    CODING_MOTOR_TYPE     = 0b0000_1000 << 0

    CODING_RCC_TIME       = 0b0001_0000 << 0  
    UNALLOCATED           = 0b0010_0000 << 0    # Unallocated
    EQUIPPED_AUX_CONTROL  = 0b0100_0000 << 0

## Byte 1

#### Language `0b0000_1111`

    LANG_DE             = 0b000_0000
    LANG_GB             = 0b000_0001
    LANG_US             = 0b000_0010
    LANG_IT             = 0b000_0011
    LANG_ES             = 0b000_0100
    LANG_JP             = 0b000_0101
    LANG_FR             = 0b000_0110
    LANG_CA             = 0b000_0111
    LANG_AR             = 0b000_1000

## Byte 2

#### Format: Time `0b0000_0001`

    TIME_24H            = 0b0000_0000   # 17:30
    TIME_12H            = 0b0000_0001   # 5:30pm

#### Format: Temperature `0b0000_0010 `

    TEMP_CELSIUS        = 0b0000_0000   # +18.0
    TEMP_FAHRENHEIT     = 0b0000_0010   # + 64

#### Unit: Average Speed `0b0001_0000 `

    AVG_SPEED_KMPH      = 0b0000_0000   # 100 KM/H
    AVG_SPEED_MPH       = 0b0001_0000   # 62 MPH

#### Unit: Limit `0b0010_0000`
    
    LIMIT_KMPH          = 0b0000_0000   # 100 KM/H
    LIMIT_MPH           = 0b0010_0000   # 62 MPH
    
#### Unit: Distance `0b0100_0000`

    DISTANCE_KM         = 0b0000_0000   # 100 KM
    DISTANCE_MILES      = 0b0100_0000   # 62 MLS

#### Format: Arrival Time `0b1000_0000`
    
    ARRIVAL_24H         = 0b0000_0000   # 17:30
    ARRIVAL_12H         = 0b1000_0000   # 5:30pm
    
## Byte 3

#### Unit: Consumption 1 `0b0000_0011`

    CONSUMP_1_L_100     = 0b0000_0000   # 39.5 L/100
    CONSUMP_1_MPG_UK    = 0b0000_0001   # 7.1 MPG
    CONSUMP_1_MPG_US    = 0b0000_0010   # 7.1 MPG
    CONSUMP_1_KM_L      = 0b0000_0011   # 2.5 KM/L

#### Unit: Consumption 2 `0b0000_1100`
    
    CONSUMP_2_L_100     = 0b0000_0000   # 39.5 L/100
    CONSUMP_2_MPG_UK    = 0b0000_0100   # 7.1 MPG
    CONSUMP_2_MPG_US    = 0b0000_1000   # 7.1 MPG
    CONSUMP_2_KM_L      = 0b0000_1100   # 2.5 KM/L
    
#### Unit: Range `0b0001_0000`
    
    RANGE_KM            = 0b0000_0000   # 100 KM
    RANGE_MILES         = 0b0001_0000   # 62 MLS

#### Format: Aux. Timer 1 `0b0010_0000`
    
    TIMER_1_24H         = 0b0000_0000   # 17:30
    TIMER_1_12H         = 0b0010_0000   # 5:30pm
    
#### Format: Aux. Timer 2 `0b0100_0000`
    
    TIMER_2_24H         = 0b0000_0000   # 17:30
    TIMER_2_12H         = 0b0100_0000   # 5:30pm
    
## Byte 4

#### Equipped: Aux. Heating `0b0000_0001`

    AUX_HEAT_FALSE      = 0b0000_0000
    AUX_HEAT_TRUE       = 0b0000_0001

#### Equipped: Aux. Ventilation `0b0000_0010`

    AUX_VENT_FALSE      = 0b0000_0000
    AUX_VENT_TRUE       = 0b0000_0010

#### Equipped: Aux. Controller (TBC)

    AUX_CONT_LEGACY     = 0b0100_0000