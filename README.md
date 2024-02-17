# Vertux-Combat-Hacking
Hacking the Vertux Combat Quickstrike gaming keypad. 

<img src="https://github.com/chopsuwe/Vertux-Combat-Hacking/assets/55773924/f7e1c6c0-aea9-4aef-91bb-4f75a5107d20" alt="VertuxC promo pic" width=75%/>

The Vertux Combat QuickStrike is a one handed gaming keypad with a thumb joystick similar to the classic Razer Tartarus. The body has the the same layout as a standard keyboard with the addition of a joystick under the thumb.

It is a very well built product with one major problem - the joystick is mapped to the WSAD keys, the same keys that are replicated on the keyboard section. There is no way to change any of the key assignments, which makes the product largely pointless. 

There is very little information about this product on the internet so, as I was given one, I figured I would try to hack it. Spoiler alert: there is no happy ending, reprogramming it will require someone with better hacking skills than me.

## Who made it?

The Vertux Combat is also sold under the brands of NEXiLUX and IINE. According to [this reddit comment](https://www.reddit.com/r/NintendoSwitch/comments/o4k474/i_tried_one_of_those_20_aliexpress_pro/h2iuhsj/), IINE sells third party game controllers into Southeast Asia, with a few products appearing on Amazon, eBay and Walmart under the NEXiLUX brand. However it appears this one actually made by NEXiLUX.

## Software and updates

There is no software or drivers available under any of the brand names. Several web sites say "no driver required" and that it is designed for Xbox One, 360, PS 4, 3, Switch, lite, PC. It is possible the macro keys could be mapped as a game controller in Windows but I have not tired this and there is no way to remap the joystick.

The NEXiLUX website does have the gamepad listed under the name PRO GAMING KEYBOARD AND RGB MOUSE COMBO NS/X1/PS4/PC with a [link to a firmware update](https://img1.wsimg.com/blobby/go/2caddf61-9f88-40c8-825e-452ee5a1972b/downloads/NEXILUX%20KEYBOARD%20MOUSE%20COMBO%20FIRMWARE%20UPDATE%202.zip?ver=1704647026111) on the [download page](https://nexilux.com/drivers). That page gives no detail as to what the update does, however the file dates match a news page from January 2024 which states "Pro Gaming Keyboard update adds Xbox Series X|S Compatibility. Added Firmware update for Pro Gaming Keyboard which makes it compatible with XBOX Series X|S. It will require a Windows PC."

The update package includes an executable updater (Windows only) and a binary file. In theory it would be possible for someone with sufficient skills to write and compile new firmware. Unfortunately I haven't been able to find any information on the microprocessor used and probably don't have the skills anyway. 

It's a real shame as this is such a well made product that would make a great alternative to the Tartarus. If anyone is interested on taking on the challenge I'd love to hear from you.

## Features

<img src="https://github.com/chopsuwe/Vertux-Combat-Hacking/assets/55773924/51211985-d152-4574-87b0-81eab82b5246" alt="VertuxC top" width=75%/>

The main section is the left side of a standard keyboard. There is no branding on the keys, they are mechanical, very clicky tactile. And as a bonus they are optical keys so will never suffer from switch bounce. On the left are macro keys G1-4 and the ???? key on the right, all of which are membrane. The joystick is analogue but is mapped to produce WSAD when pressed. It also has a push which does ????

On the back right are connectors for the USB-C output (to the PC/console), three USB2.0 inputs and one stereo headphones jack (3.5mm).

The wrist rest is nicely padded and adjustable.

<img src="https://github.com/chopsuwe/Vertux-Combat-Hacking/assets/55773924/6834ea05-5142-41c4-acea-3afb7c05a3e7" alt="VertuxC bottom" width=75%/>

## Disassembly & Reverse Engineering

<img src="https://github.com/chopsuwe/Vertux-Combat-Hacking/assets/55773924/8285fb76-a785-4f32-9d16-c035415fe47d" alt="VertuxC buttons removed" width=75%/>

Remove the keycaps and undo all the screws. The top panel lifts off.

<img src="https://github.com/chopsuwe/Vertux-Combat-Hacking/assets/55773924/4e5bcf0d-9f17-4398-a22b-1aaa36d34bca" alt="VertuxC button plate" width=75%/>

The top panel is made to a very high standard. It is a hefty sheet of metal, precisely machined, powder coated and silk screened.

<img src="https://github.com/chopsuwe/Vertux-Combat-Hacking/assets/55773924/75ddd1e6-e05e-4463-867f-40f717281e12" alt="PCB assembled" width=75%/>

Remove all the screws and lift out the main circuit board. Remove the smaller boards by flicking up the black tabs on the connectors, pulling out the ribbon cable and undoing the screws.

Construction is very robust with plenty of mechanical support for the electronics.

<img src="https://github.com/chopsuwe/Vertux-Combat-Hacking/assets/55773924/3607f238-363b-48a0-97f6-47116b089d19" alt="VertuxC usb board" width=75%/>

Connector board. Top left is the USB-C for connecting to the host PC or console. Bottom right is the headphone jack. The others are USB2.0 for connecting a mouse, etc.

The DN35 chip is likely to be the DAC and headphones driver IC.

<img src="https://github.com/chopsuwe/Vertux-Combat-Hacking/assets/55773924/007b0e4f-fbfb-4e2c-a7a1-677d07751473" alt="VertuxC main pcb top" width=75%/>

Top of the main board.

Each key has a RGB led at the top and an infrared TX/RX pair to detect the key press. Top left is the Caps Lock LED. Top right are the backlight LEDs for the Vertux logo (LED1-3). Next to those are status lights for the USB2.0 ports, mouse (LED4), gamepad (LED5) and headset (LED6).

<img src="https://github.com/chopsuwe/Vertux-Combat-Hacking/assets/55773924/b06d5b16-9fa7-4563-9aea-cae53bf9acdc" alt="VertuxC pcb bottom" width=75%/>

Bottom of the main board.

U1 (far right). VS12L03A I2C/SPI LED matrix driver. Can drive up to 256 LEDs. It also has an analogue input so could potentially produce a music controlled light show. 

U2 (bottom left). Has no markings. Possibly some sort of USB buffer, it connects to the u4's DMU/DPU pins (D- & D+ of the upstream facing port). 

U3 (on connector board). DN335. Probably a headphone driver DAC. 

U4 (top left). the FE1.1S USB 2.0 High Speed 4-Port Hub Controller made by Terminus. This controls the status LEDs (LED4-6).

U5 (bottom left). 4A2D linear voltage regulator (2.0-6.0V)

U6 (bottom left). FM25Q04 is a 4M-bit (512k byte) serial flash memory chip.

U7 (bottom middle). Unknown. Marked with DN2503 ET64 949 J129BG.

U8 (far right). 4A2D linear voltage regulator (2.0-6.0V)

