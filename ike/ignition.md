# `0x11` Ignition

The cluster (IKE or KOMBI) will broadcast the ignition status:

 - when the ignition switch position changes
 - periodically while at KL-R (position 1) or greater
 - periodically at KL-30 (position 0) while bus remains active
 - in response to a module announcement (`0x02`)
 - when ignition status is requested (`0x10`: Ignition Request)
 
A number of modules will not activate unless the required ignition status is broadcast by the cluster. For example, while the navigation computer has a KL-R supply circuit, it will not wake until the cluster broadcasts a KL-R ignition status.

#### Check your fuses!

It's not the ignition switch position itself that drives the ignition status, but the associated supply circuit to the cluster that the switch closes. Thus, if the applicable supply is not closed due to a blown fuse, the cluster will not broadcast the applicable igntition status.

## Ignition `0b0000_0111`

The command has a single byte bit field, of which the least significant 3 bits are represent ignition state.

    KL_30   = 0b0000_0000   # Position 0
    KL_R    = 0b0000_0001   # Position 1
    KL_15   = 0b0000_0011   # Position 2
    KL_50   = 0b0000_0111   # Position 3

### Examples

    80 04 BF 11 00 2A   # KL-30
    80 04 BF 11 01 2B   # KL-R
    80 04 BF 11 03 29   # KL-15
    80 04 BF 11 07 2D   # KL-50

---

# `0x10` Ignition Request

A device can request ignition status.

### Examples

    18 03 80 10 8B  # CDC
    30 03 80 10 A3  # CCM
    3B 03 80 10 A8  # GT
    AC 03 80 10 3F  # EHC
    ED 03 80 10 7E  # TV
    F0 03 80 10 63  # BMBT