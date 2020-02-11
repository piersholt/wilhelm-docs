# `0x02` "Pong"

This command has two purposes:

1. Annoucing the presence of a module on the bus.
2. "Pong" in response to a "Ping" `0x01`.

### Examples

The length of the message does not vary. The single data byte is a bitmask.

    60 04 F0 02 00 96
    3B 04 C8 02 10 E5
    BB 04 68 02 00 D5

## Bitmasks
    
    ANNOUNCE    = 0b0000_0001 << 0
    SIGNATURE   = 0b1111_0000 << 0

Bit|7|6|5|4|3|2|1|0
:---|:---|:---|:----|:----|:---|:---|:---|:---
Use|Signature|Signature|Signature|Signature|-|-|-|Announce

## Properties

### Announce `0b0000_0001`

    REPLY       = 0b0000_0000
    ANNOUNCE    = 0b0000_0001

The announce bit is set when a module becomes active on the bus. This is most frequently seen at ignition with modules commonly powered/activated by ignition circuits (KL-R, KL-15).

    C8 04 FF 02 31 00       # Telephone broadcasting an announcement

The announcement is what determines the availability of numerous features. For example, Television, Telephone, and DSP will all appear in the BMBT main menu following announcement.

An annoucement also allows the new module to establish it's state. and any applicable modules will respond as necessary. The response will depend on the announcing module, but will at minimum, include ignition state `0x11` from the cluster.

After a module has announced, it's ongoing presence will be checked by interested modules via "pings" `0x01`, for which this bit will never be set.

    C8 04 FF 02 30 01       # Telephone replying to a "ping" (no announce bit!)

### Signature `0b1111_0000`

In the case that a module has variants, and that variant affects behaviour of other modules on the bus, a "signature" is used to allow variants to be identified.

A good working example of this is the BMBT which was introduced with the 4x3 display, and was later upgraded to the larger 16x9 display. In order for the navi. computer/video module to output a video signal with the correct aspect ratio, it must be able to identify the BMBT variant.

#### GT `0x3b`

Module|Variant|Signature|Frame|
:---|:---|:---|:---|
GT|Video Module GT|`0x10`|`3B 04 FF 02 11 D3`
GT|Nav. GT (incl. MK1)|`0x40`|`3B 04 BF 02 41 C3`

#### Nav. Computer `0x7f`

Module|Variant|Signature|Frame|
:---|:---|:---|:---|
Nav.|MK4?|`0x40`|`7F 04 BF 02 41 87`
Nav.|MK4? + BMW Assist|`0xc0`|`7F 04 BF 02 C1 07`

- telephone to presumably configure BMW Assist
- may affect MRS and sending impact notification

#### Telephone `0xc8`

Module|Variant|Signature|Frame|
:---|:---|:---|:---|
Telephone|CMT3000|`0x00`|`C8 04 FF 02 01 30`
Telephone|Motorola V-Series|`0x30`|`C8 04 FF 02 31 00`

- nav. computer will send telematics data `0xa2`, `0xa4`

#### BMBT `0xf0`

Module|Variant|Signature|Frame|
:---|:---|:---|:---|
BMBT|4x3|`0x00`|`F0 04 BF 02 01 48`
BMBT|16x9|`0x30`|`F0 04 BF 02 31 78`

- GT/VM should set correct aspect ratio and encoding.

### No Signatures

While the need for a signature is likely predicated upon a module hardware/software revision, *it's only in the case that the module must be differentiated on the bus that a signature will be used*. Some modules, despite having one or more revisions, will not distinguish variants.

The following module variants do not appear to have a signature:

Module|Module ID|Variant|Signature|Frame|
:---|:---|:---|:---|:---|
GM|`0x00`|GM III (E39)|`0x00`|`00 04 BF 02 01 B8`
CDC|`0x18`|All?|`0x00`|`18 04 BF 02 01 A0`
CCM|`0x30`|All?|`0x00`|`30 04 BF 02 01 88`
PDC|`0x60`|All?|`0x00`|`60 04 BF 02 01 D8`
Radio|`0x68`|C23 BM|`0x00`|`68 04 FF 02 01 90`
Radio|`0x68`|BM53|`0x00`|`68 04 BF 02 01 D0`
IKE|`0x80`|IKE, IKI, KOMBI|`0x00`|`80 04 BF 02 01 38`
EHC|`0xAC`|All?|`0x00`|`AC 04 BF 02 01 14`
LCM|`0xD0`|LCM III (E39)|`0x00`|`D0 04 BF 02 01 68`
TV|`0xED`|MK1 VM, "MK3" VM|`0x00`|`ED 04 FF 02 01 15`
