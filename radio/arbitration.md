Module|Variant|Announce|
:---|:---|:---|
BMBT|4x3|0x01|
BMBT|16x9|0x31|
Radio|C23|0x01|
Radio|BM53|0x01|
GT|VM|0x11|
GT|Nav. (MK1, MK4)|0x41|

Module|Variant|Note|Command|Argument|
:---|:---|:---|:---|:---|
GT|MK1|Ignition|0x45|0b0000_0000
GT|VM|Ignition|0x45|0b0000_0000|
GT|VM|Ignition|0x46|0b0000_0001|
Radio|C23|Hide Overlay|0x46|0b0000_1110
GT|MK1|Menu|0x45|0b0000_0001
Radio|C23|Menu|0x46|0b0000_0001
Radio|C23|Turn Off|0x46|0b0000_1110
Radio|C23|Hide Tone|0x46|0b0000_1000
GT|MK1|Audio OBC|0x45|0b0000_0011




## GT: MK1, BMBT: Wide, Radio: None


### Ignition (KL-R)
    bmbt    glo_l	PONG      	status: 0x30 
    tv      glo_h	PONG      	status: 0x01 (Announce)
    
    # enter announce/ignition loop... x5
    ike     glo_l	IGN       	position: 0x01 (Ignition: KL-R (Pos. I))
    bmbt    glo_l	PONG      	status: 0x31 
    
    # then Vid. GT comes to party...
    gt      glo_l	PONG      	status: 0x41 
    
    # which causes another igntion
    ike     glo_l	IGN       	position: 0x01 (Ignition: KL-R (Pos. I))
    
    # which it's then a normal announce
    gt      glo_l	PONG      	status: 0x40 
    
    gt      rad	    SRC-SND   	00 00
    # setup code, limit, timer, date time, OBC....
    
    gt      rad	    UI-GT     	config: 00 ((0000 0000) )

## GT: MK1, BMBT: Wide, Radio: C23

### KL-30

    bmbt    glo_l	PONG      	status: 0x31 
    # lots of ignition etc
    gt	glo_l	PONG      	status: 0x41 (3B/7F -> BF [Announce])
    
### Ignition (KL-R)

    rad     glo_h   PONG      	status: 0x01 (Announce)
    rad     bmbt    RAD-LED   	led: 0x90 ((LED) Off (Reset))
    rad     bmbt    RAD-LED   	led: 0x48 ((Tape) Stop)
    
    # stuff doing it's thing
    rad     bmbt    RAD-LED   	led: 0x48 ((Tape) Stop)
    bmbt    rad     TAPE      	control: 0x06 (Tape) / mode: 0x30 (Tape / Stopped)
    
    # another ignition so BMBT announces again...
    tv      glo_h   PONG      	status: 0x01 (Announce)
    ike     glo_l   IGN       	position: 0x01 (Ignition: KL-R (Pos. I))
    bmbt    glo_l   PONG      	status: 0x31 
    rad     bmbt    RAD-LED   	led: 00 ((LED) Off)
    rad     bmbt    RAD-LED   	led: 0x90 ((LED) Off (Reset))
    bmbt    rad     TAPE      	control: 0x06 (Tape) / mode: 0x30 (Tape / Stopped)
    bmbt    rad     TAPE      	control: 0x06 (Tape) / mode: 0x30 (Tape / Stopped)
    
    # GT sets it's up again...
    gt	rad	UI-GT     	config: 00 ((0000 0000) )
    rad	gt	UI-RAD    	state: 0x01 ((0000 0001) Hide: --, Main Menu: [ON])
    
    # then we go into BAU
    bmbt	rad	PING   
    rad	glo_h	PONG      	status: 00 (Reply)
    bmbt	rad	PING 
    rad	glo_h	PONG      	status: 00 (Reply)


### Radio On...

#### hide overlay

    bmbt  rad	BMBT-RAD* 	0x30 (0011 0000) :bmbt_overlay   	[Overlay]      	Press 
    rad   gt	UI-RAD    	state: 0x0e ((0000 1110) Hide: Menu, Hide Header: [ON])
    bmbt  rad	BMBT-RAD* 	0xb0 (1011 0000) :bmbt_overlay   	[Overlay]      	Release
    
#### menu button
    bmbt  glo_h	BMBT-GLO  	0x34 (0011 0100) :bmbt_menu      	[Menu]         	Press 
    gt    rad	UI-GT     	config: 0x01 ((0000 0001) Main Menu: [ON])
    rad   gt	UI-RAD    	state: 0x01 ((0000 0001) Hide: --, Main Menu: [ON])
    bmbt  glo_h	BMBT-GLO  	0xb4 (1011 0100) :bmbt_menu      	[Menu]         	Release
    
#### radio off
    bmbt    rad     BMBT-RAD* 	0x06 (0000 0110) :bmbt_power     	[Power]        	Press 
    rad     bmbt	RAD-LED   	led: 00 ((LED) Off)
    rad	    gt    	UI-RAD    	state: 0x0e ((0000 1110) Hide: Menu, Hide Header: [ON])
    bmbt    rad     TAPE      	control: 0x06 (Tape) / mode: 0x12 (Tape / (1/A) ▶︎)
    bmbt    rad     BMBT-RAD* 	0x86 (1000 0110) :bmbt_power     	[Power]        	Release
    rad     bmbt    RAD-LED   	led: 0x48 ((Tape) Stop)
    rad     bmbt    RAD-LED   	led: 0x48 ((Tape) Stop)
    bmbt	rad    TAPE      	control: 0x06 (Tape) / mode: 0x30 (Tape / Stopped)
    bmbt	rad    TAPE      	control: 0x06 (Tape) / mode: 0x30 (Tape / Stopped)

#### ignition off -> on (radio on, overlay on)
    # KL-30
    # nada!

    # KL-R
    rad	    glo_h   PONG      	status: 0x01 (Announce)
    rad	    bmbt    RAD-LED   	led: 0x90 ((LED) Off (Reset))
    bmbt    rad     TAPE      	control: 0x06 (Tape) / mode: 0x30 (Tape / Stopped)
    gt      rad     SRC-SND   	00 00
    rad	    bmbt    RAD-LED   	led: 0xff ((LED) On)
    gt	rad	UI-GT     	config: 00 ((0000 0000) )
    # radio writes as requested
    rad	gt	RAD-23    	gt: 0x40 ((Radio) Set Station) / ike: 0x20 (Reset) / chars: 46 4D 20 03 31 30 35 2E 31 04 20 20 20 ("FM ☐105.1☐   ")
    rad	gt	RAD-21*   	layout: 0x41 ([Radio] Presets) / m2: 0x05 ((0000 0101) Band (0x43): FMA, Preset (0x41), Dolby: (0x83): P5) / m3: 0x60 ((0110 0000) Block: [ON], Flush: [ON], index: "0") / chars: 20 41 31 05 41 32 20 05 20 41 33 05 41 34 20 05 2A 41 35 05 41 36 20 (" A1☐A2 ☐ A3☐A4 ☐*A5☐A6 ")
    rad	gt	RAD-21*   	layout: 0x43 ([Radio] Source) / m2: 00 ((0000 0000) Band (0x43): FMA, Preset (0x41), Dolby: (0x83): No Preset) / m3: 0x06 ((0000 0110) index: "6") / chars: 46 4D 05 41 4D 05 53 43 05 20 20 05 54 41 50 45 05 20 20 20 ("FM☐AM☐SC☐  ☐TAPE☐   ")
    
    # Tone
    bmbt	rad	BMBT-RAD* 	0x04 (0000 0100) :bmbt_tone      	[Tone]         	Press 
    bmbt	rad	BMBT-RAD* 	0x84 (1000 0100) :bmbt_tone      	[Tone]         	Release
    rad	gt	RAD-ALT   	mode: 0x80 ((Tone) EQ. Set) / opts: 00 00 10 ( 16 )
    rad	gt	UI-RAD    	state: 0x08 ((0000 1000) Hide: Tone)

