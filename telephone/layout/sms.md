# SMS

![Telephone SMS Option](dial/IMG_2774.JPG)

When I installed the MK4, the Telephone menu had a new option **SMS** which sparked my interest.

SMS readily pops up in TIS in reference to ULF, Everest etc, but there was no clues as to usage.

As for the web, there was unusually little mentioned of it (with respect to I/K-Bus vehicles). There was anecdotal suggestions that it was not available in NA (CDMA/GSM compatibility perhaps?), but the introduction being relatively late in the lifecycle of E38/E39/E46 might also come into play.

Nonetheless, I did find one [useful thread from 2004](https://www.bimmerfest.com/forums/showthread.php?t=69485), and dug up the thread attachments from Google cached results and found the following:

![SMS Example 1](sms/2004_1_main_menu.jpeg)
![SMS Example 2](sms/2004_2_phone_menu.jpeg)
![SMS Example 3](sms/2004_3_sms_selection.jpeg)
![SMS Example 4](sms/2004_4_message.jpeg)

**Hurrah!**

The implementation does feel like a bit of an afterthought considering most functionality via the BMBT has custom layouts (DSP, Aux. Heat/Vent, OBC, Settings etc), but given MOST was already in production vehicles, and the 68k, OS-9 based VDO/Dayton platform was already long in the tooth, I'm not entirely surprised.

The **SMS index** layout is seemingly a repurposed **Directory/Top 8**, which I say because the top right cell (where the phone icon usually is) is addressed with an out of order index.

_'Fake' Directory_
![Fake Directory](sms/directory_fake.JPG)
_'Real' Directory_
![Real Directory](sms/directory_real.JPG)


The **SMS view** layout appears to just a repurposed **SOS/Emergency** layout.


![Example SMS](sms/message/reference_sms_message.jpeg)
![Example SOS](sms/sms_emergency.jpg)


The functionality itself isn't particularly useful- particularly without a factory phone. However the layouts introduce more options for custom UIs.
