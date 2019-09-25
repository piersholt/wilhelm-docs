# Controls

## Onboard-Monitor (BMBT)

### Volume Control (Rotary)
### Navigation Control (Rotary)
### Button Controls (Momentary)

## Multifunction Steering Wheel (MFL)

_Note: behaviour varies based on equipment!_


### Multifunction `0x3B`

- Bit field
- R/T is a flag without state
- telephone mode will only be active if telephone has announced and ready

### Back & Forward

### Telephone
Note: depending on year, and options, the button icon may be either a "telephone", or "speaking".

### R/T

### 

MFL

to tel:

R/T 1 = turn on (no other use)


R/T is strictly a signal to the telephon-
will TURN ON if off-.... default connect!
will trigger directory reply...
i suppose the report of 1 is technically for on..
as why else would it send it?


### Volume `0x32`

The **MFL** uses the same command as **BMBT** when the volume controls are used.

Even though the command is the same, the MFL's momentary switches can only "emulate" the BMBT's rotary encoder output. They will emit a direction, but do not support velocity/rate of change. The "step" will always be `1` regardless of the rate at which the switch is used. A higher/lower rate of use will simply send single step commands at a higher/lower rate respectively.

In emulating the rotary encoder, there is no button state, i.e press, hold, and release. If a volume control is held, the MFL will continuously send the same command at a fixed rate.


Bit|7-4|3|2|1|0
:---|:---|:---|:----|:----|:---|:---|:---|:---
Use|Step(s)|--|--|--|Direction|


### Volume Down


	# MFL 0x50
	# TEL 0xC8.
	
	# VOLUME_DOWN = 0b0000_0000
	# STEP_1      = 0b0001_0000
	# VOLUME_DOWN OR STEP_1 = 0b0001_0000 => 0x10
	
	# Volume Down
	50 04 C8 32 10 BF
	

### Volume Up

	# MFL 0x50
	# TEL 0xC8.
	
	# VOLUME_UP = 0b0000_0001
	# STEP_1    = 0b0001_0000
	# VOLUME_UP OR STEP_1 = 0b0001_0001 => 0x11
	
	# Volume Up Press
	50 04 C8 32 11 BF
	
	
	50 04 C8 32 11 BF