#### Audio+OBC

    # Enable Audio OBC
    gt	rad	UI-GT     	config: 0x03 ((0000 0011) Audio+OBC (MK1/TV): [ON], Main Menu: [ON])
    rad	gt	UI-RAD    	state: 0x01 ((0000 0001) Hide: --, Main Menu: [ON])
    
    # hide overlay (radio on)
    bmbt	rad	BMBT-RAD* 	0x30 (0011 0000) :bmbt_overlay   	[Overlay]      	Press 
    brad	gt	UI-RAD    	state: 0x0e ((0000 1110) Hide: Menu, Hide Header: [ON])
    bmbt	rad	BMBT-RAD* 	0xb0 (1011 0000) :bmbt_overlay   	[Overlay]      	Release
    
    # radio off
    bmbt    rad     BMBT-RAD* 	0x06 (0000 0110) :bmbt_power     	[Power]        	Press 
    rad     bmbt    RAD-LED   	led: 00 ((LED) Off)
    rad     gt      UI-RAD    	state: 0x0e ((0000 1110) Hide: Menu, Hide Header: [ON])
    bmbt    rad     TAPE      	control: 0x06 (Tape) / mode: 0x30 (Tape / Stopped)
    bmbt    rad     BMBT-RAD* 	0x86 (1000 0110) :bmbt_power     	[Power]        	Release
    
    # Disable Audio OBC
    bmbt    gt	BMBT-GT*  	0x05 (0000 0101) :bmbt_confirm   	[Confirm]      	Press 
    gt      rad	UI-GT     	config: 0x01 ((0000 0001) Main Menu: [ON])
    bmbt    gt	BMBT-GT*  	0x85 (1000 0101) :bmbt_confirm   	[Confirm]      	Release
    rad     gt	UI-RAD    	state: 0x01 ((0000 0001) Hide: --, Main Menu: [ON])
    
    # Enable Audio OBC (radio on)
    gt      rad	UI-GT     	config: 0x03 ((0000 0011) Audio+OBC (MK1/TV): [ON], Main Menu: [ON])
    rad     gt	UI-RAD    	state: 0x01 ((0000 0001) Hide: --, Main Menu: [ON])


## GT: MK3 (VM), BMBT: Wide, Radio: None

### KL-30

    gt      rad     SRC-SND     00 00 
    bmbt    glo_l   PONG        status: 0x31 
    bmbt    rad     TAPE        control: 0x06 (Tape) / mode: 0x30 (Tape / Stopped)
    gt      glo_h   PONG        status: 0x11
    tv      glo_h   PONG        status: 0x01 (Announce)
    tv      bmbt    PING        --
    bmbt    tv      PONG        status: 0x30
    
### Ignition (KL-R)

    # usual stuff then...
    gt	rad	SRC-SND   	00 00
    # switch LC to correct mode...
    tv	bmbt	TV-BMBT*  	a: 0x12 ((0001 0010) Power: [ON], Source: [Vid. GT]) / b: 0x11 ((0001 0001) Aspect Ratio: [16:9], Encoding: [NTSC])
    # familiar
    bmbt	glo_l	PONG      	status: 0x31 
    gt	glo_h	PONG      	status: 0x11 (3B -> FF [Announce])
    tv	glo_h	PONG      	status: 0x01 (Announce)
    tv	bmbt	PING 
    bmbt	tv	PONG      	status: 0x30 (F0 -> 3B [Reply])
    
    # lots of set up OBC etc...

    # GT kicks in
    gt	bmbt	GT-BMBT*  	a: 0x12 ((0001 0010) Power: [ON], Source: [Vid. GT])

    # then tries to get radio... (bmbt pinging int he mean time)
    gt      rad     UI-GT     	config: 0x01 ((0000 0001) Main Menu: [ON])
    gt      rad     UI-GT     	config: 0x01 ((0000 0001) Main Menu: [ON])
    bmbt    rad     PING      	--
    gt      rad     UI-GT     	config: 0x01 ((0000 0001) Main Menu: [ON])
    gt      rad     UI-GT     	config: 0x01 ((0000 0001) Main Menu: [ON])
    bmbt    rad     PING      	--
    gt      rad     UI-GT     	config: 0x01 ((0000 0001) Main Menu: [ON])
    bmbt    rad     PING      	--
     

#### Menu
    # Regardless of radio state
    gt	rad	UI-GT     	config: 0x01 ((0000 0001) Main Menu: [ON])
    
#### Ignition Off (KL-30)
    gt	bmbt GT-BMBT*  	a: 0x02 ((0000 0010) Power: [OFF], Source: [Vid. GT])

     
     
remove battery.. plug radio in..

## GT: MK3 (VM), BMBT: Wide, Radio: C23

### KL-30

    # we know this...
    gt	rad	SRC-SND   	00 00
    # lots of OBC, date tie stuff... and as above..
    
### Ignition (KL-R)

    rad	glo_h	PONG      	status: 0x01 (Announce)
    rad	bmbt	RAD-LED   	led: 0x90 ((LED) Off (Reset))
    rad	bmbt	RAD-LED   	led: 0x48 ((Tape) Stop)
    
    # similar to no radio.. GT eventually kicks in
    gt	bmbt	GT-BMBT*  	a: 0x12 ((0001 0010) Power: [ON], Source: [Vid. GT])
    gt	rad	UI-GT     	config: 0x01 ((0000 0001) Main Menu: [ON])
    rad	gt	UI-RAD    	state: 0x01 ((0000 0001) Hide: --, Main Menu: [ON])
    
    # then alive loop begins...
    
#### Radio On

    # pretty similr stuff
    bmbt	rad	BMBT-RAD* 	0x06 (0000 0110) :bmbt_power     	[Power]        	Press 
    rad	bmbt	RAD-LED   	led: 0xff ((LED) On)
    bmbt	rad	TAPE      	control: 0x06 (Tape) / mode: 0x30 (Tape / Stopped)
    bmbt	rad	BMBT-RAD* 	0x86 (1000 0110) :bmbt_power     	[Power]        	Release
    # UI
    rad	gt	RAD-23    	gt: 0x40 ((Radio) Set Station) / ike: 0x20 (Reset) / chars: 46 4D 20 03 31 30 35 2E 31 04 20 20 20 ("FM ☐105.1☐   ")
    rad	gt	RAD-21*   	layout: 0x41 ([Radio] Presets) / m2: 0x05 ((0000 0101) Band (0x43): FMA, Preset (0x41), Dolby: (0x83): P5) / m3: 0x60 ((0110 0000) Block: [ON], Flush: [ON], index: "0") / chars: 20 41 31 05 41 32 20 05 20 41 33 05 41 34 20 05 2A 41 35 05 41 36 20 (" A1☐A2 ☐ A3☐A4 ☐*A5☐A6 ")
    rad	gt	RAD-21*   	layout: 0x43 ([Radio] Source) / m2: 00 ((0000 0000) Band (0x43): FMA, Preset (0x41), Dolby: (0x83): No Preset) / m3: 0x06 ((0000 0110) index: "6") / chars: 46 4D 05 41 4D 05 53 43 05 20 20 05 54 41 50 45 05 20 20 20 ("FM☐AM☐SC☐  ☐TAPE☐   ")
    rad	gt	RAD-21*   	layout: 0x41 ([Radio] Presets) / m2: 0x05 ((0000 0101) Band (0x43): FMA, Preset (0x41), Dolby: (0x83): P5) / m3: 0x60 ((0110 0000) Block: [ON], Flush: [ON], index: "0") / chars: 20 41 31 05 41 32 20 05 20 41 33 05 41 34 20 05 2A 41 35 05 41 36 20 (" A1☐A2 ☐ A3☐A4 ☐*A5☐A6 ")
    rad	gt	RAD-21*   	layout: 0x43 ([Radio] Source) / m2: 00 ((0000 0000) Band (0x43): FMA, Preset (0x41), Dolby: (0x83): No Preset) / m3: 0x06 ((0000 0110) index: "6") / chars: 46 4D 05 41 4D 05 53 43 05 20 20 05 54 41 50 45 05 20 20 20 ("FM☐AM☐SC☐  ☐TAPE☐   ")

    # then into BAU... 
    
