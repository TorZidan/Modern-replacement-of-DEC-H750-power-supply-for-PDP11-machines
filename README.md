# Modern replacement of DEC H750 power supply for PDP11 computers

This project is about building a modern power supply for my PDP11/05 vintage computer.
You can see a video of a similar computer at https://youtu.be/JA9q6E1sv1I?si=HaifS1z651YgPFed .

## Overview:
The original power supply (PSU) is model number H750, made by DEC (Digital Equipment Corporation).
It is a metal tray with a bulky transformer, PSU board (also known as "DC regulator board model 5409728") and a fan.

We will disconnect and remove and save away the original PSU board; we will disconnect the original transformer, but leave it inside the computer (just because there is enough space for it to stay there).

We will build the new power supply from off-the-shelf components and connect it in place of the old PSU board using the same kind of connectors as the original ones.

The new power supply consists of 2 independent power supplies (one for +5V and one for -15V), and a Dc-to-Dc step-up board that generates +15V from the +5V.

No modifications to the existing wiring will be done, meaning that we can restore the computer to its original condition, if wanted.

We will keep the original fan unmodified and use it for cooling down the new PSU; however, I recommend replacing it with a modern low-noise fan.

## Why this project?
After paying $200 to replace the four largest electrolytic capacitors on the original PSU board (they are enormously big and hence expensive), I have a second thought about keeping the original PSU operational. The new PSU costs $70 total, and should provide years of reliable use.

## New wiring diagram:
![New PSU Wiring Diagram](./photos/H750ReplacementPowerSupplyWiringDiagram.png)

