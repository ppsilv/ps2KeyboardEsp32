# ps2KeyboardEsp32
This repo has code to read and process scancode from a ps2 keyboard.  

The code was tested with arduino Esp32 dev module(ESP-WROOM-32) and it worked fine.

This code do a scancode translate to ASCII, and caps lock and shift work fine producing lower case and capital letters.

The led for caps lock, num lock and scroll lock work fine.

This text is from https://github.com/michalhol/ps2kbdlib) and some others fragment of code.

* http://retired.beyondlogic.org/keyboard/keybrd.htm (source I was using)
* When you receive 0xE0, it means, the key pressed/or released is extended code key.
* It is followed with second byte of the key scancode (eg. you receive E0 5A (numpad enter pressed)) or
* 0xF0 in case the extended key has been released (eg. E0 F0 5A (numpad enter released)).
* Otherwise when you receive 0xF0, it means, the next byte will be key code of key, which was released (eg. F0 29 (released space)).
* Then there is another "special" scancode -
* E1 14 77 E1 F0 14 F0 77 - that is Pause/Break key - 8 Bytes long scancode!
* And maybe (on my keyboard it is not so) there yould be another code for Print screen key -
* E0 12 E0 7C (and probably something similar for release but that's something you will have to find out yourself).
* Anything else is a scancode of "normal" key (eg. 1C (pressed 'a')).

* And be aware of buffer overflow - when it does, all codes you haven't read yet will be lost
* Current size of the buffer is 256 keys.
* If you do want to change it's size, open PS2Kbd.h (it is located in the <path-to-library>/PS2Kbd/src/)
*and on line 39 replace 256 with whatever you want (it just has to be bigger number than 0).
