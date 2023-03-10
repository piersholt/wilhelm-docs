# `0xaa` Voice Input

## Use Cases

### Navigation

#### Map Scale (KM)

> When the map mode has been activated, you can call up all valid scales with the commands *"scale 400 feet"* to *"scale 50 miles"*.
> 
> Valid scales are:  
> - 400 or 800 feet  > - 0.25, 0.5, 1, 2.5, 5, 10, 25 or 50 miles.

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

#### Information

> **Information on current position or destination**  
> 
> Following the command *"gas station at current location"* all gas stations in your vicinity are listed on the on-board computer.
> 
> If you have entered a destination in the navigation system, you can **also** call up with the command *"gas station at destination"* a list of all gas stations in the vicinity of the destination specified. Browse up and down the list with the rotary knob for the on-board computer.
> 
> The same principle applies to calling up information on **parking lots**, **hotels** or **restaurants**.

    B0 05 7F AA 20 00 40  # Hotels: at destination
    B0 05 7F AA 20 01 41  # Hotels: at current location
    
    B0 05 7F AA 20 02 42  # Petrol Stations: at destination
    B0 05 7F AA 20 03 43  # Petrol Stations: at current location
    
    B0 05 7F AA 20 04 44  # Parking: at destination
    B0 05 7F AA 20 05 45  # Parking: at current location
    
    B0 05 7F AA 20 06 45  # Restaurants: at destination
    B0 05 7F AA 20 07 45  # Restaurants: at current location