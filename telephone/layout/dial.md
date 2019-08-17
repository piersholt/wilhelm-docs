
# Dial

![Example Dial Layout](dial/IMG_2774.JPG)

## Create

There's not a great deal one can do here.

I have attempted to update the various fields to set a new value that is returned by `0x31`, but without success.

Maybe the only thing worth noting is that the second argument is `0x02`, which is what is returned by `0x31` when a digit is selected (as it is with Pin-Code). Also, that the third argument- `0x20`, has the flush bit set. These might be used by the older GT, or MID?

    # Open Dial/Home
    C8 06 3B 21 42 02 20 B4
    #               ^ *
    # ^ value returned by 0x31
    # * flush bit set 0b0010_0000 => 0x20

## Input

_NOTE: Last Numbers is in a separate doc._

    # Press event
    Input > Dial > Digit > 0             3B 06 C8 31 42 02 00 <CS>
    Input > Dial > Digit > 1             3B 06 C8 31 42 02 01 <CS>
    Input > Dial > Digit > 2             3B 06 C8 31 42 02 02 <CS>
    Input > Dial > Digit > 3             3B 06 C8 31 42 02 03 <CS>
    Input > Dial > Digit > 4             3B 06 C8 31 42 02 04 <CS>
    Input > Dial > Digit > 5             3B 06 C8 31 42 02 05 <CS>
    Input > Dial > Digit > 6             3B 06 C8 31 42 02 06 <CS>
    Input > Dial > Digit > 7             3B 06 C8 31 42 02 07 <CS>
    Input > Dial > Digit > 8             3B 06 C8 31 42 02 08 <CS>
    Input > Dial > Digit > 9             3B 06 C8 31 42 02 09 <CS>
    Input > Dial > Digit > <-            3B 06 C8 31 42 02 0a <CS>
    Input > Dial > Digit > *             3B 06 C8 31 42 02 1a <CS>
    Input > Dial > Digit > #             3B 06 C8 31 42 02 1b <CS>

    Input > Dial > SOS   > SOS           3B 06 C8 31 42 05 08 <CS>

    Input > Dial > Open  > Messaging     3B 06 C8 31 42 07 1d <CS>
    Input > Dial > Open  > Directory     3B 06 C8 31 42 07 1f <CS>

    Input > Dial > Info  > Info          3B 06 C8 31 42 08 0a <CS>

    # Note: selecting Top 8 sends command 0x20

    # Hold and Release add 0x20 and 0x40 respectively to last byte
    # Example: Input Dial Digit 7
    3B 06 C8 31 42 02 07 <CS> # Press
    3B 06 C8 31 42 02 27 <CS> # Hold
    3B 06 C8 31 42 02 47 <CS> # Release

## Update

### Digits

![Dial Layout Digits](dial/IMG_2756.JPG)

    # Dial number buffer
    # factory telephone has leading character "_", i.e. "123_"
    C8 <LEN> 3B 23 63 00 "5551234" <CS>

    # Clear number buffer
    C8 05 3B 23 61 20 94
    #              ^
    # Factory unit sets IKE argument regardless of sending to GT,
    # or broadcast.


The factory usually has a leading character \"_\"
