## Addresses

- 8-bit addressing
- Addresses are assigned fro
- Addresses are programed from the factory
- The addresses are preprogramed from the factory

- Device addresses are preprogramed from the factory
- The 8-bit address pool is shared between every model that utilises this bus system. e.g. once the address `0x69` was allocated to the elektronic bodymodule of the E31, it was not used again, even on models to which the device was not applicable to.

### Address Index

ID    |Description
------|----------
`0x00`|General Module (GM)
`0x08`|Tilt/Slide Sunroof (SHD)
`0x15`|???
`0x18`|CD Changer
`0x24`|Trunk lid module
`0x28`|Radio Controlled Clock
`0x2c`|TBC
`0x2e`|Electronic Damper Control (EDC)
`0x30`|Check Control Module
`0x31`|TBC
`0x35`|steering column's memory E31 / E32 / E34
`0x3b`|Graphics Stage (GT)
`0x3f`|Diagnostics (Gateway)
`0x40`|Remote Control for Central Locking
`0x44`|Drive Away Protection System (EWS)
`0x45`|Anti-Theft System (DWA3, DWA4)
`0x46`|Central Information Display
`0x47`|Rear Compartment Monitor
`0x48`|Japan Basis Interface Telephone
`0x50`|Multifunction Steering Wheel
`0x51`|Mirror Memory (Passenger)
`0x59`|Heating/Air Conditioning?
`0x5b`|Automatic Heating/Air Conditioning (IHKA)
`0x60`|Park Distance Control
`0x65`|TBC
`0x66`|Active Light Control
`0x68`|Radio
`0x69`|elektronic bodymodule EKM [E31]
`0x6a`|Digital Sound Processor (DSP)
`0x6b`|Auxiliary Heating (Webasto) (TIS A14)
`0x70`|Tire Pressure Control/Warning
`0x71`|mirror-memory E46 driver's doorm mirror-memory E46 passenger's door
`0x72`|Seat Memory (Driver) [SM] [ZKE5]
`0x72`|Gateway SZM<->SM(E46)
`0x74`|Seat Occupancy Detection 3
`0x76`|CD Player (Business)
`0x7f`|Navigation
`0x80`|Instrument Cluster
`0x81`|Remote Instrument Pack TBC 
`0x86`|Xenon Light Right [E46?]
`0x98`|Xenon Light Left [E46?]
`0x9a`|Automatic Headlight Vertical Aim Control
`0x9b`|Mirror Memory (Driver) [seat control, driver (SBFA)] [ZKE5]
`0x9c`|The Convertible Top Module
`0x9e`|Roll-over Sensor/Protection System
`0xa0`|Rear Multi-information display (E38)
`0xa4`|Multiple Restraint System
`0xa7`|Rear compartment heating/air conditioning [E38]
`0xac`|Electronic Height Control
`0xb0`|Speech recognition system
`0xb9`|compact remote control (RF/Infra.)
`0xbb`|Navigation [Japan]
`0xbf`|Multicast: K + I buses?
`0xc0`|Multi-information display "MID"
`0xc8`|Telephone
`0xcd`|Multi Information Display (OBC) [E31]
`0xce`|Seat occupancy detection 2
`0xd0`|Lamp Check Module (LCM), Light Switch Center (LSZ) [E46]
`0xda`|Seat Memory (Passenger) [passenger seat memory (SMB)] [ZKE5]
`0xe0`|Integrated Radio and Information System
`0xe7`|Multicast: Displays
`0xe8`|Rain/driving light sensor, Automatic Interval Control
`0xea`|DSP-controler [E38]
`0xed`|Video Module
`0xf0`|On-board computer control panel (BMBT)
`0xf5`|Lamp control module [E31]