##### Hide Overlay

    bmbt	rad	BMBT-RAD* 	0x30 (0011 0000) :bmbt_overlay   	[Overlay]      	Press 
    rad	gt	UI-RAD    	state: 0x0e ((0000 1110) Hide: Menu, Hide Header: [ON])
    bmbt	rad	BMBT-RAD* 	0xb0 (1011 0000) :bmbt_overlay   	[Overlay]      	Release
    
##### Power Off

    bmbt	rad	BMBT-RAD* 	0x06 (0000 0110) :bmbt_power     	[Power]        	Press 
    rad	bmbt	RAD-LED   	led: 00 ((LED) Off)
    rad	gt	UI-RAD    	state: 0x0e ((0000 1110) Hide: Menu, Hide Header: [ON])
    bmbt	rad	TAPE      	control: 0x06 (Tape) / mode: 0x30 (Tape / Stopped)
    bmbt	rad	BMBT-RAD* 	0x86 (1000 0110) :bmbt_power     	[Power]        	Release
    
##### Ignition Off
    
    # Nada, like before!
    
#### Ignition Off (with radio on)

    rad	bmbt	RAD-LED   	led: 0x90 ((LED) Off (Reset))
    rad	bmbt	RAD-LED   	led: 0xff ((LED) On)
    gt	rad	UI-GT     	config: 00 ((0000 0000) )
    rad	gt	RAD-23    	gt: 0x40 ((Radio) Set Station) / ike: 0x20 (Reset) / chars: 46 4D 20 03 31 30 35 2E 31 04 20 20 20 ("FM ☐105.1☐   ")
    rad	gt	RAD-21*   	layout: 0x41 ([Radio] Presets) / m2: 0x05 ((0000 0101) Band (0x43): FMA, Preset (0x41), Dolby: (0x83): P5) / m3: 0x60 ((0110 0000) Block: [ON], Flush: [ON], index: "0") / chars: 20 41 31 05 41 32 20 05 20 41 33 05 41 34 20 05 2A 41 35 05 41 36 20 (" A1☐A2 ☐ A3☐A4 ☐*A5☐A6 ")
    rad	gt	RAD-21*   	layout: 0x43 ([Radio] Source) / m2: 00 ((0000 0000) Band (0x43): FMA, Preset (0x41), Dolby: (0x83): No Preset) / m3: 0x06 ((0000 0110) index: "6") / chars: 46 4D 05 41 4D 05 53 43 05 20 20 05 54 41 50 45 05 20 20 20 ("FM☐AM☐SC☐  ☐TAPE☐   ")

### Audio+OBC

    # radio on, hit MENU
    gt	rad	UI-GT     	config: 0x01 ((0000 0001) Main Menu: [ON])
    rad	gt	UI-RAD    	state: 0x01 ((0000 0001) Hide: --, Main Menu: [ON])
    
    # enable Audio + OBC (radio doesn't display)
    gt	rad	UI-GT     	config: 0x03 ((0000 0011) Audio+OBC (MK1/TV): [ON], Main Menu: [ON])
    rad	gt	UI-RAD    	state: 0x01 ((0000 0001) Hide: --, Main Menu: [ON])
    
    # show overlay, then hide it
    bmbt	rad	BMBT-RAD* 	0x30 (0011 0000) :bmbt_overlay   	[Overlay]      	Press 
    rad	gt	UI-RAD    	state: 0x0e ((0000 1110) Hide: Menu, Hide Header: [ON])
    bmbt	rad	BMBT-RAD* 	0xb0 (1011 0000) :bmbt_overlay   	[Overlay]      	Release
    
    # show then MENU
    bmbt	glo_h	BMBT-GLO  	0x34 (0011 0100) :bmbt_menu      	[Menu]         	Press 
    gt	rad	UI-GT     	config: 0x03 ((0000 0011) Audio+OBC (MK1/TV): [ON], Main Menu: [ON])
    rad	gt	UI-RAD    	state: 0x01 ((0000 0001) Hide: --, Main Menu: [ON])
    bmbt	glo_h	BMBT-GLO  	0xb4 (1011 0100) :bmbt_menu      	[Menu]         	Release
    
    # show then ignition off
    # nothing!
    
    # ignition back on (audio obc enabled of course...)
    rad	glo_h	PONG      	status: 0x01 (Announce)
    rad	bmbt	RAD-LED   	led: 0x90 ((LED) Off (Reset))
    rad	bmbt	RAD-LED   	led: 0xff ((LED) On)
    # as expected...
    gt	rad	UI-GT     	config: 0x02 ((0000 0010) Audio+OBC (MK1/TV): [ON])
    # and radio draws... 
    rad	gt	RAD-23    	gt: 0x40 ((Radio) Set Station) / ike: 0x20 (Reset) / chars: 46 4D 20 03 31 30 35 2E 31 04 20 20 20 ("FM ☐105.1☐   ")
    rad	gt	RAD-21*   	layout: 0x41 ([Radio] Presets) / m2: 0x05 ((0000 0101) Band (0x43): FMA, Preset (0x41), Dolby: (0x83): P5) / m3: 0x60 ((0110 0000) Block: [ON], Flush: [ON], index: "0") / chars: 20 41 31 05 41 32 20 05 20 41 33 05 41 34 20 05 2A 41 35 05 41 36 20 (" A1☐A2 ☐ A3☐A4 ☐*A5☐A6 ")
    rad	gt	RAD-21*   	layout: 0x43 ([Radio] Source) / m2: 00 ((0000 0000) Band (0x43): FMA, Preset (0x41), Dolby: (0x83): No Preset) / m3: 0x06 ((0000 0110) index: "6") / chars: 46 4D 05 41 4D 05 53 43 05 20 20 05 54 41 50 45 05 20 20 20 ("FM☐AM☐SC☐  ☐TAPE☐   ")

## GT: MK3 (VM), BMBT: Wide, Radio: BM53

### Ignition (KL-R)
    
    rad	glo_l	PONG      	status: 0x01 (Announce)
    rad	bmbt	RAD-LED   	led: 00 ((LED) Off)
    bmbt	rad	TAPE      	control: 0x06 (Tape) / mode: 0x30 (Tape / Stopped)
    # Radio Off
    gt	rad	UI-GT     	config: 00 ((0000 0000) )
    rad	gt	UI-RAD    	state: 0x01 ((0000 0001) Hide: --, Main Menu: [ON])
    
### Radio On
    
    # BM53 doesn't seem to write at power on?
    bmbt rad	BMBT-RAD* 	0x06 (0000 0110) :bmbt_power     	[Power]        	Press 
    rad bmbt	RAD-LED   	led: 0x90 ((LED) Off (Reset))
    rad bmbt	RAD-LED   	led: 0x5f ((Tape) Dolby OFF)
    rad	cd      CDC-REQ   	control: 00 (Status!) / mode: 00 (mode: "00")
    rad	cdc     CDC-REQ   	control: 00 (Status!) / mode: 00 (mode: "00")
    bmbt rad	TAPE      	control: 0x06 (Tape) / mode: 0x30 (Tape / Stopped)
    bmbt rad	BMBT-RAD* 	0x86 (1000 0110) :bmbt_power     	[Power]        	Release
    bmbt rad	TAPE      	control: 0x06 (Tape) / mode: 0x81 (Tape / Dolby Off)
    rad bmbt	RAD-LED   	led: 0x5f ((Tape) Dolby OFF)
    bmbt rad	TAPE      	control: 0x06 (Tape) / mode: 0x81 (Tape / Dolby Off)
    rad bmbt	RAD-LED   	led: 0xff ((LED) On)
    bmbt rad	TAPE      	control: 0x06 (Tape) / mode: 0x30 (Tape / Stopped)
    
