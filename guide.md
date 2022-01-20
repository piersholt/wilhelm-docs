# `0xID` Command Name

### Senders/Receivers

List of possible recipients.
 
A given command mightn't be limited to a single sender, or receiver.
 
#### Example: `0x23` [Title Text: Radio](radio/23.md).

> Radio `0x68` → GT `0x3b`  
> Radio `0x68` → IKE `0x80`  
> Radio `0x68` → Broadcast `0xff`

### Overview

General overview of the command, and it's purpose. Detailed usage can be discussed in *Use Cases*.

#### Example: `0x37` [Radio Tone/Select](radio/37.md).

> This command allows the radio to load the appropriate **Tone** (EQ) and **Select** (playback options) menus.
> 
> The Tone and Select functionality as introduced with the C23/C24 was almost unusable owing to the counterintuitive UX. Thankfully, the NG radios, and the accompanying UI update (`3-1/40+`) implemented a number of changes to make the functionality somewhat suitable for humans.

### Related Commands

Any given command usually relates to a specific feature set, for which there's usually a number of applicable commands.

#### Example: `0x21` [Menu Text: Telephone](telephone/21.md).

> - `0x21` Menu Text: Radio
> - `0x21` Menu Text: Cluster
> - `0x23` [Title Text: Telephone](23.md)
> - `0x24` [Property Text: Telephone](24.md)
> - `0x31` Menu Button: Telephone
> - `0xa5` [Body Text: Telephone](a5.md)

### Example Frames

A representative sample of frames.

#### Example: `0x7a` [Door/Lid Status](gm/7a.md)

    00 05 BF 7A 51 1F 8E
    00 05 BF 7A 30 1F EF
    00 05 BF 7A 54 30 A4
    [...]

#### Example: `0x13` [Sensors](ike/13.md)

Be aware that some commands did evolve over the lifetime of the bus system. If so, try to denote how they're distinguished

Here the command varies with cluster type:

    # High Cluster (IKE)
    80 06 BF 13 03 00 00 29
    80 06 BF 13 03 B0 00 99
    [...]
    
    # High Cluster (IKI)
    80 0A BF 13 00 00 00 00 00 00 47 61
    80 0A BF 13 02 B0 00 00 00 00 47 D3
    [...]

#### Example: Data Leak!

Make sure you don't unwittingly publish personal data!

Good examples of this risk are:

- Your location via `0xa2` [Telematics: Coordinates](nav/a2.md)
- Your telephone contacts via `0x23` [Title Text: Telephone](telephone/23.md)

## Parameters

The formatting of the parameters section is quite inconsistent. It's evolved as the documentation has grown.

As a rule of thumb, the formatting depends on the number of parameters, and the number of data types. *The more parameters/data types, the more detailed the format.*

This general rule is demonstrated in the following examples:

- `0xa2` [Telematics: Coordinates](nav/a2.md) has a large number of parameters and numerous types, so it's broken down in detail.
- `0x21` [Menu Text: Telephone](telephone/21.md) has a medium number of parameters/types, so it's not broken down to the same degree as `0xa2`.
- `0x7a` [Door/Lid Status](gm/7a.md) has a small number of parameters of only the bitfield type. As the bitfield is comprised of multiple, smaller combination bitfields, each combination bitfield broken down in detail.
- `0x5b` [Cluster Indicators](lcm/5b.md), like `0x7a`, has a small number of parameters, but has *effectively* no combination bitfields, i.e. 1 bit = 1 distinct thing.

## Use Cases

This section is a newer addition to the documentation format. It arose from needing to decouple the **what** (a feature) from the **how** (a parameter).

*Use Cases* provide a natural fit for worked examples of the command.

Good examples of *Use Cases* are:

- `0x36` [Radio EQ](radio/36.md): _Set EQ Treble_
- `0x40` [OBC Input](gt/40.md): _Setting Time_
- `0x42` [OBC Remote Control](ike/42.md): _Edit Configuration_