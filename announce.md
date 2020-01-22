# `0x02` "Pong"

One byte.

Bit|7|6|5|4|3|2|1|0
:---|:---|:---|:----|:----|:---|:---|:---|:---
Use|Signature|Signature|Signature|Signature|-|-|-|Announce


## Bitmasks
    
    ANNOUNCE    = 0b0000_0001 << 0
    SIGNATURE   = 0b1111_0000 << 0


## Properties

### Announce `0b0000_0001`

    REPLY       = 0b0000_0000
    ANNOUNCE    = 0b0000_0001

- Establish state.
- IKE will always send ignition status `0x11`

### Signature `0b1111_0000`

In the case that modules have multiple variants, and that variant affects behaviour of other modules on the bus, a "signature" is used.

#### GT

Module|Variant|Signature|Frame|
:---|:---|:---|:---|
GT|Nav. GT (incl. MK1)|`0x40`|`3B 04 BF 02 41 C3`
GT|Video Module GT|`0x10`|`3B 04 FF 02 11 D3`

#### Radio

Module|Variant|Signature|Frame|
:---|:---|:---|:---|
Radio|C23 BM|`0x00`|`68 04 FF 02 01 90`
Radio|BM53|`0x00`|`68 04 BF 02 01 D0`
Radio|Business Nav.|`0x20`|`tbc`

#### Nav. Computer

Module|Variant|Signature|Frame|
:---|:---|:---|:---|
Nav.|MK4|`0x40`|`7F 04 BF 02 41 87`
Nav.|MK4 + BMW Assist|`0xc0`|`7F 04 BF 02 C1 07`


- telephone to presumably configure BMW Assist
- may affect MRS and sending impact notification

#### Telephone

Module|Variant|Signature|Frame|
:---|:---|:---|:---|
Telephone|CMT3000|`0x00`|`C8 04 FF 02 01 30`
Telephone|Motorola V-Series|`0x30`|`C8 04 FF 02 31 00`

- nav. computer will send telematics data `0xa2`, `0xa4`

#### BMBT

Module|Variant|Signature|Frame|
:---|:---|:---|:---|
BMBT|4:3|`0x00`|`F0 04 BF 02 01 48`
BMBT|16:9|`0x30`|`F0 04 BF 02 31 78`

- GT/VM should set correct aspect ratio and encoding.

### No known variants...

Module|Module ID|Variant|Signature|Frame|
:---|:---|:---|:---|:---|
GM|`0x00`|GM III (E39)|`0x00`|`00 04 BF 02 01 B8`
CDC|`0x18`|All?|`0x00`|`18 04 BF 02 01 A0`
CCM|`0x30`|All?|`0x00`|`30 04 BF 02 01 88`
PDC|`0x60`|All?|`0x00`|`60 04 BF 02 01 D8`
IKE|`0x80`|All?|`0x00`|`80 04 BF 02 01 38`
EHC|`0xAC`|All?|`0x00`|`AC 04 BF 02 01 14`
LCM|`0xD0`|LCM III (E39)|`0x00`|`D0 04 BF 02 01 68`
TV|`0xED`|MK1 VM, "MK3" VM|`0x00`|`ED 04 FF 02 01 15`