### Overlay (Show)
    
    bmbt	rad	BMBT-RAD* 	0x30 (0011 0000) :bmbt_overlay   	[Overlay]      	Press 
    rad	    gt	RAD-A5*   	layout: 0x62 (Header) / padding: 0x01 (No Padding) / zone: 0x41 ((0100 0001) Block: [ON], Zone: A/1) / chars: 20 46 4D 41 20 (" FMA ")
    rad	    gt	RAD-A5*   	layout: 0x62 (Header) / padding: 0x01 (No Padding) / zone: 0x42 ((0100 0010) Block: [ON], Zone: B/2) / chars: 20 50 20 32 20 (" P 2 ")
    rad	    gt	RAD-A5*   	layout: 0x62 (Header) / padding: 0x01 (No Padding) / zone: 0x43 ((0100 0011) Block: [ON], Zone: C/3) / chars: 20 20 20 20 20 ("     ")
    rad	    gt	RAD-A5*   	layout: 0x62 (Header) / padding: 0x01 (No Padding) / zone: 0x44 ((0100 0100) Block: [ON], Zone: D/4) / chars: 20 20 20 20 20 ("     ")
    bmbt	rad	BMBT-RAD* 	0xb0 (1011 0000) :bmbt_overlay   	[Overlay]      	Release
    rad	gt	RAD-A5*   	layout: 0x62 (Header) / padding: 0x01 (No Padding) / zone: 0x45 ((0100 0101) Block: [ON], Zone: E/5) / chars: 20 20 52 44 53 20 20 ("  RDS  ")
    rad	gt	RAD-A5*   	layout: 0x62 (Header) / padding: 0x01 (No Padding) / zone: 0x46 ((0100 0110) Block: [ON], Zone: H2/6) / chars: 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 ("                    ")
    rad	gt	RAD-A5*   	layout: 0x62 (Header) / padding: 0x01 (No Padding) / zone: 0x07 ((0000 0111) Zone: H3/7) / chars: 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 ("                    ")
    rad	gt	RAD-23    	gt: 0x62 ((RDS)) / ike: 0x10 (Overwrite) / chars: 03 31 30 31 2E 39 04 20 20 20 20 20 20 ("☐101.9☐      ")
    gt	rad	TXT-CACHE 	status: 00 (status: "00")
    # BM53 will use "new" bitfield combination (presumably due to no menus)
    rad	gt	UI-RAD    	state: 0x0c ((0000 1100) Hide: Menu)
    
### Menu

    # At this point.. still only:
    gt	rad	UI-GT     	config: 00 ((0000 0000) )
    rad	gt	UI-RAD    	state: 0x01 ((0000 0001) Hide: --, Main Menu: [ON])
    rad	gt	UI-RAD    	state: 0x0c ((0000 1100) Hide: Menu)
    
    bmbt  glo_h	BMBT-GLO  	0x34 (0011 0100) :bmbt_menu      	[Menu]         	Press 
    bmbt  glo_h	BMBT-GLO  	0xb4 (1011 0100) :bmbt_menu      	[Menu]         	Release
    gt    rad	UI-GT     	config: 0x01 ((0000 0001) Main Menu: [ON])
    rad   gt	UI-RAD    	state: 0x01 ((0000 0001) Hide: --, Main Menu: [ON])

### Overlay (Hide)

    bmbt	rad	BMBT-RAD* 	0x30 (0011 0000) :bmbt_overlay   	[Overlay]      	Press 
    rad   gt	UI-RAD    	state: 0x02 ((0000 0010) Hide: --, Hide Header: [ON])
    rad   gt	UI-RAD    	state: 0x0c ((0000 1100) Hide: Menu)
    bmbt	rad	BMBT-RAD* 	0xb0 (1011 0000) :bmbt_overlay   	[Overlay]      	Release
    
### Radio Off

    # still nothing like 0x10 yet..
    rad   bmbt	RAD-LED   	led: 00 ((LED) Off)
    rad   gt	UI-RAD    	state: 0x02 ((0000 0010) Hide: --, Hide Header: [ON])
    bmbt  rad	TAPE      	control: 0x06 (Tape) / mode: 0x30 (Tape / Stopped)
    bmbt  rad	BMBT-RAD* 	0x86 (1000 0110) :bmbt_power     	[Power]        	Release
    
### Menu (Radio Off)

    bmbt  glo_h	BMBT-GLO  	0x34 (0011 0100) :bmbt_menu      	[Menu]         	Press 
    bmbt  glo_h	BMBT-GLO  	0xb4 (1011 0100) :bmbt_menu      	[Menu]         	Release
    gt    rad	UI-GT     	config: 0x01 ((0000 0001) Main Menu: [ON])
    rad   gt	UI-RAD    	state: 0x01 ((0000 0001) Hide: --, Main Menu: [ON])

### Ignition (KL-30) (Radio Off)

    # Nada!

### Ignition (KL-R) (Radio Off)
    
    # As before...
    gt	rad	UI-GT     	config: 00 ((0000 0000) )
    rad	gt	UI-RAD    	state: 0x01 ((0000 0001) Hide: --, Main Menu: [ON])

### Radio On, Overlay On, Ignition (KL-30)

    # Radio On
    bmbt	rad	BMBT-RAD* 	0x06 (0000 0110) :bmbt_power     	[Power]        	Press 
    rad	bmbt	RAD-LED   	led: 0x90 ((LED) Off (Reset))
    rad	bmbt	RAD-LED   	led: 0x5f ((Tape) Dolby OFF)
    rad	bmbt	RAD-LED   	led: 0x5f ((Tape) Dolby OFF)
    bmbt	rad	TAPE      	control: 0x06 (Tape) / mode: 0x30 (Tape / Stopped)
    bmbt	rad	TAPE      	control: 0x06 (Tape) / mode: 0x81 (Tape / Dolby Off)
    rad	bmbt	RAD-LED   	led: 0x5f ((Tape) Dolby OFF)
    bmbt	rad	TAPE      	control: 0x06 (Tape) / mode: 0x81 (Tape / Dolby Off)
    bmbt	rad	BMBT-RAD* 	0x86 (1000 0110) :bmbt_power     	[Power]        	Release
    rad	bmbt	RAD-LED   	led: 0xff ((LED) On)
    bmbt	rad	TAPE      	control: 0x06 (Tape) / mode: 0x30 (Tape / Stopped)
    
    # Overlay
    bmbt	rad	BMBT-RAD* 	0x30 (0011 0000) :bmbt_overlay   	[Overlay]      	Press 
    rad	gt	RAD-A5*   	layout: 0x62 (Header) / padding: 0x01 (No Padding) / zone: 0x41 ((0100 0001) Block: [ON], Zone: A/1) / chars: 20 46 4D 41 20 (" FMA ")
    rad	gt	RAD-A5*   	layout: 0x62 (Header) / padding: 0x01 (No Padding) / zone: 0x42 ((0100 0010) Block: [ON], Zone: B/2) / chars: 20 20 20 20 20 ("     ")
    rad	gt	RAD-A5*   	layout: 0x62 (Header) / padding: 0x01 (No Padding) / zone: 0x43 ((0100 0011) Block: [ON], Zone: C/3) / chars: 20 20 20 20 20 ("     ")
    rad	gt	RAD-A5*   	layout: 0x62 (Header) / padding: 0x01 (No Padding) / zone: 0x44 ((0100 0100) Block: [ON], Zone: D/4) / chars: 20 20 20 20 20 ("     ")
    rad	gt	RAD-A5*   	layout: 0x62 (Header) / padding: 0x01 (No Padding) / zone: 0x45 ((0100 0101) Block: [ON], Zone: E/5) / chars: 20 20 52 44 53 20 20 ("  RDS  ")
    bmbt	rad	BMBT-RAD* 	0xb0 (1011 0000) :bmbt_overlay   	[Overlay]      	Release
    rad	gt	RAD-A5*   	layout: 0x62 (Header) / padding: 0x01 (No Padding) / zone: 0x46 ((0100 0110) Block: [ON], Zone: H2/6) / chars: 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 ("                    ")
    rad	gt	RAD-A5*   	layout: 0x62 (Header) / padding: 0x01 (No Padding) / zone: 0x07 ((0000 0111) Zone: H3/7) / chars: 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 ("                    ")
    gt	rad	TXT-CACHE 	status: 00 (status: "00")
    rad	gt	RAD-23    	gt: 0x62 ((RDS)) / ike: 0x10 (Overwrite) / chars: 03 20 38 37 2E 37 04 20 20 20 20 20 20 ("☐ 87.7☐      ")
    rad	gt	UI-RAD    	state: 0x0c ((0000 1100) Hide: Menu)
    ike	glo_l	IGN       	position: 0x01 (Ignition: KL-R (Pos. I))
    
    # Ignition Off
    ike	glo_l	IGN       	position: 00 (Ignition: KL-30 (Pos. 0))
    gt	nav_jp	SRC-NAV_JP*	02
    gt	bmbt	GT-BMBT*  	a: 0x02 ((0000 0010) Power: [OFF], Source: [Vid. GT])
    rad	bmbt	RAD-LED   	led: 00 ((LED) Off)
    bmbt	rad	TAPE      	control: 0x06 (Tape) / mode: 0x30 (Tape / Stopped)
    rad	gt	UI-RAD    	state: 0x02 ((0000 0010) Hide: --, Hide Header: [ON])
    
    # Ignition On
    rad	    bmbt	RAD-LED   	led: 0x90 ((LED) Off (Reset))
    rad	    bmbt	RAD-LED   	led: 0x5f ((Tape) Dolby OFF)
    rad	    bmbt	RAD-LED   	led: 0x5f ((Tape) Dolby OFF)
    rad	    bmbt	RAD-LED   	led: 0xff ((LED) On)
    bmbt    rad     TAPE      	control: 0x06 (Tape) / mode: 0x30 (Tape / Stopped)
    gt	bmbt	GT-BMBT*  	a: 0x12 ((0001 0010) Power: [ON], Source: [Vid. GT])
    gt	rad	UI-GT     	config: 0x01 ((0000 0001) Main Menu: [ON])
    rad	gt	UI-RAD    	state: 0x01 ((0000 0001) Hide: --, Main Menu: [ON])

