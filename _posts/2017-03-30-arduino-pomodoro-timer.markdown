---
layout: post
title:  "Arduino Pomodoro Timer"
date:   2017-03-30 23:40:00 +0200
tags:   arduino pomodoro
---

I have been thinking about making
a [Pomodoro](https://en.wikipedia.org/wiki/Pomodoro_Technique) timer
for quite a while. I thought of combining a tactile button-based timer
with a clear indicator light to make my colleagues aware or my work
mode, hopefully reducing interruptions during focus and flow.

This is what I've come up with:

![Pomodoro Timer](/img/pomodoro_red.jpeg){:class="img-responsive"}

This a 3d-printed/Arduino 25-minute + 5-minute Pomodoro timer, showing
a red indicator light while running. Then the Pomodoro is up, the
light turns green and sets a 5 second timer:

This is actually version 2. (My first Pomodoro
timer)[https://youtu.be/qhwcxlW7Q04] project ended up being fun but
not that useful.

![Pomodoro Timer](/img/pomodoro_green.jpeg){:class="img-responsive"}

The indicator light is also the button! The indicator is printed with
2 shells for a total 0.8 mm thickness in white filament. The diode
inside is a [8 mm diffuse
APA106](https://www.aliexpress.com/store/product/APA106-F8-8mm-round-hat-RGB-LED-with-APA-106-chipset-inside-full-color-frosted/701799_2043993382.html)
RGB diode with integrated IC (WS2812b compatible). I chose this
because I had some lying around. An PWM-driven RGB diode would also
work.

The inside is a spiderweb. It was an easy way to make it compact and
get the enclosure I wanted.

![Pomodoro Timer](/img/pomodoro_inside_front.jpeg){:class="img-responsive"}

![Pomodoro Timer](/img/pomodoro_inside_back.jpeg){:class="img-responsive"}

The 7-segment display is a 12-pin common anode type and takes up 12
pins on the Arduino.

Design and implementation choices:

* The 25-minute focus period and 5-minute break period are fixed
  (Pomodoro standard)
* The 25-minute focus period _can_ be interrupted by holding the
  button. The timer will return to idle mode.
* The 5-minute pause timer _can't_ be interrupted. This is to prevent
  myself from just restarting another Pomodoro focus period.

Ideas for version 3:

* Integrate with a PC-application that set all applications to _Do Not Disturb_.
* Completed Pomodoro counter or score.
* The indicator/button could be more robust

The [source, STL and FreeCAD files](https://github.com/larsch/arduino-pomodoro-timer) for
this project are available on GitHub.