## Power requirements of the PDP computer:
See them [Here](./DEC_H740_PSU_Documentation.pdf#page=5), Pages 9 and 10. They are:

- +5V at 15A max, to ICs.
- +15V at 1A max, to I/O (communication) circuits.
- -15V at 7A max, to core memory.
- Note: the two fans run at 120V AC; they are not powered by the power supply.

The new PSU can provide more than the power required above.
In reality, I found out that my PDP11/05 uses much less that (note: it draws the same amount of power when executing a program and when "halted"):

- +5V: 11A
- +15V: 0.06A
- -15V: 0.2A


## Parts list for the new PSU

- For the +5V: "LRS-150F-5" (Switching Power Supply 110W 5V 22A max), from https://www.digikey.com/short/mnfv3f7d , $28
- For the +15V: we will produce it from the 5V PSU above using a "DFR0123" (DC-to-DC step-up transformer board), from https://www.digikey.com/short/pft4r07v , $8
- We will need 2 to 4 "raisers" (1/4 to 1/2 inch high) to safely mount the board above onto the metal plate (below), so that it does not touch the metal. You can improvise, using e.g. short pieces of plastic straw with a bolt in each; I used two metal raisers from an old motherboard.
- For the -15V: "LRS-150F-15" (Switching Power Supply 110W 15V 10A max), from https://www.digikey.com/short/8nvp5fb9 , $25
- For the 120V AC connector: 1-480276-0 (MATE-N-LOK, 6-pins in 2rows-by-3columns) from https://www.digikey.com/short/ffhqw77z, $1, specs are at https://www.te.com/usa-en/product-1-480276-0.datasheet.pdf
- 3 male pins for the connector above (only 3 out of the 6 pins are used): 60620-1 (CONN PIN 14-20AWG CRIMP TIN) from https://www.digikey.com/short/hqh9ct32, $1 total
- For the DC output connector: 1-480274-0 (MATE-N-LOK, 6-pins in 3rows-by-3columns) from https://www.digikey.com/short/cq30t74r, $1
- 7 female pins for the connector above (only 7 out of the 9 pins are used): 60619-1 (CONN SOCKET 14-20AWG CRIMP TIN) from https://www.digikey.com/short/59ppt31r, $2 total
- a few feet of 18 AWG stranded wire similar to the one used in modern computer PSUs (or go with a thicker 16 AWG if you want), ideally in 8 different colors, to reduce wiring mistakes.
- something to hold these things together. I used a 3inch x 7 inch metal plate HTP37 from Home Depot, $3
- TOTAL COST: about $70 plus tax plus shipping.

Tools:
- you will need a crimping tool for 18 AWG wire; I used a "PA-09", bit it was a bit too-small for the job (it is rated for 20-to-32-awg); so I can't recommend a specific crimper.
- you will need some skills to crimp wires. It's fun, in small quantities such as this.
- you will need to drill holes into the metal plate (if you choose to assemble things the way I did).
- screwdrivers, wire stripper, patience.
  
## Assembly:

Note: in many places in this document I talk about "120V" AC power, but in fact the two PSUs used for this project can work at 240V too (the European power grid), without any modifications.

WARNING: you are working with 120V high voltages (or even higher 240V in Europe)!!! Do this at your own risk. I am not liable for any injuries or monetary loss. Even when power is disconnected, a PSU may hold some power in its capacitors, which may shock you if you handle it improperly.

Follow the assembly diagram above. For an experienced electronics enthusiast the diagram  and the photos should be sufficient to assemble the PSU. So the instructions below are somewhat self-explanatory.

Note that the "ground" (the negative terminal) of the 5V PSU is connected to the "+15V" on the 15V PSU (not ground to ground!). This way the 15V PSU provides the "-15V". This is totally acceptable because both PSUs outputs are "isolated", "floating", "not connected to earth's ground".

Assemble the two power supplies and the DC-to-DC step-up transformer board together, on the metal plate. I placed the 5V PSU on top (above) the 15V PSU, and left about 1 inch between them, so that air can flow easily.

Crimp 3 wires (white, black and green) to the 3 male pins, and plug them at the proper places in the 6-pin connector. Connect the other end of these wires to the "L" (Load), "N" (Neutral) and Ground terminals on the top PSU, and from there run wires to the bottom PSU; this way, both PSUs will be powered. Cover the "L" (Load) terminal on each PSU with electric tape, to prevent human electrocution.

Crimp 7 different-colored wires to the 7 female pins, and plug them in the 9-pin connector. Connect the other ends according to the diagram.

Complete all other wirings according to the diagram.

Verify your work by comparing it with the wiring diagram and the provided photos. Pull on each wire and ensure that it is secured well.

Unplug the PDP computer power cable from the outlet. 
Disconnect the original regulator board (connectors J2, J3, J9). The capacitors on the board may still hold power which may shock you if you handle the board improperly! Leave the original bulky transformer disconnected (or remove it if wanted, to reduce the weight of the computer).

Make a jumper wire from e.g. 2-inch-long piece of 12-gauge insulated solid copper wire, and plug it into the 2-wire J3 connector (with 2 black cables on it); it is used by the PDP to detect if the PSU has overheated; inserting a jumper wire tells it that the PSU is not overheated. Put some tape to hold the jumper wire in place (to not fall).

Place the new PSU assembly into the PDP, where the old PSU board was. Find a way to secure it there, if needed. Mine is just laying there, unsecured, and I am ok with that.

Plug the 6-pin connector (120V AC power supply to the PSU) into the PDP. Do not plug the 9-pin connector just yet.

Plug the PDP computer power cable in the outlet and turn on the key in front of the computer to horizontal position (power on). The two fans on the PDP should start spinning (they are powered by 120V AC), but the PDP will remain off (because the 9-pin connector is not plugged yet).
Adjust the voltage on the DC-to-DC step-up transformer to 15.0V by rotating the potentiometer on in with a small flat-head screwdriver.
Measure the voltages at the 9-pin (DC out) connector and make sure they are the same as on the diagram. If not, 

Turn off the PDP from the key on the front panel, disconnect the PDP computer power cable, plug the 9-pin (DC out) connector into the PDP,
then restore power and turn on the power key again to horizontal position (power on). The PDP should run.
Measure the voltages on the back of the backplane; on mine, I have labeled the wires (using white paper tape) that provide power to the backplane with labels
"5V", "15V", "-15V", "Ground"; this simplifies this check. This is it! We did it. Yaaaay.

Note: No cats were harmed while building and testing this project!

## Further improvements:
 - The "BUS DC LO L" and "BUS AC LO L" power fail early warning signals are supposed to go "high" (to +5V) few milliseconds after the power is turned on (see Page 11 at ...). 
   We connected them directly to the +5V PSU output, meaning that they go high as soon as the power is on.
   It seems that things work ok, but we may want to introduce a delay circuit for these two signals.
 - The "LTCL output" 50Hz signal is not being generated by the new PSU. I just capped the brown wire on Pin 4 on the J2 DC Out connector (the blue plastic cap on the pictures).
   This is some kind of a square-wave 5V TTL clock signal that is used to track date and time when the machine is running.
   My PDP is able to execute programs from PDP11GUI just fine; a further investigation is needed to find out where this signal is needed.
   It canvbe produced in various ways, e.g. with a NE555 timer, or with single-board signal generators from AliExpress.

# Photos
There are many photos in the [Photos folder](./photos/)
Here are some of them:

![](./photos/OriginalPsuBoardWithLabels.jpg)
![](./photos/TheNewPsuIsConnectedAndIsOutsideOfTheEnclosureWithLabels.jpg)
![](./photos/TheNewPsuAssemblyWithLabels.jpg)
![](./photos/TheDcToDcBoardIsAdjustedToProduce15V.jpg)
![](./photos/ACrimpedWire.jpg)
![](./photos/6Pin120vAcInConnectorWithLabels.jpg)
![](./photos/9PinDcOutConnectorWithLabels.jpg)
![](./photos/The5vRailDraws11Amps.jpg)
![](./photos/WeAreRunningFullSpeedWithTheNewPsu.jpg)


