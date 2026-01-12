# `0xaa` Navigation Control

SES `0x3b` → NAV `0x7f`  
GTF `0x43` → NAV `0x7f`

This command is used to control the navigation view.\
The SES module uses this for POI search and map scale commands.

It is not directly confirmed that this is used by the GTF in the E38, because of their rarity  and the therefore lack of logs.\
But it's very likely, since the GT only accepts this command from the SES and the GTF.\
However, if the source address is the GTF, the only thing you can really do is focus the navigation applet.\
So obviously, the command was extended with the development of the SES module.

### Related Commands

- `0xab` [Navigation View Status](ab.md)

### Example Frames
    
    43 04 7F AA 00 92

    B0 05 7F AA 10 01 71  # Scale 100m
    B0 05 7F AA 10 02 72  # Scale 200m
    B0 05 7F AA 10 04 74  # Scale 500m

For detailed examples, see below!

## Parameters

This message doesn't have a fixed length.

### Focus Navigation (as GTF)

You can send any byte you want if the source is the GTF.\
It will always focus the navigation applet and continue where you left off.

    43 04 7F AA 00 92

### Focus Navigation (as SES)

The SES has more control over the navigation applet.\
You can decide if you want to focus the map directly or the menu.\
It's also possible to switch from menu to map or the other way around.

    B0 05 7F AA 02 00 62  # Focus Menu
    B0 05 7F AA 04 00 62  # Focus Map

### Set Map Scale

The SES has the ability to set the map scale.\
As mentioned above, the GTF is not allowed to do this.

    B0 05 7F AA 10 01 71  # 100m
    B0 05 7F AA 10 02 72  # 200m
    B0 05 7F AA 10 04 74  # 500m
    B0 05 7F AA 10 10 60  # 1km
    B0 05 7F AA 10 11 61  # 2km
    B0 05 7F AA 10 12 62  # 5km
    B0 05 7F AA 10 13 63  # 10m
    B0 05 7F AA 10 14 64  # 20km
    B0 05 7F AA 10 15 64  # 50km
    B0 05 7F AA 10 16 66  # 100km
    B0 05 7F AA 10 18 68  # 200km
    B0 05 7F AA 10 19 69  # 500km
    B0 05 7F AA 10 1A 6A  # 1000km

### Find POIs

The SES has the ability to open the POI browser and search for hotels, petrol stations, parking areas and restaurants.\
This can be done for the current or destination location.

The command will instantly open the list view.

As mentioned above, the GTF is not allowed to do this.


    B0 05 7F AA 20 00 40  # Hotels: at destination
    B0 05 7F AA 20 01 41  # Hotels: at current location
    
    B0 05 7F AA 20 02 42  # Petrol Stations: at destination
    B0 05 7F AA 20 03 43  # Petrol Stations: at current location
    
    B0 05 7F AA 20 04 44  # Parking: at destination
    B0 05 7F AA 20 05 45  # Parking: at current location
    
    B0 05 7F AA 20 06 45  # Restaurants: at destination
    B0 05 7F AA 20 07 45  # Restaurants: at current location
