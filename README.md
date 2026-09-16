# Wilhelm Documentation

*Documentation for the I/K-Bus protocol found in BMW vehicles from 1989 to 2013.*

## Introduction

This documentation covers the common functions of the I-Bus and K-Bus.

P-Bus, and M-Bus are not covered. D-Bus is also not discussed, although it may be added in the future.

This is an ongoing project, and the documentation will be expanded as time allows.

#### Warning!

This documentation should not be considered authoritative. While great care, and effort has been taken in creating it,
if you choose to use it, you do so at your own risk.

## Contents

1. [Applicable Models](#applicable-models)
2. [Glossary](#glossary)
3. Device Index
    1. [K/I-Bus](#ki-bus)
    2. [D-Bus](#d-bus)
4. [Command Index](#command-index)
5. Features
    1. [Sensors](#sensors)
    2. [OBC](#obc)
    3. [Redundant Data Storage](#redundant-data-storage)
    4. [Controls](#controls)
    5. [Radio](#radio)
    6. [Telephone](#telephone)
    7. [TCU and BMW Assist](#tcu-and-bmw-assist)
    8. [Navigation](#navigation)
    9. [Lighting](#lighting)
    10. [Body](#body)

## Applicable Models

This protocol applies to the bus system in the models listed below.

| Model | Series   | Period      | I-Bus | K-Bus |
|-------|:---------|:------------|:------|:------|
| E31   | 8 Series | 1989 - 1999 | ✅     |       |
| E38   | 7 Series | 1999 - 2001 | ✅     | ✅     |
| E39   | 5 Series | 1995 - 2004 | ✅     | ✅     |
| E46   | 3 Series | 1997 - 2006 |       | ✅     |
| E52   | Z8       | 2000 - 2003 |       | ✅     |
| E53   | X5       | 1999 - 2006 | ✅     | ✅     ||
| E83   | X3       | 2003 - 2010 |       | ✅     |
| E85   | Z4       | 2002 - 2008 |       | ✅     |
| E87   | 1 series | 2004 - 2013 |       | ✅     |

MINI and Range Rover (early L322) implementations are not discussed.

## Glossary

#### **Body [Karosserie] Bus** (K-Bus)

> K-Bus was added to the E38 along with the I-Bus. Models without Navigation or IKE will use the K-Bus only. Both of
> these bus systems are technically identical, the only difference is their use by model.

#### **Diagnosis Bus** (D-Bus)

> The D-Bus was introduced as TXD (and RXD) in 1987. The term D-Bus was adopted with the introduction of the E38 in
> 1995, however it is still referred to as TXD in the ETM [electrical troubleshooting manual].
>
> All modules in the vehicle are not connected directly to the D-Bus, some systems are connected through a gateway such
> as the IKE or cluster. The gateway handles all diagnostic “traffic” and routes the necessary information to the
> correct
> bus system.

#### **Gateway**

> On vehicles equipped with an I-Bus (E38, E39, E53 High) messages to be sent back and forth between the K-Bus and I-Bus
> have to be transferred via a Gateway. This Gateway is the IKE. The IKE determines by the address of the message
> recipient whether the message needs to be passed along to the other bus.

#### **Instrument Bus** (I-Bus)

> I-Bus was introduced on the E31 as the **information bus**. The E31 version of the I-Bus was used for body electronics
> and driver information systems. With the introduction of the E38, the I-Bus is now referred to as the **instrument bus
**.

#### **M-Bus**

> The M-Bus is used exclusively in the climate control systems for the control of the “smart:” stepper motors. These
> stepper motors are used to control various air distribution flaps.
>
> The M-Bus was introduced on the E38 climate control system (IHKA). The M-Bus was also installed on subsequent models
> equipped with IHKA and IHKR.

#### **Peripheral Bus** (P-Bus)

> The P-Bus is a single wire serial communications bus that is used exclusively on vehicle that are equipped with ZKE
> III. These vehicles are the E38, E39 and E53.
>
> The P-Bus provides the Central Body Electronics system with a low speed bus for use by the General Module (GM) to
> control various functions.

## Device Index

- 8-bit addressing (256 unique addressess).
- Multicast, and broadcast addresses.
- Addresses are preassigned, and static.
- All buses are within the 8-bit scope, i.e. an address is unique across the I, K, and D buses.
- Variants of a device will have the same address, e.g. the address `0x80` is used by the low cluster (KOMBI), high
  clusters (IKE, IKI).
- The adress pool is shared by all models that utilise this bus system. An address is rarely reallocated even if the
  originally allocated device is not applicable to a new model.

### K/I-Bus

| Device | Bus | Abbreviation | Description                                      | Vehicles      |
|--------|-----|--------------|--------------------------------------------------|---------------|
| `0x00` | K   | ZKE          | General Body Electronics                         |               |
| `0x08` | K   | SHD          | Tilt/Slide Sunroof                               |               |
| `0x18` | K/I | CDC          | CD Changer                                       |               |
| `0x24` | K   | HKM          | Trunk Lid Module                                 | E38, E39      |
| `0x28` | I   | RCC          | Radio Clock Control                              | E38           |
| `0x2e` | K   | EDC          | Electronic Damper Control                        | E38, E39      |
| `0x30` | I   | CCM          | Check Control Module                             | E38           |
| `0x3b` | I   | GT           | Graphics Stage                                   |               |
| `0x3f` | K/I |              | Diagnostics (via [gateway](#gateway))            |               |
| `0x40` | K   | FBZV         | Remote Control for Central Locking               | E31           |
| `0x43` | I   | GTF          | Rear Graphics Stage                              | E38           |
| `0x44` | K   | EWS          | Drive Away Protection System                     |               |
| `0x45` | K   | DWA          | Anti-Theft System                                |               |
| `0x46` | I   | CID          | Central Information Display                      | E83, E85      |
| `0x47` | I   | FMBT         | Rear Control Panel                               | E38           |
| `0x48` | I   | JBIT         | Telephone (Japan)                                |               |
| `0x50` | K/I | MFL          | Multifunction Steering Wheel                     |               |
| `0x51` | K   | SPMBT        | Mirror Memory: Passenger                         | E46           |
| `0x53` | K/I |              | Unconfirmed: Multicast 📣                        |               |
| `0x5b` | K   | IHKA         | Automatic Heating/Air Conditioning               |               |
| `0x60` | K/I | PDC          | Park Distance Control                            |               |
| `0x66` | K   | ALC          | Active Light Control                             |               |
| `0x67` | K/I | ONL          | General Module logical GATS/service interface    |               |
| `0x68` | K/I | RAD          | Radio                                            |               |
| `0x69` | K   | EKM          | Electronic Body Module                           | E31           |
| `0x6a` | K/I | DSP          | Digital Sound Processor                          |               |
| `0x6b` | K   | STH          | Auxiliary Heater                                 |               |
| `0x70` | K   | RDC/DWS      | Tire Pressure Control & Deflation Warning System |               |
| `0x71` | K   | SMF          | Seat Memory: Driver                              | E31           |
| `0x72` | K   | SMF          | Seat Memory: Driver                              | E46, E53      |
| `0x73` | I   | SDRS         | Sirius Satellite Radio                           |               |
| `0x76` | K   | CDC          | CD Changer (DIN?)                                |               |
| `0x7f` | K/I | NAV          | Navigation                                       |               |
| `0x80` | K/I | KMB/IKE      | Instrument Cluster                               |               |
| `0x9a` | K/I | ALWR         | Automatic Headlight Vertical Aim Control         |               |
| `0x9b` | K   | CVM          | Convertible Soft Top Module                      | E36           |
| `0x9b` | K   | SPMFT        | Mirror Memory: Driver                            | E46           |
| `0x9c` | K   | CVM          | Convertible Soft Top Module                      | E46           |
| `0x9d` | K   | ETS          | Electronic Disconnecting Switch                  | E38           |
| `0xa0` | I   | FID          | Rear Multi-functional Display                    | E38, E39      |
| `0xa4` | K   | MRS          | Multiple Restraint System                        |               |
| `0xa7` | K   | FHK          | Rear Compartment Heating/Air Conditioning        | E38           |
| `0xac` | K   | EHC          | Electronic Height Control                        |               |
| `0xb0` | K/I | SES          | Speech Input System                              |               |
| `0xb9` | K   | RF/IR        | Compact Remote Control                           |               |
| `0xbb` | K/I | NAJ          | Navigation (Japan)                               |               |
| `0xbf` | K   |              | Global Broadcast 📣                                     |               |
| `0xc0` | K/I | MID          | Multi-functional Display                         | E38, E39, E53 |
| `0xc8` | K/I | TEL          | Telephone logical interface                      |               |
| `0xca` | I   | TCU          | BMW Assist / telematics interface                 |               |
| `0xcd` | K   | MID          | Multi-functional Display                         | E31           |
| `0xda` | K   | SMB          | Seat Memory: Passenger                           | E46           |
| `0xd0` | K/I | LCM/LSZ      | Lamp Check Module & Light Switch Center          |               |
| `0xe0` | K   | IRIS         | Integrated Radio and Information System          | E39           |
| `0xe7` | K/I |              | Multicast: Displays 📣                           |               |
| `0xe8` | K   | RLS          | Rain/Light Sensor                                |               |
| `0xea` | I   | DSPC         | DSP Controller                                   | E38           |
| `0xed` | I   | VID          | Video Module                                     |               |
| `0xf0` | I   | BMBT         | On-board Computer Control Panel                  |               |
| `0xf5` | K   | LKM2         | Lamp Control Module 2                            | E31           |
| `0xf5` | K   | SZM          | Center Console Switch Center                     |               |
| `0xff` | K/I |              | Local Broadcast 📣                                     |               |

### D-Bus

The shared address space might suggest it's possible to communicate with D-Bus devices from the K/I-Bus, however that's
not the case. This is purely a function of diagnostics, in which all devices must be addressable from the D-Bus.

| Device | Bus | Description                                          |
|--------|-----|------------------------------------------------------|
| `0x10` | D   | Engine Management                                    |
| `0x11` | D   | Central Body Electronics (ZKE 1/2) [E31, E34]        |
| `0x12` | D   | Engine Management                                    |
| `0x13` | D   | Engine Management                                    |
| `0x14` | D   | Engine Management                                    |
| `0x15` | D   | Double Sunroof (DDSHD) [E34]                         |
| `0x16` | D   | Thermal Level Oil Sensor [E36]                       |
| `0x19` | D   | *Range Rover*                                        |
| `0x20` | D   | Electronic Engine Power Control (EML) [M70]          |
| `0x21` | D   | Central locking module [E34, E36]                    |
| `0x22` | D   | Electronic Engine Power Control (EML) [M73]          |
| `0x31` | D   | *MINI*                                               |
| `0x32` | D   | Gearbox Control                                      |
| `0x35` | D   | Steering Column Memory (LSM) [E31/E32/E34]           |
| `0x36` | D   | ABS/ASC (Concept 1/2)                                |
| `0x56` | D   | ABS/ASC/DSC (DS2)                                    |
| `0x57` | D   | Steering Angle Sensor (LWS)                          |
| `0x59` | D   | Automatic Heating/Air Conditioning (IHKA) [E31, E36] |
| `0x5a` | D   | Electric Steering Lock (ELV) [E52]                   |
| `0x65` | D   | Fuel Pump (EKP)                                      |
| `0x6c` | D   | Gearbox Control                                      |
| `0x74` | D   | Seat Occupation Detection US (OC3) [E83, 85]         |
| `0x81` | D   | *MINI*                                               |
| `0x86` | D   | Active Rear Axle Kinematics (AHK) [E31]              |
| `0x9e` | D   | Rollover Sensor [E36]                                |
| `0xa6` | D   | Cruise Control                                       |
| `0xc2` | D   | Servotronic (SVT)                                    |
| `0xce` | D   | Seat Occupancy Detection                             |

## Command Index

| Command | Description                                                              |
|:--------|:-------------------------------------------------------------------------|
| `0x00`  | [ONL Service](onl/00.md)                                                 |
| `0x01`  | [Ping](common/01.md)                                                     |
| `0x02`  | [Pong & Announce](common/02.md)                                          |
| `0x05`  | [BMBT Service Mode Request](gt/05.md)                                    |
| `0x06`  | Service Reply: [BMBT](bmbt/06.md) / [VID](vid/06.md)                     |
| `0x10`  | [Ignition Request](ike/10.md)                                            |
| `0x11`  | [Ignition](ike/11.md)                                                    |
| `0x12`  | [Sensors Request](ike/12.md)                                             |
| `0x13`  | [Sensors](ike/13.md)                                                     |
| `0x14`  | [Language & Region Request](ike/14.md)                                   |
| `0x15`  | [Language & Region](ike/15.md)                                           |
| `0x16`  | [Odometer Request](ike/16.md)                                            |
| `0x17`  | [Odometer](ike/17.md)                                                    |
| `0x18`  | [Speed / RPM](ike/18.md)                                                 |
| `0x19`  | [Temperature](ike/19.md)                                                 |
| `0x1a`  | [Check Control Message](lcm/1a.md)                                       |
| `0x1b`  | [IKE Text Status](lcm/1b.md)                                             |
| `0x1d`  | [Temperature Request](ike/1d.md)                                         |
| `0x1f`  | [GPS Time](nav/1f.md)                                                    |
| `0x20`  | MID Button                                                               |
| `0x21`  | [Menu Text](common/21.md)                                                |
| `0x22`  | [Text Display Confirmation](common/22.md)                                |
| `0x23`  | [Title Text](common/23.md)                                               |
| `0x24`  | [Property Text](common/24.md)                                            |
| `0x27`  | [MID Display Request](ike/27.md)                                         |
| `0x2a`  | [OBC Status](ike/2a.md)                                                  |
| `0x2b`  | [Telephone LEDs](tel/2b.md)                                              |
| `0x2c`  | [Telephone Status](tel/2c.md)                                            |
| `0x2d`  | [Telephone Direct Dial](tel/2d.md)                                       |
| `0x31`  | Menu Button                                                              |
| `0x32`  | Volume: [BMBT](bmbt/32.md) / [MFL](mfl/32.md) / [DSP](dsp/32.md)         |
| `0x33`  | [TMC Station Status](rad/33.md)                                          |
| `0x34`  | [DSP Equalizer Button](dsp/34.md)                                        |
| `0x35`  | [DSP Status](dsp/35.md)                                                  |
| `0x36`  | [Radio EQ](rad/36.md) / [DSP Control](dsp/36.md)                         |
| `0x37`  | [Radio Tone/Select](rad/37.md)                                           |
| `0x38`  | [CDC Request](cdc/38.md)                                                 |
| `0x39`  | [CDC Status](cdc/39.md)                                                  |
| `0x3b`  | [MFL Buttons](mfl/3b.md)                                                 |
| `0x3c`  | [TMC Station List Text](rad/3c.md)                                       |
| `0x3f`  | [CDC ID3 Text](cdc/3f.md)                                                |
| `0x40`  | [OBC Input](gt/40.md)                                                    |
| `0x41`  | [OBC Control](gt/41.md)                                                  |
| `0x42`  | [OBC Remote Control](ike/42.md)                                          |
| `0x45`  | [Set Radio UI](gt/45.md)                                                 |
| `0x46`  | [Request Radio UI](rad/46.md)                                            |
| `0x47`  | [BMBT "Soft" Buttons](bmbt/47.md)                                        |
| `0x48`  | [BMBT Buttons](bmbt/48.md)                                               |
| `0x49`  | [BMBT Navigation Dial](bmbt/49.md)                                       |
| `0x4a`  | [BMBT Tape/LED Control](bmbt/4a.md)                                      |
| `0x4b`  | [BMBT Tape Status](bmbt/4b.md)                                           |
| `0x4d`  | [Video Module State](vid/4d.md)                                          |
| `0x4e`  | [Radio Source / Navigation Volume](rad/4e.md)                            |
| `0x4f`  | [BMBT Monitor Control](bmbt/4f.md) & [Video Module Source](vid/4f.md)    |
| `0x50`  | [Check Control Status Request](lcm/50.md)                                |
| `0x51`  | [Check Control Status](lcm/51.md)                                        |
| `0x52`  | [Check Control Message Relay](lcm/52.md)                                 |
| `0x53`  | [Redundant Data Request](ike/53.md)                                      |
| `0x54`  | [Redundant Data](ike/54.md)                                              |
| `0x55`  | [Replicate Data](ike/55.md)                                              |
| `0x56`  | [Rain/Driving-Light Status Request](rls/56.md)                           |
| `0x57`  | [Cluster Buttons](ike/57.md)                                             |
| `0x58`  | [RLS Wiper Interval Data](rls/58.md)                                     |
| `0x59`  | [Rain/Driving-Light Status](rls/59.md)                                   |
| `0x5a`  | [Cluster Indicators Request](lcm/5a.md)                                  |
| `0x5b`  | [Cluster Indicators](lcm/5b.md)                                          |
| `0x5c`  | [Instrument Backlighting (58G)](lcm/5c.md)                               |
| `0x5d`  | [Instrument Backlighting (58G) Request](lcm/5d.md)                       |
| `0x61`  | [EHC Status](ehc/61.md)                                                  |
| `0x62`  | [RDC Status](rdc/62.md)                                                  |
| `0x70`  | [MRS Status](mrs/70.md)                                                  |
| `0x71`  | [Rain Sensor Status Request](gm/71.md)                                   |
| `0x72`  | [Remote Key Buttons](gm/72.md) / [FBZV Check Control Status](fbzv/72.md) |
| `0x73`  | [Immobiliser Status Request](ews/73.md)                                  |
| `0x74`  | [Immobiliser Status](ews/74.md)                                          |
| `0x75`  | [Wiper Status Request](gm/75.md)                                         |
| `0x76`  | [Visual Indicators](gm/76.md)                                            |
| `0x77`  | [Wiper Status](gm/77.md)                                                 |
| `0x78`  | [Memory](gm/78.md)                                                       |
| `0x79`  | [Door/Lid Status Request](gm/79.md)                                      |
| `0x7a`  | [Door/Lid Status](gm/7a.md)                                              |
| `0x7c`  | [Sunroof Status](shd/7c.md)                                              |
| `0x7d`  | [Sunroof Control](gm/7d.md)                                              |
| `0x82`  | [IHKA Status](ihka/82.md)                                                |
| `0x83`  | [IHKA A/C Control](ihka/83.md)                                           |
| `0x86`  | [Rear Defroster Status](ihka/86.md)                                      |
| `0x87`  | [Rear Defroster Status Request](ihka/87.md)                              |
| `0x9e`  | [Rear Monitor Control](fmbt/9e.md)                                  |
| `0x9f`  | [Rear Monitor Status](fmbt/9f.md)                                   |
| `0xa0`  | [TCU Emergency-Call Status](tcu/a0.md) / [Telephone Data](tel/a0.md)     |
| `0xa2`  | [Telematics Coordinates](tel/a2.md)                                      |
| `0xa4`  | [Telematics Location](tel/a4.md)                                         |
| `0xa5`  | [Body Text](common/a5.md)                                                |
| `0xa6`  | [SMS Icon](tel/a6.md)                                                    |
| `0xa7`  | Traffic Management Channel Request                                       |
| `0xa8`  | [Traffic Management Channel](rad/a8.md)                                  |
| `0xa9`  | [BMW Assist Data](tel/a9.md)                                             |
| `0xaa`  | Navigation Control: [SES](ses/aa.md) / [GTF](nav/aa.md)                  |
| `0xab`  | [GTF Remote Control Status](nav/ab.md)                                   |
| `0xaf`  | [SES Navigation Status](ses/af.md)                                       |
| `0xd4`  | [NG-Radio Station List](rad/d4.md)                                       |
| `0xd5`  | [CID Display Status](cid/d5.md)                                          |

## Features

### Sensors

1. `0x10` [Ignition Request](ike/10.md)
2. `0x11` [Ignition](ike/11.md)
3. `0x12` [Sensors Request](ike/12.md)
4. `0x13` [Sensors](ike/13.md)
5. `0x16` [Odometer Request](ike/16.md)
6. `0x17` [Odometer](ike/17.md)
7. `0x18` [Speed / RPM](ike/18.md)
8. `0x19` [Temperature](ike/19.md)
9. `0x1d` [Temperature Request](ike/1d.md)

### OBC

1. `0x14` [Language & Region Request](ike/14.md)
2. `0x15` [Language & Region](ike/15.md)
3. `0x24` [Property Text: IKE](ike/24.md)
4. `0x27` [MID Display Request](ike/27.md)
5. `0x2a` [OBC Status](ike/2a.md)
6. `0x40` [OBC Input](gt/40.md)
7. `0x41` [OBC Control](gt/41.md)
8. `0x42` [Remote Control](ike/42.md)

### Redundant Data Storage

1. `0x53` [Redundant Data Request](ike/53.md)
2. `0x54` [Redundant Data](ike/54.md)
3. `0x55` [Replicate Data](ike/55.md)

### Controls

1. `0x20` [MID Button: Telephone](tel/20.md)
2. `0x31` BMBT/MID Menu Button
3. `0x32` [MFL Volume](mfl/32.md)
4. `0x3b` [MFL Buttons](mfl/3b.md)
5. `0x32` [BMBT Volume Dial](bmbt/32.md)
6. `0x48` [BMBT Buttons](bmbt/48.md)
7. `0x47` [BMBT "Soft" Buttons (i.e. INFO)](bmbt/47.md)
8. `0x49` [Navigation Dial](bmbt/49.md)
9. `0x57` [Cluster Buttons](ike/57.md)

### Radio

1. `0x21` [Menu Text: Radio](rad/21.md)
2. `0x23` [Title Text: Radio](rad/23.md)
3. `0x24` [Property Text: Radio](rad/24.md)
4. `0x32` [DSP Volume](dsp/32.md)
5. `0x33` [TMC Station Status](rad/33.md)
6. `0x34` [DSP Equalizer Button](dsp/34.md)
7. `0x35` [DSP Status](dsp/35.md)
8. `0x36` [Radio EQ](rad/36.md) / [DSP Control](dsp/36.md)
9. `0x37` [Radio Tone/Select](rad/37.md)
10. `0x38` [CDC Request](cdc/38.md)
11. `0x39` [CDC Status](cdc/39.md)
12. `0x3c` [TMC Station List Text](rad/3c.md)
13. `0x3f` [CDC ID3 Text](cdc/3f.md)
14. `0x46` [Request Radio UI](rad/46.md)
15. `0x4a` [BMBT Tape/LED Control](bmbt/4a.md)
16. `0x4e` [Radio Source / Navigation Volume](rad/4e.md)
17. `0xa5` [Body Text: Radio](rad/a5.md)
18. `0xa8` [Traffic Management Channel](rad/a8.md)
19. `0xd4` [NG-Radio Station List](rad/d4.md)

### Telephone

TEL `0xc8` is the logical telephone interface. It may be provided by a dedicated telephone module or by a TCU. An Everest TCU uses `0xc8` for the normal telephone UI/data path and may simultaneously use TCU address `0xca` for its BMW Assist/telematics path.

1. `0x02` [Announce: Telephone](common/02.md#telephone-0xc8)
2. `0x2b` [Telephone LEDs](tel/2b.md)
3. `0x2c` [Telephone Status](tel/2c.md)
4. `0x2d` [Telephone Direct Dial](tel/2d.md)
5. `0x21` [Menu Text: Telephone](tel/21.md)
6. `0x23` [Title Text: Telephone](tel/23.md)
7. `0x24` [Property Text: Telephone](tel/24.md)
8. `0xa0` [Telephone Data](tel/a0.md)
9. `0xa5` [Body Text: Telephone](tel/a5.md)
10. `0xa6` [SMS Icon](tel/a6.md)
11. `0xa9` [BMW Assist Data](tel/a9.md)

#### Displays

1. [Default](tel/default.md)
2. [Pin-Code](tel/pin.md)
3. [Dial](tel/dial.md)
4. [Last Numbers](tel/last_numbers.md)
5. [Directory](tel/directory.md)
6. [Top 8](tel/top_8.md)
7. [Info](tel/info.md)
8. [Bluetooth Pairing](tel/list.md)
9. [SMS Index](tel/list.md)
10. [SMS Message](tel/detail.md)
11. [SOS/Emergency](tel/detail.md)

### TCU and BMW Assist

TCU `0xca` is the additional BMW Assist/telematics interface. It does not replace TEL `0xc8`; a TCU that also provides telephone service can use both logical addresses.

1. `0x02` [Announce: TCU](common/02.md#announce)
2. `0x23` [Title Text: TCU](tcu/23.md)
3. `0xa0` [TCU Emergency-Call Status](tcu/a0.md)

### Navigation

1. `0x02` [Announce: BMBT](common/02.md#bmbt-0xf0)
2. `0x02` [Announce: GT](common/02.md#gt-0x3b)
3. `0x02` [Announce: Nav.](common/02.md#nav-computer-0x7f)
4. `0x1f` [GPS Time](nav/1f.md)
5. `0x4f` [Monitor Control](bmbt/4f.md)
6. `0xaa` [GTF Navigation Control](nav/aa.md)
7. `0xab` [GTF Remote Control Status](nav/ab.md)

#### Telematics

1. `0xa2` [Telematics Coordinates](tel/a2.md)
2. `0xa4` [Telematics Location](tel/a4.md)
3. `0xa9` [BMW Assist Data](tel/a9.md)

### Speech Input System

1. `0xaa` [SES Navigation Control](ses/aa.md)
2. `0xaf` [SES Navigation Status](ses/af.md)

### Lighting

1. `0x56` [Rain/Driving-Light Status Request](rls/56.md)
2. `0x59` [Rain/Driving-Light Status](rls/59.md)
3. `0x5a` [Cluster Indicators Request](lcm/5a.md)
4. `0x5b` [Cluster Indicators](lcm/5b.md)
5. `0x5c` [Instrument Backlighting (58G)](lcm/5c.md)
6. `0x5d` [Instrument Backlighting (58G) Request](lcm/5d.md)

### Body

1. `0x58` [RLS Wiper Interval Data](rls/58.md)
2. `0x71` [Rain Sensor Status Request](gm/71.md)
3. `0x72` [Remote Key Buttons](gm/72.md)
4. `0x73` [Immobiliser Status Request](ews/73.md)
5. `0x74` [Immobiliser Status](ews/74.md)
6. `0x75` [Wiper Status Request](gm/75.md)
7. `0x76` [Visual Indicators](gm/76.md)
8. `0x77` [Wiper Status](gm/77.md)
9. `0x78` [Memory](gm/78.md)
10. `0x79` [Door/Lid Status Request](gm/79.md)
11. `0x7a` [Door/Lid Status](gm/7a.md)
