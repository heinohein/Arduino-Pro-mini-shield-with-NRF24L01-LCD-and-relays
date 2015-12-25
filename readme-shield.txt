This document describes a "shield" for a Arduino Pro mini, also supporting a NRF24L01(+),
a LCD and single or double  relay brick.

Of this shield 2 versions exist, one with the NRF24L01 in parallel with the LCD called 
"straight" and one with NRF24L01 pointing away from the LCD called "down".

I use this "shield" with several Arduino project, also to befound on Github. Those projects
contain sketch files and a reference to the PCB and documents here. 

In the map Fritzing-schem-and-PCB the files Pro mini nrf24 lcd relais V1.11 straight and
down can be found. The program Fritzing was used to draw these PCB's and the files are
available for your modifications. Please note that only PCB tabs of theze files are 
usefull, the other tabs are a mess.
Also the Fritzing file Arduino Pro mini shield pinciple schem and its JPG can be found. 
It helps to understand the relation between the components discussed below without the need
to follow wires on the PCB.
The PCB was designed so that one or two sided perf board wich copper rings can be used to 
create a PCB. All wires on the top layer are just wires to make cross connections. 
In the design I only use standard, classicle, non SMS components only.
The PDF output of Fritzing was used to create a single sided PCB for DIY etching. 
I use 70x100 mm one sided copper clay layer PCB to create 2 PCB of 50*70 at the same time.
Of course Fritzing can be used to generate Gerber files.
Together with the files you find 2 JPG, showing you quickly what the top and bottom layer 
combined looks like. The brighter yellow is the top layer, the darker yellow the bottom 
layer.
Regarding DIY etching, my laserprinter doen not produce intensif enough black lines. 
A local camerashop prints my document on "lustre" photopaper to accomodate the more easy 
toner transfer, giving me 16 PCB's for 1 dollar. 

In the map Photo's you find pictures of the end result.

Overview of aspects of the PCB:

J1  jumper LCD
J2  input connector for A0
J3  connection NRF24L01
J4  output connector
J5  connector for 5V power supply  
J6  connector for 5V power supply via USB
J10 connector to LCD
J11 connector to PCB Pro mini
J12 connector to PCB Pro mini
J13 connector on PCB Pro mini for programming
R,R+,R- Pull up/down resitor for A0
R1  variable resistor for LCD
R2  protection resistor for A0
D1  protection zener diode for A0
C1  protection capacitor for A0
Rl  resistor for extra led
led extra led
jmp1a or jpm1b jumper for power via J5/J6 or VCC
jmp2 auto reset
jmp3 led
jmp4a or jmp4b LCD backlight. 
5V 3V - 5V connector
C+ C- capacitor

Below I refer to "generic male or female headers". By this I mean a x pins; form male or
female; package THT; hole size 1.0mm,0.508mm; pin spacing 0.1in (2.54mm); row single, 
connector.

J1  jumper LCD, 2 pin generic male header. Must be present if the optional LCD is used. Use
a female 2 pin jumper to feed 5V to the leds in the LCD. If you want to switch off the LCD, 
use this header for a on-off switch.


J2  input connector for A0, 3 pin generic male or female header. Solder a male or a 
female header, fitting your requirements. Normally I use a female header. Please note that
pin 0 = GND, pin 1 = +5V, pin 2 = link to A0.


J3  connection NRF24L01(+), 2*4 generic female header. If your application needs wireless 
transmission, insert the optional NRF24L01(+) module. Please note that these modules needs 
3,3 V power, so a voltage converter or a step down converter must be present, see below.

J4  output connector, 5 pin generic female header. The main purpose is to connect a single
or double relay brick, controlled by A1 and A2. Of couse these pins can also be used for 
other input or output purposes. Please note the sequence of pin1 (+5V) and pin2 (GND), so 
buy simmular relay bricks supporting a straight 3 of 4 pin cable. Pin5 is connected to A3 
and when not in use by extra led or the reset function, is also available for general 
purposes. 


J5  connector for 5V power supply, 3 pin generic male header. Use a 2 or 3 pin generic 
female header to supply power to this header. Please carefully note the sequence of the 
pins, pin 1 and 2 is GND, pin 3 is +5V. It is advised to supply 5V or 6V , and maximum 9V 
because with the allowed 12V the onboard step down converter of the Pro mini PCB becomes 
extremely hot. 
Personally I only use 230V to 5V USB type transformers without any instability problems.
 
 
J6  connector for 5V power supply via USB. Use a available DIP to USB converter PCB, which
can be ordered on Ebay. This allows a micro USB plug (or if you prefer a mini USB) to be 
used without the need to solder these SMT type of connectors. 

