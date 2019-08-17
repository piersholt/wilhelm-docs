
# Default


This is the fallback layout which I believe is only used in the event of a Telephone error.

![Default Layout Example](default/IMG_2719.JPG)

The CMT4000 in the 528i would (prior to sourcing a SIM card the size of a surfboard) display "INSERT CARD!" using this layout.

I stumbled upon another message "Phone Connected?" in a random YouTube video which I presume is for the later Motorola V-Series cradles with detachable handsets.

## Create/Update

- can only be created by `0x23`
- there is only a single line
- not possible to use carriage return/link break

![Create Default Layout](default/IMG_2718.JPG)


    C8 <LEN> 3B 23 00 00 "23 00 Default Layout" <CS>


### Flashing Text

[![Default Flash](http://img.youtube.com/vi/Zh3U35ADoQg/0.jpg)](https://www.youtube.com/watch?v=Zh3U35ADoQg)

    # Prefix string with control character 0x01
    C8 <LEN> 3B 23 00 00 "Here is some..." 01 "flashing text!" <CS>


## Inputs

    Default > SOS > SOS		3B 06 C8 31 00 05 08 <CS> # Press