_I wonder if this is due to no date/time being set? Won't let Radio draw at KL-R?_

### Set Date/Time...

    # Exit Settings via Menu
    gt	rad	UI-GT     	config: 0x01 ((0000 0001) Main Menu: [ON])
    rad	gt	UI-RAD    	state: 0x01 ((0000 0001) Hide: --, Main Menu: [ON])

### Radio Off, Ignition (KL-30 to KL-R)
    
    # No defaults to home screen
    # No radio change...
    gt	rad	UI-GT     	config: 00 ((0000 0000) )
    rad	gt	UI-RAD    	state: 0x01 ((0000 0001) Hide: --, Main Menu: [ON])

### Trying...

    # Radio On
    # Overlay On
    # Overlay Off
    # Overlay On
    # Radio Off
    # FM Band FMA, FM1, FM2
    # Change presets
    # Menu
    # Still nothing....
    # Mode: Tape
    # Overlay Off
    # Overlay On
    # Menu
    # Nup, still he same...

### Tone

    21:51:36 [INFO ] [     virtual] [             Display] bmbt	rad	BMBT-RAD* 	0x04 (0000 0100) :bmbt_tone      	[Tone]         	Press 
    21:51:36 [INFO ] [     virtual] [             Display] bmbt	rad	BMBT-RAD* 	0x84 (1000 0100) :bmbt_tone      	[Tone]         	Release
    21:51:36 [INFO ] [     virtual] [             Display] rad	gt	RAD-ALT   	mode: 0x86 ((Tone) EQ. Set) / opts: 06 15 13 ( 398611 )
    21:51:37 [INFO ] [     virtual] [             Display] gt	ike	PING      	--
    21:51:37 [INFO ] [     virtual] [             Display] gt	tel	PING      	--
    21:51:37 [INFO ] [     virtual] [             Display] ike	glo_l	PONG      	status: 00 (Reply)
    21:51:37 [INFO ] [     virtual] [             Display] tel	glo_h	PONG      	status: 0x30 (BMBT (Wide)/Tel (Motorola) -> 3B [Reply])
    21:51:37 [INFO ] [     virtual] [             Display] ike	glo_l	IGN       	position: 0x01 (Ignition: KL-R (Pos. I))
    21:51:37 [INFO ] [     virtual] [             Display] ike	anzv	ANZV-BOOL-IKE	control_a: 00 ((0000 0000) (Settings) Memo: [OFF], (OBC) Timer: [OFF], (OBC) Limit: [OFF]) / control_b: 00 ((0000 0000) (Code) Lock: [OFF], (Aux.) Heating: [OFF], (Aux.) Timer 2: [OFF], (Aux.) Vent.: [OFF], (Aux.) Timer 1: [OFF])
    21:51:39 [INFO ] [     virtual] [             Display] rad	dsp	PING      	--
    21:51:40 [INFO ] [     virtual] [             Display] bmbt	rad	PING      	--
    21:51:40 [INFO ] [     virtual] [             Display] rad	glo_l	PONG      	status: 00 (Reply)
    21:51:44 [INFO ] [     virtual] [             Display] rad	gt	UI-RAD    	state: 0x08 ((0000 1000) Hide: Tone)
    21:51:44 [INFO ] [     virtual] [             Display] rad	gt	RAD-A5*   	layout: 0x62 (Header) / padding: 0x01 (No Padding) / zone: 0x41 ((0100 0001) Block: [ON], Zone: A/1) / chars: 20 46 4D 41 20 (" FMA ")
    21:51:44 [INFO ] [     virtual] [             Display] rad	gt	RAD-A5*   	layout: 0x62 (Header) / padding: 0x01 (No Padding) / zone: 0x42 ((0100 0010) Block: [ON], Zone: B/2) / chars: 20 50 20 31 20 (" P 1 ")
    21:51:45 [INFO ] [     virtual] [             Display] rad	gt	RAD-A5*   	layout: 0x62 (Header) / padding: 0x01 (No Padding) / zone: 0x43 ((0100 0011) Block: [ON], Zone: C/3) / chars: 20 20 20 20 20 ("     ")
    21:51:45 [INFO ] [     virtual] [             Display] rad	gt	RAD-A5*   	layout: 0x62 (Header) / padding: 0x01 (No Padding) / zone: 0x44 ((0100 0100) Block: [ON], Zone: D/4) / chars: 20 20 20 20 20 ("     ")
    21:51:45 [INFO ] [     virtual] [             Display] rad	gt	RAD-A5*   	layout: 0x62 (Header) / padding: 0x01 (No Padding) / zone: 0x45 ((0100 0101) Block: [ON], Zone: E/5) / chars: 20 20 52 44 53 20 20 ("  RDS  ")
    21:51:45 [INFO ] [     virtual] [             Display] rad	gt	RAD-A5*   	layout: 0x62 (Header) / padding: 0x01 (No Padding) / zone: 0x46 ((0100 0110) Block: [ON], Zone: H2/6) / chars: 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 ("                    ")
    21:51:45 [INFO ] [     virtual] [             Display] rad	gt	RAD-A5*   	layout: 0x62 (Header) / padding: 0x01 (No Padding) / zone: 0x07 ((0000 0111) Zone: H3/7) / chars: 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 ("                    ")
    21:51:45 [INFO ] [     virtual] [             Display] rad	gt	RAD-23    	gt: 0x62 ((RDS)) / ike: 0x10 (Overwrite) / chars: 03 31 30 31 2E 31 04 20 20 20 20 20 20 ("☐101.1☐      ")
    21:51:45 [INFO ] [     virtual] [             Display] gt	rad	TXT-CACHE 	status: 00 (status: "00")
    21:51:45 [INFO ] [     virtual] [             Display] rad	gt	UI-RAD    	state: 0x0c ((0000 1100) Hide: Menu)
    
    # Hit Menu... still nothing...
    21:52:18 [INFO ] [     virtual] [             Display] bmbt	glo_h	BMBT-GLO  	0x34 (0011 0100) :bmbt_menu      	[Menu]         	Press 
    21:52:18 [WARN ] [         tel] [ Telephone::Emulated] Menu pressed! @layout -> :background
    21:52:18 [INFO ] [     virtual] [             Display] bmbt	glo_h	BMBT-GLO  	0xb4 (1011 0100) :bmbt_menu      	[Menu]         	Release
    21:52:18 [INFO ] [     virtual] [             Display] gt	rad	UI-GT     	config: 0x01 ((0000 0001) Main Menu: [ON])
    21:52:18 [INFO ] [     virtual] [             Display] rad	gt	UI-RAD    	state: 0x01 ((0000 0001) Hide: --, Main Menu: [ON])
    21:52:19 [INFO ] [     virtual] [             Display] rad	dsp	PING      	--

