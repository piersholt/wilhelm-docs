# Wilhelm Documentation
---

## Telephone
1. `0x02` Announce
1. `0x20` [Main Menu](telephone/main_menu.md)
1. `0x21` UI
	1. `0x00` [Default](telephone/layout/default.md)
	1. `0x05` [Pin-Code](telephone/layout/pin.md)
	1. `0x42` [Dial](telephone/layout/dial.md)
		1. [Last Numbers](telephone/layout/last_numbers.md)
	1. `0x43` [Directory](telephone/layout/directory.md)
	1. `0x80` [Top 8](telephone/layout/top_8.md)
	1. `0x90` [Info](telephone/layout/info.md)
	1. [SMS Overview](telephone/layout/sms.md)
		1. `0xf0` [SMS Index](telephone/layout/sms/index.md)
		1. `0x01` [SMS Message/Emergency](telephone/layout/sms/message.md)
1. `0x2b` [Telephone LEDs](telephone/led.md)
1. `0x2c` [Telephone Status](telephone/status.md)
1. `0xa6` [SMS Icon](telephone/icon.md)

## On-board Computer Control Panel (BMBT)

1. `0x4f` [Monitor Control](bmbt/monitor.md)

#### Controls
1. `0x48` [Buttons](bmbt/controls.md)
1. `0x47` ["Soft" Buttons (i.e. INFO)](bmbt/controls.md)
1. `0x32` [Volume Dial](bmbt/controls.md)
1. `0x49` [Navigation Dial](bmbt/controls.md)


## Multifunctional Steering Wheel (MFL)

#### Controls
1. `0x3b` [Buttons](mfl/controls.md)
1. `0x32` [Volume](mfl/controls.md)

## Cluster (IKE)

1. `0x11` [Ignition](ike/ignition.md)
1. `0x15` [Language & Region](ike/region.md)

#### Redundant Data Storage
1. `0x53` [Redundant Data Request](ike/redundant.md)
1. `0x54` [Redundant Data](ike/redundant.md)
1. `0x55` [Replicate Data](ike/redundant.md)
