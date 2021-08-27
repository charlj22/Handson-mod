This is how I modified my Handson Tech motor shield to provide a current sense output for a Arduino.
I needed to do this so I could use the board with DCC++EX.
This is my board:http://www.handsontec.com/dataspecs/arduino-shield/L298P%20Motor%20Shield.pdf

*DO AT YOUR OWN RISK*

MOVE THE DESOLDERED PINS AS LITTLE AS POSIBLE

![alt text](https://github.com/charlj22/Handson-mod/blob/main/Images/20210816_071305.jpg?raw=true)
The second pins from the top on both sides of the big IC L298P needs to be desoldered. Its pins 2 and 15.

![alt text](https://github.com/charlj22/Handson-mod/blob/main/Images/20210816_124721.jpg?raw=true)
I used a piece of coper wire with a hook bent to help with lifting the pin while heating the solder joint.

![alt text](https://github.com/charlj22/Handson-mod/blob/main/Images/20210816_125156.jpg?raw=true)
Bend the pin up to clear the ground pane under it

![alt text](https://github.com/charlj22/Handson-mod/blob/main/Images/20210816_125156.jpg?raw=true)
Do the same for the other pin

![alt text](https://github.com/charlj22/Handson-mod/blob/main/Images/20210816_132055.jpg?raw=true)
![alt text](https://github.com/charlj22/Handson-mod/blob/main/Images/20210816_132338.jpg?raw=true)
Solder an piece of wire to the pins

![alt text](https://github.com/charlj22/Handson-mod/blob/main/Images/20210825_144405.jpg?raw=true)
Bend the wire so pin2 connects with the Analog0 header pin. Bend the wire so pin15 connects with the Analog1 header pin and solder them in place

![alt text](https://github.com/charlj22/Handson-mod/blob/main/Images/20210825_145049.jpg?raw=true)
Solder a 0.5 Ohm 2 Watt resistor between the Analog0 and Ground Headers. Do the same with the Analog1 header

In the DCC++EX config.h you have to change 

#define MOTOR_SHIELD_TYPE STANDARD_MOTOR_SHIELD 

to

#define HANDSON F("HANDSON"),\
  new MotorDriver(10, 12, UNUSED_PIN, UNUSED_PIN, A0, 2.80, 2000, UNUSED_PIN), \
  new MotorDriver(11, 13, UNUSED_PIN, UNUSED_PIN, A1, 2.80, 2000, UNUSED_PIN)

#define MOTOR_SHIELD_TYPE HANDSON

You might have to tweak the sense factor to suite your installation. I use 2.80 with mine.