### Select


    rad	gt	UI-RAD    	state: 0x04 ((0000 0100) Hide: Select)
    bmbt	glo_h	BMBT-SOFT 	0x0f (0000 1111) :bmbt_soft_select	[Select]       	Press 
    rad	gt	RAD-ALT   	mode: 0x04 ((Select) "m" Manual Staion Choice) / opts:  ( 0 )
    bmbt	glo_h	BMBT-SOFT 	0x8f (1000 1111) :bmbt_soft_select	[Select]       	Release  
    bmbt	gt	BMBT-GT*  	0x05 (0000 0101) :bmbt_confirm   	[Confirm]      	Press 
    bmbt	gt	BMBT-GT*  	0x85 (1000 0101) :bmbt_confirm   	[Confirm]      	Release
    rad	gt	RAD-ALT   	mode: 0x05 ((Select) "< m >" Manual Staion Choice [Selected]) / opts:  ( 0 )
    rad	gt	RAD-A5*   	layout: 0x62 (Header) / padding: 0x01 (No Padding) / zone: 0x03 ((0000 0011) Zone: C/3) / chars: 20 20 6D 20 20 ("  m  ")
    rad	gt	RAD-A5*   	layout: 0x62 (Header) / padding: 0x01 (No Padding) / zone: 00 ((0000 0000) Zone: 0) / chars:  ("")
    bmbt	gt	BMBT-NAV  	0x81 (1000 0001) :bmbt_right      Right: 1
    rad	gt	RAD-23    	gt: 0x62 ((RDS)) / ike: 0x10 (Overwrite) / chars: 03 31 30 31 2E 33 04 20 20 20 20 20 20 ("☐101.3☐      ")
    rad	gt	RAD-A5*   	layout: 0x62 (Header) / padding: 0x01 (No Padding) / zone: 0x02 ((0000 0010) Zone: B/2) / chars: 20 20 20 20 20 ("     ")
    rad	gt	RAD-A5*   	layout: 0x62 (Header) / padding: 0x01 (No Padding) / zone: 00 ((0000 0000) Zone: 0) / chars:  ("")
    bmbt	gt	BMBT-NAV  	0x81 (1000 0001) :bmbt_right      Right: 1
    rad	gt	RAD-23    	gt: 0x62 ((RDS)) / ike: 0x10 (Overwrite) / chars: 03 31 30 31 2E 35 04 20 20 20 20 20 20 ("☐101.5☐      ")
    bmbt	gt	BMBT-NAV  	0x81 (1000 0001) :bmbt_right      Right: 1
    rad	gt	RAD-23    	gt: 0x62 ((RDS)) / ike: 0x10 (Overwrite) / chars: 03 31 30 31 2E 37 04 20 20 20 20 20 20 ("☐101.7☐      ")
    bmbt	gt	BMBT-NAV  	0x81 (1000 0001) :bmbt_right      Right: 1
    rad	gt	RAD-23    	gt: 0x62 ((RDS)) / ike: 0x10 (Overwrite) / chars: 03 31 30 31 2E 39 04 20 20 20 20 20 20 ("☐101.9☐      ")
    rad	gt	RAD-A5*   	layout: 0x62 (Header) / padding: 0x01 (No Padding) / zone: 0x02 ((0000 0010) Zone: B/2) / chars: 20 50 20 32 20 (" P 2 ")
    rad	gt	RAD-A5*   	layout: 0x62 (Header) / padding: 0x01 (No Padding) / zone: 00 ((0000 0000) Zone: 0) / chars:  ("")
    bmbt	gt	BMBT-GT*  	0x05 (0000 0101) :bmbt_confirm   	[Confirm]      	Press 
    bmbt	gt	BMBT-GT*  	0x85 (1000 0101) :bmbt_confirm   	[Confirm]      	Release
    rad	gt	RAD-ALT   	mode: 0x04 ((Select) "m" Manual Staion Choice) / opts:  ( 0 )
    rad	gt	RAD-A5*   	layout: 0x62 (Header) / padding: 0x01 (No Padding) / zone: 0x03 ((0000 0011) Zone: C/3) / chars: 20 20 20 20 20 ("     ")
    rad	gt	RAD-A5*   	layout: 0x62 (Header) / padding: 0x01 (No Padding) / zone: 00 ((0000 0000) Zone: 0) / chars:  ("")
    rad	gt	UI-RAD    	state: 0x04 ((0000 0100) Hide: Select)

#### Note
As long as Menu has not been pressed in the time since radio was off, thus not having radio send 0x46 0x01, when it is next turned on, it will be displayed.

Which interestinly, is enforced by the radio, which doesn't actually send any text when powered on. Presumably 0x46 0x01 is in radio state, and it won't draw until "overlay" is requested.
    
    
    
### Info
    
    bmbt glo_h   BMBT-SOFT       0x38 (0011 1000) :bmbt_soft_info     [Info]          Press 
    rad  gt      RAD-A5*         layout: 0x62 (Header) / padding: 0x01 (No Padding) / zone: 0x41 ((0100 0001) Block: [ON], Zone: A/1) / chars: 20 46 4D 41 20 (" FMA ")
    bmbt glo_h   BMBT-SOFT       0xb8 (1011 1000) :bmbt_soft_info    [Info]          Release
    rad  gt      RAD-A5*         layout: 0x62 (Header) / padding: 0x01 (No Padding) / zone: 0x42 ((0100 0010) Block: [ON], Zone: B/2) / chars: 20 50 20 32 20 (" P 2 ")
    rad  gt      RAD-A5*         layout: 0x62 (Header) / padding: 0x01 (No Padding) / zone: 0x43 ((0100 0011) Block: [ON], Zone: C/3) / chars: 20 20 20 20 20 ("     ")
    rad  gt      RAD-A5*         layout: 0x62 (Header) / padding: 0x01 (No Padding) / zone: 0x44 ((0100 0100) Block: [ON], Zone: D/4) / chars: 20 20 20 20 20 ("     ")
    rad  gt      RAD-A5*         layout: 0x62 (Header) / padding: 0x01 (No Padding) / zone: 0x45 ((0100 0101) Block: [ON], Zone: E/5) / chars: 20 20 52 44 53 20 20 ("  RDS  ")
    rad  gt      RAD-A5*         layout: 0x62 (Header) / padding: 0x01 (No Padding) / zone: 0x46 ((0100 0110) Block: [ON], Zone: H2/6) / chars: 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 ("                    ")
    rad  gt      RAD-A5*         layout: 0x62 (Header) / padding: 0x01 (No Padding) / zone: 0x07 ((0000 0111) Zone: H3/7) / chars: 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 ("                    ")
    rad  gt      RAD-23          gt: 0x62 ((RDS)) / ike: 0x10 (Overwrite) / chars: 03 31 30 31 2E   39 04 20 20 20 20 20 20 ("☐101.9☐      ")

    # Info Menu
    rad  gt      RAD-21*         layout: 0x60 ([Digital] Menu A) / m2: 00 ((0000 0000) Band (0x43): FMA, Preset (0x41), Dolby: (0x83): No Preset) / m3: 0x40 ((0100 0000) Block: [ON], index: "0") / chars: 50 54 59 20 20 20 20 20 20 20 20 20 20 2A 06 ("PTY          *☐")
    rad  gt      RAD-21*         layout: 0x60 ([Digital] Menu A) / m2: 00 ((0000 0000) Band (0x43): FMA, Preset (0x41), Dolby: (0x83): No Preset) / m3: 0x01 ((0000 0001) index: "1") / chars: 52 44 53 20 20 20 20 20 20 20 20 20 20 2A 06 06 06 06 06 06 06 06 06 ("RDS          *☐☐☐☐☐☐☐☐☐")
    rad  gt      RAD-A5*         layout: 0x60 (Menu A) / padding: 0x01 (No Padding) / zone: 00 ((0000 0000) Zone: 0) / chars:  ("")
    # Header
    rad  gt      RAD-A5*         layout: 0x62 (Header) / padding: 0x01 (No Padding) / zone: 0x41 ((0100 0001) Block: [ON], Zone: A/1) / chars: 20 46 4D 41 20 (" FMA ")
    rad  gt      RAD-A5*         layout: 0x62 (Header) / padding: 0x01 (No Padding) / zone: 0x42 ((0100 0010) Block: [ON], Zone: B/2) / chars: 20 50 20 32 20 (" P 2 ")
    rad  gt      RAD-A5*         layout: 0x62 (Header) / padding: 0x01 (No Padding) / zone: 0x43 ((0100 0011) Block: [ON], Zone: C/3) / chars: 20 20 20 20 20 ("     ")
    rad  gt      RAD-A5*         layout: 0x62 (Header) / padding: 0x01 (No Padding) / zone: 0x44 ((0100 0100) Block: [ON], Zone: D/4) / chars: 20 20 20 20 20 ("     ")
    rad  gt      RAD-A5*         layout: 0x62 (Header) / padding: 0x01 (No Padding) / zone: 0x45 ((0100 0101) Block: [ON], Zone: E/5) / chars: 20 20 52 44 53 20 20 ("  RDS  ")
    rad  gt      RAD-A5*         layout: 0x62 (Header) / padding: 0x01 (No Padding) / zone: 0x46 ((0100 0110) Block: [ON], Zone: H2/6) / chars: 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 ("                    ")
    rad  gt      RAD-A5*         layout: 0x62 (Header) / padding: 0x01 (No Padding) / zone: 0x07 ((0000 0111) Zone: H3/7) / chars: 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 ("                    ")
    rad  gt      RAD-23          gt: 0x62 ((RDS)) / ike: 0x10 (Overwrite) / chars: 03 31 30 31 2E 39 04 20 20 20 20 20 20 ("☐101.9☐      ")
    # Timeout, hide menu.
    rad  gt      UI-RAD          state: 0x0c ((0000 1100) Hide: Menu)