Connect jmp1a and NOT jpm1b to feed power to RAW pin of the Pro mini PCB, the leds of the 
LCD, the J5 connector and the step down converter for the NRF24L01(+). 


J10 connector to LCD, 16 pin generic female or male header. Using a LCD is optional. 
Normally a male connector is soldered to the PCB of the LCD and there a female connector on 
the PCB could be used. But if you want to mount the LCD in a housing it is practical to 
use a flat-ribbon cable 1.27 mm spacing with 2x16 female connector on both sides. The 2x16 
connector is obtainable in HW stores (Assman etc) and on Ebay. Personally I use an old 
floppy disc cable (2x17 connector), modified to the desired length. Ask your local PC shop 
for an old cable. Instruction how to lift a connector can be found on Google. The crimping 
of the connector I do (slowly) with a bench vise. 
Use jumper jmp4a to control the backlight of the LCD with D6 and PWM in your scetch. 
Use jumper jmp4b to get full backlight on the LCD.   


J11 and J12 connector to PCB Pro mini, both 12 pin generic female header. I always solder 
12 pin male headers to the PCB of the Arduino, and by using female headers on this PCB 
the Arduino can be easily removed.  


J13 connector on PCB Pro mini for programming, 6 pin generic male header. Soldered on the 
side of the PCB and used for loading sketches and Serial IO to a USB port on the PC. I use 
a FTDI FT232RL converter without any hazzle.
Power to the PCB of the pro mini can also be connected via J13. Connect jmp1b and NOT 
jpm1a to feed power to the other components. Also do NOT connect power via J5 nor J6.
However, if you do not connect voltage to the VCC pin of the Pro mini PCB, then you can 
supply power with J5 or J6 (and jmp3a), but never sypply power via J13 and J5/J6 
simultanously, this may blow up your Arduino. In this way you still have Serial IO to your 
PC over USB and a have very stable power supply.


R,R+,R- Pull up/down resitor for A0. Connect a 10 KOhm to 470 KOhm resistor between R+ and R
or between R- and R to create a pull up or pull down resistor on analog input A0. 


R1  variable resistor for LCD. Must be present if the optional LCD is used. A 10 KOhm 
varibale resistor to control the visibility of the characters on the LCD. 


If you want seriously protect the A0 input against overvoltage and spikes:
install R2, D1 and C1. 
See articles "http://www.thebox.myzen.co.uk/Tutorial/Protection.html" and 
"http://www.rugged-circuits.com/10-ways-to-destroy-an-arduino/", both very recommanded 
literature.

R2  protection resistor for A0. 22 Ohm resistor or prefebly a 220 Ohm resetable PTC 30 mA 
fuse (Bourns MF-R17).
D1  protection zener diode for A0. 4.7V or 5.1V zenerdiode.
C1  protection capacitor for A0. very small capacitor for example 22-100 pF for additional 
protection agaist spikes.


The port of the standard Arduino led at D13 is used by the LCD, therefore an extra led must
be connected via A3 if you want to use LED signals. An extra led can be placed on the PCB by:
Rl  resistor for extra led. 220 Ohm.
led standard 3mm led.
jmp3 led. jumper must be present
Please note that port A3 is also directly wired on J4.

 
jmp1a or jpm1b jumper for power via J5/J6 or VCC, discussed above.
jmp2 auto reset
jmp3 led, discussed above.
jmp4a or jmp4b LCD backlight, discussed above. 

5V 3V - 5V connector. The optional NRF24L01(+) module needs 3.3V for power. Therefore a 
voltage regulator or a step down converter should be used. The standard NRF24L01(+) can be 
fed from the VCC pin from the Pro mini, but not advised since the peak current from 80 mA 
is to high. Use a L78L33 TO-92 voltage regulator and solder this "transistor" in the 
upper "5V - 3V" connection points, so starting with the 5V nearest to J11/J12 of the Pro 
mini PCB. The bold site of the L78L33 must face the J3 connector of the NRF24L01(+). Always
check the wiringscheme of the regulator you bought.
However if you want to use a NRF24L01+PA+LNA module, which takes 180 mA current, you should 
use a DC 5V to 3.3V Step-Down converter, for example a Buck AMS1117-3.3 module, which can 
supply 800 mA current. Solder this mini PCB using the  "5V 3V -" connection points, so 
starting from the bottom of the PCB. In my case the  "transistor" component of the converter 
face the J3 connector of the NRF24L01(+).  Always check the wiringscheme of the step down 
converter you bought.
Both components can be found on Ebay, and looking at the minor price differences it is a 
good idea to use always the step down converter.
In either case always mount jmp1a.
In either case a capacitor of 47 uF, tantal or classical, between the C+ C- connection 
points is recommended. Please note that these connection points are 2 times present. 

Have fun.

Heinohein
