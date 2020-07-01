## Device Index

- 8-bit addressing (256 unique addressess).
- Multicast, and broadcast addresses.
- Addresses are preallocated, and remain fixed.
- The adress pool is shared by all models that utilise this bus system. i.e. once the address `0x69` was allocated to the E31 body module, it was not reallocated, even on models to which the device was not applicable to.
- Variants of a device will have the same address, e.g. the address `0x80` is used by the low cluster (KOMBI), high clusters (IKE, IKI).
- All buses are within the 8-bit scope, i.e. an address is unique across the I, K, and D buses.

*Only common I and K bus device addresses are listed.*

Device|Bus|Description
------|---|-----------
`0x00`|K|General Module (GM)
`0x08`|K|Tilt/Slide Sunroof (SHD)
`0x10`|D|Engine Management
`0x11`|D|Centrol Body Electronics [ZKE1, ZKE2]
`0x12`|D|Engine Management
`0x13`|D|Engine Management
`0x14`|D|Engine Management
`0x15`|D|Double Sunroof (DDSHD) [E34]
`0x16`|D|Thermal Level Oil Sensor [E36]
`0x18`|K|CD Changer (CDC)
`0x19`|D|*Rover Automatic Transmission Control Unit*
`0x20`|D|Electronic Engine Power Control (EML) [M70]
`0x21`|D|Central locking module [E34, E36]
`0x22`|D|Electronic Engine Power Control (EML) [M73]
`0x23`|-|
`0x24`|K|Trunk Lid Module (HKM) [E38]
`0x28`|K|Radio Controlled Clock (RCC)
`0x2e`|K|Electronic Damper Control (EDC)
`0x30`|K|Check Control Module (CCM) [E38]
`0x31`|D|*MINI EHPR50*
`0x32`|D|Transmission
`0x35`|D|Steering Column Memory (LSM) [E31/E32/E34]
`0x3b`|K|Graphics Stage (GT)
`0x3f`|K/I|Diagnostics (via [gateway](#))
`0x40`|K|Remote Control for Central Locking
`0x44`|K|Drive Away Protection System (EWS)
`0x45`|K|Anti-Theft System (DWA)
`0x46`|K|Central Information Display (CID) [E83/E85]
`0x47`|K|Rear Compartment Monitor (RCM)
`0x48`|K|Telephone (Japan)
`0x50`|K|Multifunction Steering Wheel (MFL)
`0x51`|K|Mirror Memory: Passenger (ZKE5)
`0x5b`|K|Automatic Heating/Air Conditioning (IHKA)
`0x60`|K|Park Distance Control (PDC)
`0x66`|K|Active Light Control (ALC)
`0x68`|K|Radio
`0x69`|K|Body Module [E31]
`0x6a`|K|Digital Sound Processor (DSP)
`0x6b`|K|Auxiliary Heating "Webasto" (D-Bus?)
`0x70`|K|Tire Pressure Control/Warning (RDC)
`0x71`|K|Mirror Memory: Driver (ZKE5)
`0x72`|K|Seat Memory: Driver (ZKE5)
`0x76`|K|CD Player (Business)
`0x7f`|K|Navigation
`0x80`|K|Instrument Cluster (IKE/KOMBI)
`0x9a`|K|Automatic Headlight Vertical Aim Control (LWR)
`0xa0`|K|Rear Multi-information Display (MID) [E38]
`0xa4`|K|Multiple Restraint System (MRS)
`0xa7`|K|Rear Compartment Heating/Air Conditioning
`0xac`|K|Electronic Height Control (EHC)
`0xb0`|K|Speech Recognition System (SES)
`0xb9`|K|Compact Remote Control (RF/IR)
`0xbb`|K|Navigation (Japan)
`0xbf`|K|Broadcast 📣
`0xc0`|K|Multi-information Display (MID)
`0xc8`|K|Telephone
`0xcd`|K|Multi Information Display (OBC) [E31]
`0xd0`|K|Lamp Check Module (LCM), Light Switch Center (LSZ)
`0xda`|K|Seat Memory: Passenger (ZKE5)
`0xe0`|K|Integrated Radio and Information System (IRIS)
`0xe7`|K|Multicast: Displays 📣
`0xe8`|K|Rain/Driving Light Sensor (RLS)
`0xea`|K|DSP Controler [E38]
`0xed`|K|Video Module
`0xf0`|K|On-board Computer Control Panel (BMBT)
`0xf5`|K|Lamp control module [E31]
`0xff`|K|Broadcast 📣