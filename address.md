## Addresses

- 8-bit addressing (256 unique addressess).
- Addresses are preallocated, and remain fixed.
- Multicast, and broadcast addresses.
- All buses are within the 8-bit scope, i.e. an address is unique across the I, K, and D buses.
- The adress pool is shared by all models that utilise this bus system. i.e. once the address `0x69` was allocated to the E31 body module, it was not reallocated, even on models to which the device was not applicable to.
- Variants of a device will have the same address, e.g. the address `0x80` is used by the low cluster (KOMBI), high clusters (IKE, IKI).

### Address Index

*Only common I and K bus device addresses are listed.*

Address|Device(s)
------|----------
`0x00`|General Module (GM)
`0x08`|Tilt/Slide Sunroof
`0x18`|CD Changer
`0x24`|Trunk Lid Module
`0x28`|Radio Controlled Clock (RCC)
`0x2e`|Electronic Damper Control (EDC)
`0x30`|Check Control Module (CCM)
`0x3b`|Graphics Stage (GT)
`0x3f`|Diagnostics (Gateway)
`0x40`|Remote Control for Central Locking
`0x44`|Drive Away Protection System (EWS)
`0x45`|Anti-Theft System (DWA)
`0x46`|Central Information Display (CID)
`0x47`|Rear Compartment Monitor (RCM)
`0x48`|Telephone (Japan)
`0x50`|Multifunction Steering Wheel (MFL)
`0x51`|Mirror Memory: Passenger [E46]
`0x5b`|Automatic Heating/Air Conditioning (IHKA)
`0x60`|Park Distance Control (PDC)
`0x66`|Active Light Control (ALC)
`0x68`|Radio
`0x69`|Body Module [E31]
`0x6a`|Digital Sound Processor (DSP)
`0x6b`|Auxiliary Heating [Webasto]
`0x70`|Tire Pressure Control/Warning (RDC)
`0x71`|Mirror Memory: Driver [E46]
`0x72`|Seat Memory: Driver (ZKE5)
`0x76`|CD Player (Business)
`0x7f`|Navigation
`0x80`|Instrument Cluster (IKE/KOMBI)
`0x9a`|Automatic Headlight Vertical Aim Control (LWR)
`0xa0`|Rear Multi-information Display [E38]
`0xa4`|Multiple Restraint System (MRS)
`0xa7`|Rear Compartment Heating/Air Conditioning
`0xac`|Electronic Height Control (EHC)
`0xb0`|Speech Recognition System (SES)
`0xb9`|Compact Remote Control (RF/IR)
`0xbb`|Navigation (Japan)
`0xbf`|Broadcast 📣
`0xc0`|Multi-information Display (MID)
`0xc8`|Telephone
`0xcd`|Multi Information Display (OBC) [E31]
`0xd0`|Lamp Check Module (LCM), Light Switch Center (LSZ)
`0xda`|Seat Memory: Passenger [E46]
`0xe0`|Integrated Radio and Information System (IRIS)
`0xe7`|Multicast: Displays 📣
`0xe8`|Rain/Driving Light Sensor (RLS)
`0xea`|DSP Controler [E38]
`0xed`|Video Module
`0xf0`|On-board Computer Control Panel (BMBT)
`0xf5`|Lamp control module [E31]
`0xff`|Broadcast 📣