_Still no change..._

### Render Menu 21

    # Whoops.. I don't have block in generate...?
    # I'll try Menu now...
    # Radio overlay on, then off, radio off/on.. still no change...
    # Fix menu generate.. okay, fixed..
    # generate menu 0x60 (no header...)
    # hit menu.. nothing!
    # overlay on...
    # try again menu.. (also no header..)
    # select multiple presets...
    # still nothing...
    # trying menu 0x61
    # change preset
    # menu: same again
    # overlay back on
    # redraw.. change preset... 
    # try header...0xa5
    # hit menu..
    # nada.. 
    # full retard with wilhelm...
    # nothing...
    
## MK4 (No TV, Radio, or DSP emulation.)

### No Idea?

    gt   rad     UI-GT           config: 00 ((0000 0000) )
    rad  gt      UI-RAD          state: 0x01 ((0000 0001) Hide: --, Main Menu: [ON])


    gt      glo_l   PONG            status: 0x41 (Navi. GT (MK1/4) -> BF [Announce])
    ike     glo_l   IGN             position: 00 (Ignition: KL-30 (Pos. 0))
    ike     glo_l   IGN             position: 00 (Ignition: KL-30 (Pos. 0))
    ike     glo_l   IGN             position: 00 (Ignition: KL-30 (Pos. 0))
    rad     glo_h   PONG            status: 0x01 (Announce)
    ike     glo_l   IGN             position: 00 (Ignition: KL-30 (Pos. 0))
    ike     glo_l   IGN             position: 00 (Ignition: KL-30 (Pos. 0))
    ike     glo_l   IGN             position: 00 (Ignition: KL-30 (Pos. 0))
    ike     glo_l   IGN             position: 0x03 (Ignition: KL-15 (Pos. II))
    gt      glo_l   PONG            status: 0x40 (Navi. GT (MK1/4) -> BF [Reply])
    gt      rad     UI-GT           config: 0x11 ((0001 0001) Main Menu: [ON])

### KL-30

    ike glo_l   IGN             position: 00 (Ignition: KL-30 (Pos. 0))
    nav rad   PONG            status: 0x01 (Announce),
    gt  glo_l   PONG            status: 0x41 (Navi. GT (MK1/4) -> BF [Announce]),
    gt  ike   IGN-REQ   --,
    gt  ike   REGION-GT?--,
    gt  ike   CONF-BOOL       field: 0x01 ((Settings) Time) / control: 0x01 (Variable Request (0x24)),
    gt  ike   CONF-BOOL       field: 0x02 ((Settings) Date) / control: 0x01 (Variable Request (0x24)),
    ike glo_l   REGION          lang: 0x08 (Unknown?) / b2: 0x81 ((1000 0001) Time: (12h), Temp.: (C.), Date: (mm/dd)) / b3: 0x60 ((0110 0000) Distance: (km), Consump.: (l/100km)) / b4: 42 (b4: "42"),
    ike anzv    ANZV-VAR-IKE*   field: 0x01 ((Settings) Time) / ike: 00 (--) / chars: 2D 2D 3A 2D 2D 20 20 ("--:--  "),
    ike anzv    ANZV-VAR-IKE*   field: 0x02 ((Settings) Date) / ike: 00 (--) / chars: 2D 2D 2F 2D 2D 2F 32 30 31 39 ("--/--/2019"),
    nav glo_l   PONG            status: 0xc1 (7F -> BF (Guidance Active) [Announce]),
    ike glo_l   IGN             position: 00 (Ignition: KL-30 (Pos. 0)),


### KL-R
    
    # some messages removed for brevity...
    ike glo_l   IGN         position: 0x01 (Ignition: KL-R (Pos. I)),
    gt  glo_l   PONG      	status: 0x40 (Navi. GT (MK1/4) -> BF [Reply])
    gt  rad     SRC-SND   	00 00
    gt  cid     PING      	--
    gt  nav_jp  SRC-NAV_JP*	02 00
    gt  bmbt    RAD-LED   	led: 0x90 ((LED) Off (Reset))
    gt  rad     UI-GT     	config: 0x11 ((0001 0001) Main Menu: [ON])
    gt  dsp     DSP-SET   	mode: 0x28 (Demo Off) / adjustment: 00 ((0000 0000) Band: 80hz, ±: +, magnitude: "0")
    nav rad     TMC-REQ         1F 00,
    nav rad     TMC-REQ         3F 00,
    gt  ike     REGION-SET      lang: 0x01 (GB) / b2: 0x85 ((1000 0101) Time: (12h), Temp.: (C.), Date: (mm/dd)) / b3: 0x60 ((0110 0000) Distance: (km), Consump.: (l/100km)) / b4: 42 (b4: "42"),

### KL-30

    nav rad PONG      	status: 0x01 (Announce),
    gt  glo_l PONG      	status: 0x41 (Navi. GT (MK1/4) -> BF [Announce]),
    gt  ike IGN-REQ   --,
    gt  ike REGION-GT?--,
    gt  ike CONF-BOOL 	field: 0x01 ((Settings) Time) / control: 0x01 (Variable Request (0x24)),
    gt  ike CONF-BOOL 	field: 0x02 ((Settings) Date) / control: 0x01 (Variable Request (0x24)),
    nav glo_l PONG      	status: 0xc1 (Navi. Computer -> BF [Announce]),
    nav ses NAV-VOICE-AF	04,
    nav rad TMC-REQ   	10,
    nav rad TMC-REQ   	30
    
