# `0x1f` GPS Time

With sufficient GPS signal strength, the navigation computer will begin sending GPS [date and] time.

- Dependent on GPS signal
- Time is expressed as a **24-hour clock**
- Time is in **UTC**
- Sent at the **top of every minute**, e.g. `17:23:00`, `17:24:00`
- The message recipient is the instrument cluster `0x80`
- The message length is fixed at 13 bytes

## Examples

    7F 0B 80 1F 40 07 16 26 00 01 20 19 A4
    7F 0B 80 1F 40 05 40 18 00 01 20 19 CE
    7F 0B 80 1F 40 12 30 17 00 03 20 00 BD

## Properties

Property|Index|Length|Type|Note
:---|:---|:---|:---|:---
**Unknown**|`0`|`1`|-|Default of `0x40`?
**Hour**|`1`|`1`|Packed BCD| `hh`
**Minute**|`2`|`1`|Packed BCD| `mm`
**Day**|`3`|`1`|Packed BCD| `DD`
**Unknown**|`4`|`1`|-|Default of `0x00`?
**Month**|`5`|`1`|Packed BCD| `MM`
**Year**|`6`|`2`|Packed BCD| `YYYY`

### Example

    7F 0B 80 1F 40 10 18 27 00 01 20 19 BC  # GPST frame
        
Property|--|Hour|Minute|Day|--|Month|Year
---|---|---|---|---|---|---|---
**Data**|`40`|`10`|`18`|`27`|`00`|`01`|`2019`

**Time**: 10:18am
**Date**: 27 January 2019

**ISO 8601**: `2019-01-27T10:18:00+00:00`

## GPS Week Number Rollover

As of *7 April 2019*, navigation computers shipped from 1999, or older units that have been updated since ~1999, will no longer report the correct date.

![GPS Status Date Error](gpst/gps_status_date_error.jpg)

An example of this above, whereby an MK4 (`4-1/00`) navigation computer in service mode is reporting an incorrect date of **1 June 2000** (`01.06.00`) on  **16 January 2020** (`16.01.2020`).

This is a result of [GPS week number rollover](https://en.wikipedia.org/wiki/GPS_Week_Number_Rollover), a known limitation in GPS.

### The Problem

GPS expresses time as:

- **number of weeks** since the GPS epoch on 6 January 1980
- **number of seconds** into the given week

The number of weeks is represented by a 10-bit integer, and herein lies the problem.

10 bits allows for 1024 possible values (`2^10`), or 0 to 1023 weeks since the GPS epoch. Thus, on 21 August 1999, after 1024 weeks, or ~19.7 years, the GPS date would effectively reset.

GPS obsolesence not withstanding, this reset or rollover will occur every 1024 weeks in perputuity, and as of January 2020, has occured twice.

Epoch|Start|End|Duration
:---|:---|:---|:---
**1**|`1980-01-06`|`1999-08-21`|1024 weeks
**2**|`1999-08-22`|`2019-04-06`|1024 weeks
**3**|`2019-04-07`|`...`|`...`

### The Solution

It is the responsibility of GPS receivers to correct the date for the current epoch. and presumably a navigation OS software update was released in anticipation of the first rollover event in 1999, but in the absence of another update, the navigation computer will continue to calculate the date as if GPS is in the second epoch.

However, the date correction can be handled by applying the same logic that is otherwise the responsibility of the navigation computer.

As of `V30` or `4-1/00`, navigation computers should be configured for epoch 2. So to correct for epoch 3, the reported date can simply be offset by 1 epoch. `2 + 1 = 3 # Wow! :D`

In the case of ruby, the base unit for time is seconds, so to get a period of 1 epoch, calculate the number of seconds in one week, and multiply it by 1024.

    epoch_size      = 2**10                 # 1024
    week_secs       = 60 * 60 * 24 * 7      # 604800 seconds

    epoch_offset = epoch_size * week_secs   # 619315200 seconds (1024 weeks)

The date reported by the navigation computer can be offset by 1 epoch:
    
    gpst = Time.new("2000-06-01 06:52")     # 1 June 2000
    corrected_gpst = gpst + epoch_offset    # Offset by 1 epoch
    print corrected_gpst                    # 16 January 2020

*Drive off into sunset.*