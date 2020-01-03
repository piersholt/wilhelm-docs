# `0x42` Remote Control

![Remote Control Programming](prog/prog.JPG)

On vehicles equpped with a high cluster (IKE), various parameters can be recalled on the cluster's character display.

 - it's always 12 bytes
 - the order is not important
 - used by IKE to render display
 - used by GT to set options

ID | Property
:--|---------
`0x01` | Time
`0x02` | Date
`0x04` | Consump. 1
`0x05` | Consump. 2
`0x06` | Range
`0x07` | Distance
`0x08` | Arrival
`0x09` | Limit
`0x0a` | Avg. Speed
`0x0e` | Timer
`0x0f` | [Aux.] Timer 1
`0x10` | [Aux.] Timer 2
`0xff` | No Function