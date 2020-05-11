# Wilhelm Documentation

## Overview

Instrument (I-Bus), and Body (K-Bus) protocol documentation.

While great care, and effort has been taken in creating this documentation, it's important to note the following:

This documentation is **not authoritive**.

- I am not affiliated with BMW or it's partners
- the protocol was reverse engineered while developing [Walter](https://github.com/piersholt/walter)
- the functionality is a deducation at best (as with any black box system)
- use at your own risk!

This documentation is **not comprehensive**.

- many commands are simply yet to be documented
- given the number of models, it's not realistic to test all equipment (i.e. there is more than 10 variants of instrument cluster)
- some equipment is hard to access due to rarity, or value. *"Would you mind terribly if I dismantled your Z8?"*
- equipment can be region dependent (i.e. Traffic Management Channel), or completely obsolete (i.e. factory telephone), both of which hamper testing

## Contents

1. [Applicable Models](#)
1. [Terminology](#)
1. Commands by Function
 1. [Telephone](#)
 1. [On-board Monitor Control Panel](#)
 1. [Multi-function Steering Wheel](#)
 1. [Instrument Cluster](#)
 1. [Navigation](#)
1. [Command Index](#command-index)  

## Applicable Models

This protocol applies to the bus system in the models listed below.

MINI and Range Rover (early L322) implementations are not covered owing to lack of familiarity.

Model|Series|Period|I-Bus|K-Bus
:--|:--|:--|:--|:--
E31|8 Series|1989 - 1999|✅|
E38|7 Series|1999 - 2001|✅|✅
E39|5 Series|1995 - 2004|✅|✅
E46|3 Series|1997 - 2006||✅
E52|Z8|2000 - 2003||✅
E53|X5|1999 - 2006|✅|✅|
E83|X3|2003 - 2010||✅
E85|Z4|2002 - 2008||✅
E87|1 series|2004 - 2013||✅

## Terminology

- **I-Bus** (Instrument Bus)
> I-Bus was introduced on the E31 as the information bus. The E31 version of the I-Bus was used for body electronics and driver information systems. With the introduction of the E38, the I-Bus is now referred to as the instrument bus.
 
- **K-Bus** (Karosserie "Body" Bus)
> K-Bus was added to the E38 along with the I-Bus. Models without Navigation or IKE will use the K-Bus only. Both of these bus systems are technically identical, the only difference is their use by model.
 
- **Gateway**
> On vehicles equipped with an I-Bus (E38, E39, E53 High) messages to be sent back and forth between the K-Bus and I-Bus have to be transferred via a Gateway. This Gateway is the IKE. The IKE determines by the address of the message recipient whether the message needs to be passed along to the other bus.

## Index

Command|Reference
:--|:--
`0x01`|Ping
`0x02`|[Pong & Announce (alive and wake?)](announce.md)
`0x10`|[Ignition Request](ike/ignition.md)
`0x11`|[Ignition](ike/ignition.md)
`0x12`|Sensors Request
`0x13`|Sensors
`0x14`|[Language & Region Request](ike/region.md)
`0x15`|[Language & Region](ike/region.md)
`0x16`|Mileage Request
`0x17`|Mileage
`0x18`|Speed
`0x19`|Temperature
`0x1a`|Check Control Message
`0x1b`|Check Control Message Buffer
`0x1d`|Temperature Request
`0x1f`|[GPS Time](nav/gpst.md)
`0x20`|MID Button
`0x21`|Menu Text
`0x22`|Menu Text Buffer
`0x23`|Title Text
`0x24`|Variable Output
`0x2a`|Boolean Output
`0x2b`|[Telephone LEDs](telephone/led.md)
`0x2c`|[Telephone Status](telephone/status.md)
`0x31`|Menu Button
`0x32`|[BMBT Volume (Dial)](bmbt/controls.md) & [MFL Volume (Buttons)](mfl/controls.md)
`0x34`|DSP Control
`0x36`|Radio EQ.
`0x37`|Radio Tone/Select
`0x38`|CDC Status Request
`0x39`|CDC Status
`0x3b`|[MFL Buttons](mfl/controls.md)
`0x40`|Variable Input
`0x41`|Boolean Input
`0x42`|[Remote Control](ike/prog.md)
`0x45`|Radio UI Request
`0x46`|Radio UI
`0x47`|[BMBT "Soft" Buttons](bmbt/controls.md)
`0x48`|[BMBT Buttons](bmbt/controls.md)
`0x49`|[BMBT Navigation Dial](bmbt/controls.md)
`0x4a`|Tape Control/Radio LED
`0x4b`|Tape Status
`0x4f`|[BMBT Monitor Control](bmbt/monitor.md)
`0x50`|Check Control Status Request
`0x51`|Check Control Status
`0x52`|Check Control Message Relay
`0x53`|[Redundant Data Request](ike/redundant.md)
`0x54`|[Redundant Data](ike/redundant.md)
`0x55`|[Replicate Data](ike/redundant.md)
`0x57`|Check Control/Remote Control Buttons
`0x59`|Rain/driving Lights Status
`0x5a`|Lamp Status Request
`0x5b`|Lamp Status
`0x5c`|Instrument Backlighting (58G)
`0x5d`|Instrument Backlighting (58G) Request
`0x71`|Remote (Keyless) Entry Request
`0x72`|Remote (Keyless) Entry
`0x73`|Key Status Request
`0x74`|Key Status
`0x78`|Memory
`0x79`|Door Status Request
`0x7a`|Door Status
`0xa2`|Telematics Coordinates
`0xa4`|Telematics Location
`0xa5`|Body Text (Telematics, MP3)
`0xa6`|[SMS Icon](telephone/icon.md)
`0xa7`|Traffic Management Channel Request
`0xa8`|Traffic Management Channel

## Telephone
1. `0x02` [Announce](announce.md#telephone-0xc8)
1. `0x20` [Main Menu](telephone/main_menu.md)
1. `0x21` UI
	1. `0x00` [Default](telephone/layout/default.md)
	1. `0x05` [Pin-Code](telephone/layout/pin.md)
	1. `0x42` [Dial](telephone/layout/dial.md)
		1. [Last Numbers](telephone/layout/last_numbers.md)
	1. `0x43` [Directory](telephone/layout/directory.md)
	1. `0x80` [Top 8](telephone/layout/top_8.md)
	1. `0x90` [Info](telephone/layout/info.md)
	1. `0xf0` [SMS Index](telephone/layout/sms/index.md)
	1. `0xf1` [SMS Message/Emergency](telephone/layout/sms/message.md)
1. `0x2b` [Telephone LEDs](telephone/led.md)
1. `0x2c` [Telephone Status](telephone/status.md)
1. `0xa6` [SMS Icon](telephone/icon.md)

1. Appendix
    1. [SMS Overview](telephone/layout/sms.md)

## On-board Computer Control Panel (BMBT)

1. `0x02` [Announce](announce.md#bmbt-0xf0)
1. `0x4f` [Monitor Control](bmbt/monitor.md)

##### Controls
1. `0x48` [Buttons](bmbt/controls.md)
1. `0x47` ["Soft" Buttons (i.e. INFO)](bmbt/controls.md)
1. `0x32` [Volume Dial](bmbt/controls.md)
1. `0x49` [Navigation Dial](bmbt/controls.md)

## Multifunctional Steering Wheel (MFL)

##### Controls
1. `0x3b` [Buttons](mfl/controls.md)
1. `0x32` [Volume](mfl/controls.md)

## Instrument Cluster (IKE)

1. `0x11` [Ignition](ike/ignition.md)
1. `0x14` [Language & Region Request](ike/region.md0x14-language--region-request)
1. `0x15` [Language & Region](ike/region.md#0x15-language--region)
1. `0x42` [Remote Control](ike/prog.md)

##### Redundant Data Storage
1. `0x53` [Redundant Data Request](ike/redundant.md)
1. `0x54` [Redundant Data](ike/redundant.md)
1. `0x55` [Replicate Data](ike/redundant.md)

## Navigation

1. `0x02` [Announce](announce.md#nav-computer-0x7f)
1. `0x1f` [GPS Time](nav/gpst.md)