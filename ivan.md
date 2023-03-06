Ivan, please excuse the programmatic formatting.

## `0x4e`

I haven't confirmed this as my BlueBus-esq solution didn't have a radio! Ted will probably know more about this command.

    0x4E: # SRC-SND
      :properties:
        :short_name: SRC-SND
        :long_name: Source volume...?
      :klass: Base
      :meta:
        - 3B 05 68 4E 00 00 18 (TV off/voice command end)
        - 3B 05 68 4E 01 00 18 (TV on) MUTE?
        - 3B 05 68 4E XX 3F 4B (Voice command/set navi. volume)
        - telephone mute is switched input (not bus command)

### `0x4e` Frames

    # Adjusting nav voice volume via 'Set'
    # These values seem to change a little bit so there might a bitfield mixed in?
    
    3B 05 68 4E 04 3F 23
    3B 05 68 4E 1C 3F 3B
    3B 05 68 4E 2C 3F 0B
    3B 05 68 4E 3C 3F 1B
    3B 05 68 4E 5C 3F 7B
    3B 05 68 4E 6C 3F 4B
    3B 05 68 4E 7C 3F 5B
    3B 05 68 4E 9C 3F BB
    3B 05 68 4E AC 3F 8B
    3B 05 68 4E BC 3F 9B
    3B 05 68 4E DC 3F FB
    3B 05 68 4E EC 3F CB
    3B 05 68 4E FC 3F DB

    # The current volume would be sent multiple times during a journey,
    # so I think it's just setting the nav voice volume each time the nav 'speaks'
    
    3B 05 68 4E 6C 3F 4B

## `0xaa` & `0xab`

You mentioned `0xaa` which I've only seen in the context of the rear compartment monitor (RCM).

This is based on my limited blackbox testing of what I believed were the rear compartment monitor (RCM) commands.

I'm pretty sure device `0x43` is the rear GT.

### `0xaa`

    0xAA: # GT2-NAV-AA
      :properties:
        :short_name: GT2-NAV-AA
        :long_name: Request NAV GT switch to navigation for routing to RCM
      :klass: Base
      :meta:
        - control from rear GT (E38 3 socket TV module)
        - seemingly limited to switching navi. GT to GPS Navigation
        - rear monitor controls then likely routed directly to navi. GT

#### `0xaa` Frames

No frames as I don't have rear GT! :P

### `0xab`

    0xAB: # NAV-GT2-AB
      :properties:
        :short_name: NAV-GT2-AB
        :long_name: NAV GT UI state?
      :klass: Base
      :meta:
        - 0x01: nav (only ever received upon using 0xAA)
        - 0x20: seems to immediately preceed 0x21 (only if 0xAA is sent)
        - 0x21: main menu (what i've received until now)
        - 0x11: resume guidance/directions (rare!)

#### `0xab` Frames

    7F 04 43 AB 01 92
    7F 04 43 AB 11 82
    7F 04 43 AB 20 B3
    7F 04 43 AB 21 B2
 
## `0xaf`
    
    0xAF: # NAV-VOICE-AF
      :properties:
        :short_name: NAV-VOICE-AF
        :long_name: Query if voice recognition present?
      :klass: Base
      :meta:
        - 7F 04 B0 AF 04 60

### `0xaf` Frames

    # I get this regularly.. so.. a presence query maybe?
    
    ./2019-02-19.log:7F 04 B0 AF 04 60
    ./2019-02-20.log:7F 04 B0 AF 04 60
    ./2019-02-21.log:7F 04 B0 AF 04 60
    ./2019-02-22.log:7F 04 B0 AF 04 60
    ./2019-02-23.log:7F 04 B0 AF 04 60
    ./2019-02-24.log:7F 04 B0 AF 04 60
    ./2019-02-26.log:7F 04 B0 AF 04 60
    ./2019-02-27.log:7F 04 B0 AF 04 60