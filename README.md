# Wilhelm Documentation
---
## Radio
1. [Display Arbitration](radio/arbitration.md)

## Telephone
1. `0x02` Announce
1. `0x20` [Main Menu](telephone/main_menu.md)
1. `0x21` UI
	1. `0x00`[Default](telephone/layout/default.md)
	1. `0x05`[Pin-Code](telephone/layout/pin.md)
	1. `0x42`[Dial](telephone/layout/dial.md)
		1. [Last Numbers](telephone/layout/last_numbers.md)
	1. `0x43`[Directory](telephone/layout/directory.md)
	1. `0x80`[Top 8](telephone/layout/top_8.md)
	1. `0x90`[Info](telephone/layout/info.md)
	1. [SMS](telephone/layout/sms.md)
		1. `0xf0`[SMS Index](telephone/layout/sms/index.md)
		1. `0x01`[SMS Message/Emergency](telephone/layout/sms/message.md)
1. `0x2b` [Indicator Lamps](telephone/led.md)
1. `0x2c` [Status](telephone/status.md)
1. `0xa6` [SMS Icon](telephone/main_menu/icon.md)

## On-board Computer Control Panel (BMBT)

1. [Controls](telephone/controls/bmbt.md)
    1. `0x48` Buttons
    1. `0x47` "Soft" Buttons (i.e. INFO)
    1. `0x32` Volume Dial
    1. `0x49` Navigation Dial
1. `0x4f` [Monitor Control](bmbt/monitor.md)

## Multifunctional Steering Wheel (MFL)

1. [Controls](telephone/controls/mfl.md)
    1. `0x3b` Buttons
        1. Back/Forward
        1. Telephone
        1. "R/T"
    1. `0x32` Volume

## Cluster (IKE)

1. `0x15` [Region](ike/region.md)