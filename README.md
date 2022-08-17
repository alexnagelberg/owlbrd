
# OwlBrd
This board was made to supersede EasyBrd but it has a lot more to it so for cost or complexity, you can pick and choose what you want. The only section needed to drive 8 spools is the core section, ideally with distance sensors as well. Most of these parts can be found [in the US] on Amazon/Digikey and should be widely available and low cost and swappable with different manufacturers, the one exception being the optional TCA9548A breakout which only works with Adafruit's (maybe in future I'll add another row of pins to allow the hiletgo variants, but some workarounds can be done).

All the boards can be soldered either directly down or put down a set of headers so the boards can be removed/replaced. I would maybe take care with the TMC drivers as there's a resistor under each, but you could also solder the resistors on the bottom side if there's concerns of heat/proximity without a header -- probably shouldn't be an issue at all.

## BOM (split by functionality)

### Misc (listed again throughout sections)
 - Dupont male/female headers ([Amazon Affiliate](https://amzn.to/3ps0VLI))
 - Resistors - 1k, 10k, 2.37k, 4.7k used throughout (kit: [Amazon affiliate](https://amzn.to/3c7XxCF))
 - Ceramic capacitors: 0.33uF, 0.1uF used in ERCF/heater (kit: [Amazon affiliate](https://amzn.to/3wbLxqx))
 - Electrolytic capacitors: 100uF 25v used in ERCF/rewinder (kit: [Amazon affiliate](https://amzn.to/3Qs2sNM))
 - JST-XH connectors: 2-pin, 3-pin, 4-pin (kit: [Amazon affiliate](https://amzn.to/3AnAbBp))
 - Screw terminals for power/heater ([Amazon affiliate](https://amzn.to/3T8kE0O))

### Core (Rewind Stepper + Clutches)
- Raspberry Pi Pico ([[Digikey](https://www.digikey.com/en/products/detail/raspberry-pi/SC0915/13624793)] headers are optional)
- BTT TMC2209 x1 ([[Amazon affiliate](https://amzn.to/3prqGvD)] headers encouraged, note that UART is currently wired to the 4th pin and some like FYSETC use the 5th pin. You might be able to resolve this with a jumper on the pins on top?)
- 74HC238 DIP ([Amazon affiliate](https://amzn.to/3PAAPkm)) for clutch (addresses 8 pins using 3 GPIO)
- ULN2803A DIP ([Amazon affiliate](https://amzn.to/3QPcatl)) for clutch (drives 8 clutches using one IC)
- Screw terminal for power
- Resistors: 10k (x1), 1k (x1)
- JST-XH 2 pin female (x8) for clutches
- JST-XH 4 pin female (x2) for rewinder steppers
- Electrolytic capacitor: 100uF 25v

### Distance Sensors
- Adafruit TCA9548A ([Amazon affiliate](https://amzn.to/3wdmtQd) or [adafruit](https://www.adafruit.com/product/2717)) breakout (headers optional, cheaper generics available but one side is slightly wider by like 2.5mm -- might be able to rig something to fit it or could use wires)
- JST-XH 4 pin female (x8) for each sensor

### ERCF
- BTT TMC2209 x2 ([[Amazon affiliate](https://amzn.to/3prqGvD)] headers encouraged, note that UART is currently wired to the 4th pin and some like FYSETC use the 5th pin. You might be able to resolve this with a jumper on the pins on top?)
- L7805CV ([Amazon affiliate](https://amzn.to/3zYoTTM)) 5v linear regulator (probably plenty of substitutions for this but should be readily available -- any 5v regulator with same pinout should work) for supplying 5v power on board
- Resistors: 10k (x2)
- Ceramic capacitors: 0.33uF x1, 0.1uF x1
- Electrolytic capacitors: 100uF 25v (x2)
- JST-XH 3 pin female (x4) for servo, encoder, endstop, and optional neopixel/misc
- JST-XH 4 pin female (x2) for selector/gear steppers

### Heater
- IRLB8721PBF ([Amazon affiliate](https://amzn.to/3A3fAC1)) MOSFET (probably lots of substitutable options but should be readily available)
- BAV99 SMD ([[Amazon affiliate](https://amzn.to/3Pub5Gj)] only surface mount component -- shouldn't be too difficult to solder or need anything special, needed for thermistor)
- Screw terminal (or connector of your choice) for heater
- Resistors: 2.37k (x2), 4.7k (x1)
- Ceramic capacitor: 0.1uF
- JST-XH 2 pin female (for thermistor)

### UART
There's a breakout for UART with power for pi. If you use UART, and don't connect pico to USB, you'll want to put a header and jumper on J29 Ext Power so that it powers the pico from the 5v regulator. Install the 0.33uF and 0.1uF capacitors and L7805CV from ERCF section to get 5v power if needed.
