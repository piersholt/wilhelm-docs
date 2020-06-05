## Addresses

- 8-bit addressing
- Addresses are assigned fro
- Addresses are programed from the factory
- The addresses are preprogramed from the factory

- Device addresses are preprogramed from the factory
- The 8-bit address pool is shared between every model that utilises this bus system. e.g. once the address `0x69` was allocated to the elektronic bodymodule of the E31, it was not used again, even on models to which the device was not applicable to.

### Address Index

ID|Description|Note
:--|:--|:--|:--
`0x00`|General Module (GM)|ZKE3, ZKE5,ZKE5\_S12
`0x08`|Tilt/Slide Sunroof (SHD)|SHD46, SHD46\_2, SD\_DS2
`0x15`|???|DDSHD
`0x18`|CD Changer|TBC!
`0x24`|Trunk lid module|HKM
`0x28`|Radio Controlled Clock|RCC
`0x2c`|TBC|VNC
`0x2e`|Electronic Damper Control (EDC)|EDC3P, EDC4
`0x30`|Check Control Module|CCM38
`0x31`|TBC|EHPSR50
`0x35`|steering column's memory E31 / E32 / E34|LSM
`0x3b`|Graphics Stage (GT)|VIDEO\_GT, NAVMK4, NAVMK4\_2
`0x3f`|Diagnostics (Gateway)|--
`0x40`|Remote Control for Central Locking|FBZV
`0x44`|Drive Away Protection System (EWS)|EWS, EWS3, EWS3D
`0x45`|Anti-Theft System (DWA3, DWA4)|DWA3, DWA4
`0x46`|Central Information Display|CID_?
`0x47`|Rear Compartment Monitor|FOND\_BT
`0x48`|Japan Basis Interface Telephone|JBIT, JBIT2
`0x50`|Multifunction Steering Wheel|MFL, MFL2, (MFLR, MFLR50)
`0x51`|Mirror Memory (Passenger)|TBC
`0x59`|Heating/Air Conditioning?|IHKA, IHKA31, IHR, IHKR3, IHKR36, IHRF3, HR32
`0x5b`|Automatic Heating/Air Conditioning (IHKA)|IHKA36,IHKR38,IHKA38,IHKA38\_2,IHKA38\_3,IHR39,IHKR39, IHKA39,IHKA39\_2,IHKA39\_3,IHKA39\_4,IHKA39\_5,IHKR46,IHKA46,IHKA46\_2,IHKA46\_3,IHKS52,ATC40,IHKAR50,IHKAR50R,IHKA85,IHKS85
`0x60`|Park Distance Control|PDCE38, PDCACT
`0x65`|TBC|EKP\_DS2, EKP2DS2
`0x66`|Active Light Control|ALC\_DS2
`0x68`|Radio|RADIO
`0x69`|elektronic bodymodule EKM [E31]|EKM
`0x6a`|Digital Sound Processor (DSP)|DSP, DSP2, DSP\_R50, DSP2\_R, TOPDSP, TOPDSP2
`0x6b`|Auxiliary Heating (Webasto) (TIS A14)|TBC
`0x70`|Tire Pressure Control/Warning|RDC, DWS
`0x71`|mirror-memory E46 driver's doorm mirror-memory E46 passenger's door|SPM, SM\_RD
`0x72`|Seat Memory (Driver) [SM] [ZKE5]|SM46, SM46\_4, SM46\_3, EASY\_E\_F, SM53\_6, SM53\_4, SM46C\_4, SM46C\_4M, SM46C\_5, SM46C\_5M, FAS\_63
`0x72`|Gateway SZM<->SM(E46)|BFS\_64
`0x74`|Seat Occupancy Detection 3|OC3 [E83/85]
`0x76`|CD Player (Business)|"CDC IBUS" via XML, (CDC CDC_46 from SGBD)
`0x7f`|Navigation|NAVIGAT, NAVMK2, NAVMK3, NAVMK4, NAVMK4\_2
`0x80`|Instrument Cluster|IKE, IKI, KOMBI39(C), KOMBI46(R), KOMBI52, KOMBI85
`0x81`|Remote Instrument Pack TBC |RIP
`0x86`|Xenon Light Right [E46?]|XENON\_R
`0x98`|Xenon Light Left [E46?]|XENON\_L
`0x9a`|Automatic Headlight Vertical Aim Control|LWR2A
`0x9b`|Mirror Memory (Driver) [seat control, driver (SBFA)] [ZKE5]|???
`0x9c`|The Convertible Top Module|CVM\_II,CVM\_III,CVM\_IV,CVM\_V,CVM\_R52
`0x9e`|Roll-over Sensor/Protection System|UEB2
`0xa0`|Rear Multi-information display (E38)|FOND\_ZIS
`0xa4`|Multiple Restraint System|ZAE, BAE, ZAE2, MRS2, MRS3, MRS3KW, MRS4, MRS4RD, MRS5K
`0xa7`|Rear compartment heating/air conditioning [E38]|FG38, FHK38
`0xac`|Electronic Height Control|EHC, EHC\_2, EHC\_2n, EHC\_2n2
`0xb0`|Speech recognition system|SES
`0xb9`|compact remote control (RF/Infra.)|IRS\_KOMP, FUNKKOMP
`0xbb`|Navigation [Japan]|NAV\_JAP, JNAV\_CE, JNAV\_CE2, NAV\_JAP2
`0xbf`|Multicast: K + I buses?|--
`0xc0`|Multi-information display "MID"|ZIS
`0xc8`|Telephone|BIT, TELEFON, BIT2, ULF, TELIBUS, TELIBUS2
`0xcd`|Multi Information Display (OBC) [E31]|MID, UHR\_BC, BCIII, BC\_IV, BC\_V
`0xce`|Seat occupancy detection 2|SBE2
`0xd0`|Lamp Check Module (LCM), Light Switch Center (LSZ) [E46]|LME38, LCM, LSZ, LCM\_A, LCM\_II, LCM\_III, LSZ\_2, LCM\_IV
`0xda`|Seat Memory (Passenger) [passenger seat memory (SMB)] [ZKE5]|B\_SM46\_4, B\_SM46\_3, EASY\_E\_B, BSM46C\_4, BSM46C\_5
`0xe0`|Integrated Radio and Information System|IRIS
`0xe7`|Multicast: Displays|
`0xe8`|Rain/driving light sensor, Automatic Interval Control|AIC, RLS\_DS2
`0xea`|DSP-controler [E38]|DSP\_BT
`0xed`|Video Module|VIDEO\_TV, VIDEOMOD,VIDEO\_3, VM5IBUS, VIDHIBUS
`0xf0`|On-board computer control panel (BMBT)|BORDMONI, BMBT46TN, BMBT46RN, BM\_WIDE, BM46WIDE, BMBT\_MIR, BMBTR50
`0xf5`|Lamp control module [E31]|LKM2
`0xff`|Broadcast: local bus?
