
\newpage
\thispagestyle{empty}
\mbox{}

\newpage

![](content/workshop_images/home.jpg)

\customtitlepage{Hack Your House}

>Have you ever wanted to live in a house like the Jetsons? We will be taking the first step into this inevitable future in our workshop! You will learn to build a system that notifies you immediately of an unexpected environmental change such as gas in the air or a strange loud noise in your house. We will teach you to make your home smarter by using just an Arduino, some awesome analog and digital sensors, and a set of powerful web APIs.

### Authors

__Jon Gottfried__ has been hacking on hardware since 2005, where he built competitive autonomous firefighting robots with PIC boards. Lately, he has been working on some home automation projects and phone-controlled robots that he is turning into tutorials for Twilio DIY Home Automation using Twilio and Twilio Robot as well as some Google Glass-controlled robots for fun. He loves hacking and loves teaching.

\newpage

# Hack Your House

## Overview

In this workshop you will learn how to build your own smart RFID-controlled deadbolt lock. We will be using an Arduino Uno, a servo, and a few sensors to modify a deadbolt lock so that you can control it via software and unlock it with an RFID tag. You will be able to mount our Arduino to your existing deadbolt without physically modifying or damaging it!

## Preparations

Download the Arduino IDE from <http://arduino.cc/en/Main/Software> and install it on your system.

## Main flow

### Step 1: Hello Robot!

We are going to start off by making sure that you are able to upload code to your Arduino using the Blink tutorial (<http://arduino.cc/en/tutorial/blink>). One of the best things about Arduino is the amazing open source community that exists around it. We will be making use of a number of open source examples as we build our smart lock!

Plug your LED power into pin 13 of your Arduino and ground into the GND pin next to it. The shorter pin is Ground (-) for LEDs.

![](content/workshops/home/image04.jpg)

Plug your Arduino into your computer via USB.

Open the Arduino IDE, select: *File > Examples > 01.Basics > Blink* and click the *Upload* button to install the Blink program on your board.

If you successfully uploaded your program, the LED that you plugged into your Arduino should be blinking on and off every second!

### Step 2: Connect and Test a Servo

Now that we are sure that you can program your Arduino, we will move on to the fun stuff and connect our servo to our board.

A servo is a type of motor that typically has a 180 degree movement radius. Later in the workshop, we will be using our servo to control the movement of a deadbolt lock.

For now, we just want to connect our servo to our Arduino and make sure we are able to control it via a simple program.

A servo motor has three wires - power (red), ground (black), and control (frequently yellow or white). Connect the power wire to the 5V pinout on the Arduino and the ground wire to the GND pinout next to it. We can then connect the control wire to Digital Pin 12 on our Arduino as in the following diagram:

![](content/workshops/home/image02.jpg)

Now that our servo is connected to the Arduino, we will need to write the software to control it. Let’s create a new file and start it off with the following code:

~~~~ {.numberLines}
#include <Servo.h>
Servo myservo;
~~~~~~~

This snippet includes the Servo library and defines a new Servo object that we will use later to control our servo motor.

Next, we can create two methods: `loop()` and `setup()` - these methods are common to every Arduino program. The `setup()` method runs when the Arduino turns on, and the `loop()` method constantly runs on a loop (as the name would suggest).

In our `setup()` method, we will attach our myservo object to pin 10 where we plugged in the servo earlier. The method should look like this when we are done:

~~~~ {.numberLines}
void setup()
{
  myservo.attach(12);
}
~~~~~~~

Now that the Arduino knows where to find our Servo, we can experiment a bit. In order to move the servo to a new position, you use the `myservo.write(pos);` method. pos is an integer from 0 to 180. Try using `myservo.write(pos);` in both the `setup()` and `loop()` methods - see what happens when you set pos to different values. Note that you can use the delay() method to pause execution between different commands.
For example:

~~~~ {.numberLines}
  myservo.write(180);
  delay(1000);
  myservo.write(0);
~~~~~~~

This snippet would move the servo to position 180, pause for 1 second, and then move the servo to position 0.

After each modification, Upload your code to the Arduino again. You can view the progress of your upload in the log console on the bottom of your Arduino IDE.

Once you are comfortable with controlling your Servo, we can move on. Additional examples are available here: <http://arduino.cc/en/Tutorial/Sweep>

### Step 6: Mounting to your lock

Now that the software side of our project is done, we must mount the servo to our deadbolt lock. I prefer to use household items when prototyping these types of applications, though if you have access to a 3D printer I would recommend designing and printing your own lock mount.

For the purpose of prototyping, we will be using cardboard and duct tape to mount our servo to our lock - just like astronauts do!

Attach the two metal rods to your servo with screws and washers.

\newpage

![](content/workshops/home/image00.jpg)

Now use a piece of cardboard (or other stiff material) to make a tighter bond between the servo and the lock:

![](content/workshops/home/image07.jpg)

![](content/workshops/home/image10.jpg)

Now you can tape the servo to the deadbolt lock. Make sure it is positioned on the correct side so that the direction that the servo turns in is aligned with the direction that the lock turns in:

\newpage

![](content/workshops/home/image11.jpg)

And last but not least, we will tape our servo’s arms to the deadbolt itself:

![](content/workshops/home/image09.jpg)

Now you have your fully mounted (and fully impermanent) servo-controlled deadbolt:

![](content/workshops/home/image06.jpg)


## Second flow (optional)

At this point, you have built an RFID-controlled deadbolt using your Arduino, a servo, and an RFID reader. But when it comes to home automation, there is always more to be done!

### Experiment 1: Motion-Controlled Deadbolt

This first experiment is the simplest (and most insecure) - we will unlock or lock our door every time we detect movement in front of it.

Take the PIR motion sensor and wire it into your Arduino (VCC to +5V, GND to GND, and control to digital pin 2) - NOTE that the middle wire of the PIR sensor is GND, not the black wire. This is strange, but true. The red (+) wire is still VCC (the sensor should have a + and AL marking on it to distinguish this):

![](content/workshops/home/image08.jpg)

You will need to use an internal pull-up to activate the motion sensor. This is done by setting digital pin 2 as an INPUT pin and then writing a HIGH value to it. Once you Arduino turns on, you need to wait a second or two for the PIR motion sensor to get a reading on a room without movement. Then you can start waving your arms all around!

When motion is detected, lock or unlock your deadbolt.

You can find additional details on the sensor here: <https://www.sparkfun.com/products/8630>

If you get stuck you can find the solution here: <https://gist.github.com/jonmarkgo/9060847>

Great work and happy hacking!
