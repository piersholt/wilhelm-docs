# `0xaa` SES Navigation Control

SES `0xb0` → NAV `0x7f`

Controls navigation views, spoken instructions, route functions, POI searches and map scales through SES.

### Related Commands

- `0xaf` [SES Navigation Status](af.md)
- `0xaa` [GTF Navigation Control](../nav/aa.md)

### Example Frames

    B0 05 7F AA 06 00 66  # Instruction on
    B0 05 7F AA 0B 00 6B  # Save current position
    B0 05 7F AA 10 01 71  # Scale 100m
    B0 05 7F AA 20 03 43  # Petrol stations: at current location

## Parameters

Fixed length. Two data bytes.

### Navigation Controls

| Data    | Function |
|:--------|:---------|
| `00 00` | Instruction off |
| `01 00` | Set SES navigation-audio session |
| `02 00` | Focus navigation menu (`Navigation`) |
| `04 00` | Focus map (`Route map`) |
| `06 00` | Instruction on |
| `07 00` | Request navigation status |
| `08 00` | New route |
| `0B 00` | Save current position |

    B0 05 7F AA 00 00 60  # Instruction off
    B0 05 7F AA 01 00 61  # Set SES navigation-audio session
    B0 05 7F AA 02 00 62  # Focus navigation menu
    B0 05 7F AA 04 00 64  # Focus map
    B0 05 7F AA 06 00 66  # Instruction on
    B0 05 7F AA 07 00 67  # Request navigation status
    B0 05 7F AA 08 00 68  # New route
    B0 05 7F AA 0B 00 6B  # Save current position

`Instruction on` enables spoken navigation instructions.\
`Instruction off` disables them.

`New route` enters the alternate-route function with a 5 km avoid distance.

`Save current position` stores the current vehicle position through the navigation address/location function.

The status request causes NAV to answer using `0xaf` [SES Navigation Status](af.md).

Bit 6 (`0x40`) of the second data byte is handled independently of the fixed control values.\
When set, it clears the SES navigation-audio session state established by `01 00`.

### Set Map Scale

    B0 05 7F AA 10 01 71  # 100m
    B0 05 7F AA 10 02 72  # 200m
    B0 05 7F AA 10 04 74  # 500m
    B0 05 7F AA 10 10 60  # 1km
    B0 05 7F AA 10 11 61  # 2km
    B0 05 7F AA 10 12 62  # 5km
    B0 05 7F AA 10 13 63  # 10km
    B0 05 7F AA 10 14 64  # 20km
    B0 05 7F AA 10 15 65  # 50km
    B0 05 7F AA 10 16 66  # 100km
    B0 05 7F AA 10 18 68  # 200km
    B0 05 7F AA 10 19 69  # 500km
    B0 05 7F AA 10 1A 6A  # 1000km

### Find POIs

SES can open the POI browser and search around either the route destination or current vehicle location.

    B0 05 7F AA 20 00 40  # Hotels: at destination
    B0 05 7F AA 20 01 41  # Hotels: at current location

    B0 05 7F AA 20 02 42  # Petrol stations: at destination
    B0 05 7F AA 20 03 43  # Petrol stations: at current location

    B0 05 7F AA 20 04 44  # Parking: at destination
    B0 05 7F AA 20 05 45  # Parking: at current location

    B0 05 7F AA 20 06 46  # Restaurants: at destination
    B0 05 7F AA 20 07 47  # Restaurants: at current location
