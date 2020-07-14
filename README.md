# Wilhelm Documentation

*Documentation for the I/K-Bus protocol found in BMW vehicles from 1989 to 2013.*

## Introduction

This documentation covers the common functions of the I-Bus and K-Bus.

P-Bus, and M-Bus are not covered. D-Bus is also not discussed, although it may be added in the future.

This is an ongoing project, and the documentation will be expanded as time allows.

#### Warning!

This documentation should not be considered authouratative. While great care, and effort has been taken in creating it, if you choose to use it, you do so at your own risk.

## Contents

1. [Applicable Models](#applicable-models)
1. [Glossary](#glossary)
1. Device Index
    1. [K/I-Bus](#ki-bus)
    1. [D-Bus](#d-bus)
1. [Command Index](#command-index)
1. Commands by Device
    1. [Telephone](#telephone)
    1. [On-board Monitor Control Panel](#on-board-computer-control-panel-bmbt)
    1. [Multi-function Steering Wheel](#multifunctional-steering-wheel-mfl)
    1. [Instrument Cluster](#instrument-cluster-ike)
    1. [Navigation](#navigation)


## Applicable Models

This protocol applies to the bus system in the models listed below.

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

MINI and Range Rover (early L322) implementations are not discussed.

## Glossary

#### **Body [Karosserie] Bus** (K-Bus)
> K-Bus was added to the E38 along with the I-Bus. Models without Navigation or IKE will use the K-Bus only. Both of these bus systems are technically identical, the only difference is their use by model.

#### **Diagnosis Bus** (D-Bus)
> The D-Bus was introduced as TXD (and RXD) in 1987. The term D-Bus was adopted with the introduction of the E38 in 1995, however it is still referred to as TXD in the ETM [electrical troubleshooting manual].
>
> All modules in the vehicle are not connected directly to the D-Bus, some systems are connected through a gateway such as the IKE or cluster. The gateway handles all diagnostic “traffic” and routes the necessary information to the correct bus system.
 
#### **Gateway**
> On vehicles equipped with an I-Bus (E38, E39, E53 High) messages to be sent back and forth between the K-Bus and I-Bus have to be transferred via a Gateway. This Gateway is the IKE. The IKE determines by the address of the message recipient whether the message needs to be passed along to the other bus.

#### **Instrument Bus** (I-Bus)
> I-Bus was introduced on the E31 as the **information bus**. The E31 version of the I-Bus was used for body electronics and driver information systems. With the introduction of the E38, the I-Bus is now referred to as the **instrument bus**.

#### **M-Bus**
> The M-Bus is used exclusively in the climate control systems for the control of the “smart:” stepper motors. These stepper motors are used to control various air distribu- tion flaps.
>
> The M-Bus was introduced on the E38 climate control system (IHKA). The M-Bus was also installed on subsequent models equipped with IHKA and IHKR.

#### **Peripheral Bus** (P-Bus)> The P-Bus is a single wire serial communications bus that is used exclusively on vehicle that are equipped with ZKE III. These vehicles are the E38, E39 and E53.
>
> The P-Bus provides the Central Body Electronics system with a low speed bus for use by the General Module (GM) to control various functions. 

## Device Index

- 8-bit addressing (256 unique addressess).
- Multicast, and broadcast addresses.
- Addresses are preassigned, and static.
- All buses are within the 8-bit scope, i.e. an address is unique across the I, K, and D buses.
- Variants of a device will have the same address, e.g. the address `0x80` is used by the low cluster (KOMBI), high clusters (IKE, IKI).
- The adress pool is shared by all models that utilise this bus system. An address is rarely reallocated even if the originally allocated device is not applicable to a new model.

### K/I-Bus

Device|Bus|Description
------|---|-----------
`0x00`|K|General Body Electronics (ZKE 3/4/5)
`0x08`|K|Tilt/Slide Sunroof (SHD)
`0x18`|K/I|CD Changer (CDC)
`0x24`|K|Trunk Lid Module (HKM) [E38]
`0x28`|I|Radio Clock Control (RCC) [E38]
`0x2e`|K|Electronic Damper Control (EDC)
`0x30`|I|Check Control Module (CCM) [E38]
`0x3b`|I|Graphics Stage (GT)
`0x3f`|K/I|Diagnostics (via [gateway](#gateway))
`0x40`|K|Remote Control for Central Locking (FBZV) [E31]
`0x43`|I|Unconfirmed: Rear Graphics Stage (GT) [E38]
`0x44`|K|Drive Away Protection System (EWS)
`0x45`|K|Anti-Theft System (DWA)
`0x46`|I|Central Information Display (CID) [E83, E85]
`0x47`|I|Rear Control Panel (FONT_BT) [E38]
`0x48`|?|Telephone (Japan)
`0x50`|K/I|Multifunction Steering Wheel (MFL)
`0x51`|K|Mirror Memory: Passenger [E46]
`0x53`|K/I|Unconfirmed: Multicast 📣
`0x5b`|K|Automatic Heating/Air Conditioning (IHKA)
`0x60`|K/I|Park Distance Control (PDC)
`0x66`|K|Active Light Control (ALC)
`0x68`|K/I|Radio
`0x69`|K|Electronic Body Module (EKM) [E31]
`0x6a`|K/I|Digital Sound Processor (DSP)
`0x6b`|K|Auxiliary Heater "Webasto"
`0x70`|K|Tire Pressure Control (RDC), Deflation Warning System (DWS)
`0x71`|K|Seat Memory: Driver [E31, E34]
`0x72`|K|Seat Memory: Driver [E46, E53]
`0x76`|K|CD Player (Business)
`0x7f`|K/I|Navigation
`0x80`|K/I|Instrument Cluster (IKE/KOMBI)
`0x9a`|K/I|Automatic Headlight Vertical Aim Control (LWR)
`0x9b`|K|Mirror Memory: Driver [E46], Convertible soft top module (CVM) [E36]
`0x9c`|K|Convertible Soft Top Module (CVM) [E46]
`0x9d`|K|Electronic disconnecting switch (ETS) [E38]
`0xa0`|I|Rear Multi-functional Display (MID) [E38]
`0xa4`|K|Multiple Restraint System (MRS)
`0xa7`|K|Rear Compartment Heating/Air Conditioning
`0xac`|K|Electronic Height Control (EHC)
`0xb0`|K/I|Speech Input System (SES)
`0xb9`|K|Compact Remote Control (RF/IR)
`0xbb`|K/I|Navigation (Japan)
`0xbf`|K|Broadcast 📣
`0xc0`|K/I|Multi-functional Display (MID)
`0xc8`|K/I|Telephone
`0xcd`|K|Multi-functional Display (OBC) [E31]
`0xda`|K|Seat Memory: Passenger [E46]
`0xd0`|K/I|Lamp Check Module (LCM), Light Switch Center (LSZ)
`0xe0`|K|Integrated Radio and Information System (IRIS)
`0xe7`|K/I|Multicast: Displays 📣
`0xe8`|K|Rain/Driving Light Sensor (RLS)
`0xea`|I|DSP Controler [E38]
`0xed`|I|Video Module
`0xf0`|I|On-board Computer Control Panel (BMBT)
`0xf5`|K|Lamp control module (LKM2) [E31]
`0xff`|K/I|Broadcast 📣

### D-Bus

The shared address space might suggest it's possible to communicate with D-Bus devices from the K/I-Bus, however that's not the case. This is purely a function of diagnostics, in which all devices must be addressable from the D-Bus.

Device|Bus|Description
------|---|-----------
`0x10`|D|Engine Management
`0x11`|D|Central Body Electronics (ZKE 1/2) [E31, E34]
`0x12`|D|Engine Management
`0x13`|D|Engine Management
`0x14`|D|Engine Management
`0x15`|D|Double Sunroof (DDSHD) [E34]
`0x16`|D|Thermal Level Oil Sensor [E36]
`0x19`|D|*Range Rover*
`0x20`|D|Electronic Engine Power Control (EML) [M70]
`0x21`|D|Central locking module [E34, E36]
`0x22`|D|Electronic Engine Power Control (EML) [M73]
`0x31`|D|*MINI*
`0x32`|D|Gearbox Control
`0x35`|D|Steering Column Memory (LSM) [E31/E32/E34]
`0x36`|D|ABS/ASC (Concept 1/2)
`0x56`|D|ABS/ASC/DSC (DS2)
`0x57`|D|Steering Angle Sensor (LWS)
`0x59`|D|Automatic Heating/Air Conditioning (IHKA) [E31, E36]
`0x5a`|D|Electric Steering Lock (ELV) [E52]
`0x65`|D|Fuel Pump (EKP)
`0x6c`|D|Gearbox Control
`0x74`|D|Seat Occupation Detection US (OC3) [E83, 85]
`0x81`|D|*MINI*
`0x86`|D|Active Rear Axle Kinematics (AHK) [E31]
`0x9e`|D|Rollover Sensor [E36]
`0xa6`|D|Cruise Control
`0xc2`|D|Servotronic (SVT)
`0xce`|D|Seat Occupancy Detection

## Command Index

Command|Description
:--|:--
`0x01`|Ping
`0x02`|[Pong & Announce](announce.md)
`0x10`|[Ignition Request](ike/ignition_request.md)
`0x11`|[Ignition](ike/ignition.md)
`0x12`|Sensors Request
`0x13`|Sensors
`0x14`|[Language & Region Request](ike/region_request.md)
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
`0x24`|[OBC Text](ike/24.md)
`0x27`|IKE → MID (TBC)
`0x2a`|[OBC Status](ike/2a.md)
`0x2b`|[Telephone LEDs](telephone/led.md)
`0x2c`|[Telephone Status](telephone/status.md)
`0x31`|Menu Button
`0x32`|[BMBT Volume](bmbt/32.md) & [MFL Volume](mfl/32.md)
`0x34`|DSP Control
`0x36`|Radio EQ.
`0x37`|Radio Tone/Select
`0x38`|CDC Status Request
`0x39`|CDC Status
`0x3b`|[MFL Buttons](mfl/3b.md)
`0x40`|[OBC Input](gt/40.md)
`0x41`|[OBC Control](gt/41.md)
`0x42`|[Remote Control](ike/prog.md)
`0x45`|Radio UI Request
`0x46`|Radio UI
`0x47`|[BMBT "Soft" Buttons](bmbt/47.md)
`0x48`|[BMBT Buttons](bmbt/48.md)
`0x49`|[BMBT Navigation Dial](bmbt/49.md)
`0x4a`|Tape Control/Radio LED
`0x4b`|Tape Status
`0x4e`|GT → Radio (TBC)
`0x4f`|[BMBT Monitor Control](bmbt/monitor.md)
`0x50`|Check Control Status Request
`0x51`|Check Control Status
`0x52`|Check Control Message Relay
`0x53`|[Redundant Data Request](ike/53.md)
`0x54`|[Redundant Data](ike/54.md)
`0x55`|[Replicate Data](ike/55.md)
`0x57`|Check Control/Remote Control Buttons
`0x59`|Rain/driving Lights Status
`0x5a`|Lamp Status Request
`0x5b`|Lamp Status
`0x5c`|Instrument Backlighting (58G)
`0x5d`|Instrument Backlighting (58G) Request
`0x61`|EHC → GLO (TBC)
`0x70`|MRS → GLO (TBC)
`0x71`|Remote (Keyless) Entry Request
`0x72`|Remote (Keyless) Entry
`0x73`|Key Status Request
`0x74`|Key Status
`0x75`|RLS → GM (TBC)
`0x76`|Remote (Keyless) Entry (TBC)
`0x77`|GM → RLS (TBC)
`0x78`|Memory
`0x79`|Door Status Request
`0x7a`|Door Status
`0x7c`|SHD → GLO (TBC)
`0x7d`|GM → SHD (TBC)
`0x82`|IHKA → GLO (TBC)
`0x83`|IHKA → IKE (TBC)
`0x86`|IHKA → Nav. (TBC)
`0x87`|Nav. → IHKA (TBC)
`0x9e`|GT → RCM (TBC)
`0xa2`|[Telematics Coordinates](nav/a2.md)
`0xa4`|Telematics Location
`0xa5`|Body Text (Telematics, MP3)
`0xa6`|[SMS Icon](telephone/icon.md)
`0xa7`|Traffic Management Channel Request
`0xa8`|Traffic Management Channel
`0xa9`|BMW Assist Data
`0xaa`|Rear Nav. Control
`0xab`|Forward Nav. Control
`0xaf`|Nav. → SES (TBC)

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
1. `0x48` [Buttons](bmbt/48.md)
1. `0x47` ["Soft" Buttons (i.e. INFO)](bmbt/47.md)
1. `0x32` [Volume Dial](bmbt/32.md)
1. `0x49` [Navigation Dial](bmbt/49.md)

## Multifunctional Steering Wheel (MFL)

##### Controls
1. `0x3b` [Buttons](mfl/3b.md)
1. `0x32` [Volume](mfl/32.md)

## Instrument Cluster (IKE)

1. `0x10` [Ignition Request](ike/ignition_request.md)
1. `0x11` [Ignition](ike/ignition.md)
1. `0x14` [Language & Region Request](ike/region_request.md)
1. `0x15` [Language & Region](ike/region.md)
1. `0x42` [Remote Control](ike/prog.md)

##### Redundant Data Storage
1. `0x53` [Redundant Data Request](ike/53.md)
1. `0x54` [Redundant Data](ike/54.md)
1. `0x55` [Replicate Data](ike/55.md)

## Navigation

1. `0x02` [Announce](announce.md#nav-computer-0x7f)
1. `0x1f` [GPS Time](nav/gpst.md)