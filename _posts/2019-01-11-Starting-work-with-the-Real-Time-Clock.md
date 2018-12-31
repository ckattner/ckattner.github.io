---
title: Starting work with the Real Time Clock
layout: post
published: true
tags: arduino nixie
---

I spent some time earlier assembling my Nixie's with the driver boards, soldering one in.  I had planned on finishing a single tube today and then spending some time experimenting with it and the Arduino, but then I discovered I needed another breadboard to finish attaching all the pins that connect the breadboard to the Exixe board.  Since I'm now waiting until Thursday to be able to finish any of the hardware I decided I'd insteap spend some time today learning a little bit about the real time clock.

For starters, find the RTC module from your kit.  It's pretty simple to wire up:
* VCC -> 5V
* GND -> GND
* SCL -> SCL (on the Mega this is the pin nearest the USB port on the right)
* SDA -> SDA (this is the pin next to the SCL pin)

Next, we need to get some code onto the board utilizing the RTC.  The RTC requires loading a new library to be able to utilize it.  To add the library to our VS Code configuration, open up the `.vscode\c_cpp_properties.json` file and location the `includePath` section.  We'll need to add a new item to this list, which will be the absolute path to the library as provided by our kit provider.  In my case, that means adding `C:\path\to\sdk\English\Libraries\DS3231.zip` to the list.

Now lets load some code:
~~~~
#include <DS3231.h>

DS3231 clock;

void setup()
{
  Serial.begin(9600);

  Serial.println("Initialize RTC");

  clock.begin();

  // __DATE__ and __TIME__ will be expanded at compile time.
  clock.setDateTime(__DATE__, __TIME__);    
}

void loop()
{
  RTCDateTime dt = clock.getDateTime();

  Serial.print(dt.month);  Serial.print("/");
  Serial.print(dt.day);    Serial.print("/");
  Serial.print(dt.year);   Serial.print(" ");
  Serial.print(dt.hour);   Serial.print(":");
  Serial.print(dt.minute); Serial.print(":");
  Serial.print(dt.second); Serial.println("");

  delay(1000);
}
~~~~

This code is fairly simple.  First we include our necessary library, then initialize it and open the serial port for communication (we'll use this to verify that this code is running correctly in a minute).  Then start the clock and initialize it.

What do `__DATE__` and `__TIME__` mean though?  The `setDateTime` method takes a couple parameters: the date and the time (shocking, I know).  `__DATE__` and `__TIME__` are compile time macros, which means that when you compile your sketch, they will be replaced with the date and time when the compiler is running.  So, for example, if you compile your program on January 11, 2019 at 6:52 PM then those values will be substituted at compile.  This also means that every time you start this sketch on the Arduino, the clock will have its date and time set to January 11, 2019 at 6:52 PM.  That's probably not what we actually want, but it'll work for us for now.

Down in our loop all we're doing is getting the current datetime, printing it out, then pausing for 1 second before continuing.

To test that this works, start the serial monitor from the command palette using the `Arduino: Open Serial Monitor` command.  Doing so will open the serial monitor window where you should see a steady stream of time stamps being printed out.  If you were to turn off the Arduino for a minute or two, then restart and re-attach the serial monitor you'd see that the time appears to be incorrect in that it'll now be trailing a little bit.  This is because we called setDateTime with a compile time constant and we're calling it every time we start the device.  One thing we can do this is compile and load our sketch, then edit our source commenting out the `setDateTime` line and then loading that sketch.  Now we'll be able to take advantage of the fact that the RTC has a battery backup to store the datetime so we don't need to actually set it every time.

So that's it, we've loaded our first program to the Arduino and confirmed we can execute it.  We also now know how to store the date and time for our clock.

Hopefully next time I'll be ready with some hardware and we can try driving one of the Nixie tubes.  If not maybe I can work out how to use an LCD for a temporary display device until I have the Nixie's ready.