### KL-R

    nav rad  PONG      	status: 0x01 (Announce)
    gt  glo_l  PONG      	status: 0x41 (Navi. GT (MK1/4) -> BF [Announce])
    gt  ike  IGN-REQ   	--
    ike glo_l  IGN       	position: 0x01 (Ignition: KL-R (Pos. I))
    ike anzv   ANZV-BOOL-IKE	control_a: 00 ((0000 0000) (Settings) Memo: [OFF], (OBC) Timer: [OFF], (OBC) Limit: [OFF]) / control_b: 00 ((0000 0000) (Code) Lock: [OFF], (Aux.) Heating: [OFF], (Aux.) Timer 2: [OFF], (Aux.) Vent.: [OFF], (Aux.) Timer 1: [OFF])
    ike glo_l  IGN       	position: 0x01 (Ignition: KL-R (Pos. I))
    gt  ike  CONF-BOOL 	field: 0x09 ((OBC) Limit) / control: 0x02 (Boolean Request (0x2A))
    ike anzv   ANZV-BOOL-IKE	control_a: 00 ((0000 0000) (Settings) Memo: [OFF], (OBC) Timer: [OFF], (OBC) Limit: [OFF]) / control_b: 00 ((0000 0000) (Code) Lock: [OFF], (Aux.) Heating: [OFF], (Aux.) Timer 2: [OFF], (Aux.) Vent.: [OFF], (Aux.) Timer 1: [OFF])
    ike anzv   ANZV-VAR-IKE*	field: 0x09 ((OBC) Limit) / ike: 00 (--) / chars: 2D 2D 2D 20 4B 4D 2F 48 ("--- KM/H")
    gt  ike  REGION-GT?	--
    gt  ike  CONF-BOOL 	field: 0x0c ((Settings) Memo) / control: 0x02 (Boolean Request (0x2A))
    gt  ike  CONF-BOOL 	field: 0x07 ((OBC) Distance) / control: 0x01 (Variable Request (0x24))
    gt  lcm  LAMP-REQ  	--
    gt  ike  CONF-BOOL 	field: 0x01 ((Settings) Time) / control: 0x01 (Variable Request (0x24))
    lcm glo_l  LAMP      	l1: 00 ((0000 0000) ) / l2: 00 ((0000 0000) ) / l3: 00 ((0000 0000) ) / l4: 00 ((0000 0000) )
    ike glo_l  REGION    	lang: 0x08 (Unknown?) / b2: 0x81 ((1000 0001) Time: (12h), Temp.: (C.), Date: (mm/dd)) / b3: 0x60 ((0110 0000) Distance: (km), Consump.: (l/100km)) / b4: 42 (b4: "42")
    gt  ike  CONF-BOOL 	field: 0x02 ((Settings) Date) / control: 0x01 (Variable Request (0x24))
    ike anzv   ANZV-BOOL-IKE	control_a: 00 ((0000 0000) (Settings) Memo: [OFF], (OBC) Timer: [OFF], (OBC) Limit: [OFF]) / control_b: 00 ((0000 0000) (Code) Lock: [OFF], (Aux.) Heating: [OFF], (Aux.) Timer 2: [OFF], (Aux.) Vent.: [OFF], (Aux.) Timer 1: [OFF])
    ike anzv   ANZV-VAR-IKE*	field: 0x07 ((OBC) Distance) / ike: 00 (--) / chars: 20 20 20 30 20 4B 4D 20 ("   0 KM ")
    ike anzv   ANZV-VAR-IKE*	field: 0x01 ((Settings) Time) / ike: 00 (--) / chars: 2D 2D 3A 2D 2D 20 20 ("--:--  ")
    ike anzv   ANZV-VAR-IKE*	field: 0x02 ((Settings) Date) / ike: 00 (--) / chars: 2D 2D 2F 2D 2D 2F 32 30 31 39 ("--/--/2019")
    gt  rad  SRC-SND   	00 00
    gt  cid  PING      	--
    gt  nav_jp   SRC-NAV_JP*	02 00
    gt  bmbt   RAD-LED   	led: 0x90 ((LED) Off (Reset))
    gt  rad  UI-GT     	config: 0x11 ((0001 0001) Main Menu: [ON])
    gt  dsp  DSP-SET   	mode: 0x28 (Demo Off) / adjustment: 00 ((0000 0000) Band: 80hz, ±: +, magnitude: "0")
    gt  ike  REGION-SET	lang: 0x01 (GB) / b2: 0x05 ((0000 0101) Time: (24h), Temp.: (C.), Date: (mm/dd)) / b3: 0x60 ((0110 0000) Distance: (km), Consump.: (l/100km)) / b4: 00 (b4: "00")
    gt  ike  REGION-SET	lang: 0x01 (GB) / b2: 0x05 ((0000 0101) Time: (24h), Temp.: (C.), Date: (mm/dd)) / b3: 0x60 ((0110 0000) Distance: (km), Consump.: (l/100km)) / b4: 00 (b4: "00")
    bmbt  rad  TAPE      	control: 0x05 (No Tape!)
    ike glo_l  REGION    	lang: 0x01 (GB) / b2: 0x05 ((0000 0101) Time: (24h), Temp.: (C.), Date: (mm/dd)) / b3: 0x60 ((0110 0000) Distance: (km), Consump.: (l/100km)) / b4: 42 (b4: "42")
    ike glo_l  REGION    	lang: 0x01 (GB) / b2: 0x05 ((0000 0101) Time: (24h), Temp.: (C.), Date: (mm/dd)) / b3: 0x60 ((0110 0000) Distance: (km), Consump.: (l/100km)) / b4: 42 (b4: "42")
    gt  ike  REGION-SET	lang: 0x01 (GB) / b2: 0x85 ((1000 0101) Time: (12h), Temp.: (C.), Date: (mm/dd)) / b3: 0x60 ((0110 0000) Distance: (km), Consump.: (l/100km)) / b4: 42 (b4: "42")
    gt  ike  REGION-SET	lang: 0x01 (GB) / b2: 0x85 ((1000 0101) Time: (12h), Temp.: (C.), Date: (mm/dd)) / b3: 0x60 ((0110 0000) Distance: (km), Consump.: (l/100km)) / b4: 42 (b4: "42")
    gt  ike  CONF-VAR  	field: 0x07 ((OBC/Nav.) Distance) / input: 00 00 ( 0 )
    ike glo_l  REGION    	lang: 0x01 (GB) / b2: 0x85 ((1000 0101) Time: (12h), Temp.: (C.), Date: (mm/dd)) / b3: 0x60 ((0110 0000) Distance: (km), Consump.: (l/100km)) / b4: 42 (b4: "42")
    ike glo_l  REGION    	lang: 0x01 (GB) / b2: 0x85 ((1000 0101) Time: (12h), Temp.: (C.), Date: (mm/dd)) / b3: 0x60 ((0110 0000) Distance: (km), Consump.: (l/100km)) / b4: 42 (b4: "42")
    ike anzv   ANZV-VAR-IKE*	field: 0x07 ((OBC) Distance) / ike: 00 (--) / chars: 20 20 20 30 20 4B 4D 20 ("   0 KM ")
    ike anzv   ANZV-VAR-IKE*	field: 0x08 ((OBC) Arrival) / ike: 00 (--) / chars: 2D 2D 3A 2D 2D 20 20 ("--:--  ")

##### note: 

#### Menu

df


-------


## Lifecycle

Radio exits overlay mode:

    rad	 gt 46 (0000_0010) Hide Panel [ON]
    rad	 gt 46 (0000_1100) Hide Menu [ON]

The radio will still write titles:

    rad gt 23 62 10 "☐ 89.3☐      "

but clear them after 8 second timeout:

    rad gt 46 02 (0000 0010) Hide Panel [ON]
    rad gt 46 0c (0000 1100) Hide Menu [ON]

A MENU press does not get sent to radio, but is broadcast, and instead handled by the GT, which will in turn, message the Radio relinquish (as presumably the radio does not listen for global button )

    gt  rad 45 91 (1001 0001) Info? [ON] Main Menu [ON]
    rad gt  46 01 (0000 0001) Main Menu [ON]


## C2x vs. BM5x

widescreen BMBT uses a different select... 
possibly due non-backwards compatible SELECT UI states
but not tone interestingly... 

## Tone/Select `0x37`
## GT UI `0x45`
## Radio UI `0x46`