# AlarmAll
An alternate alarm system for people with hearing loss that integrates with existing alarms.

## Existing Alarm Systems

Most alarm systems operate at high frequencies. For people with hearing loss, their hearing loss usually starts with high frequencies, usually [after 3 kHz](http://www.noisehelp.com/high-frequency-hearing-loss.html). To prevent this, there are very bright flashing lights, but that may trigger epilepsy in some individuals. Our goal is an easy-to-implement circuit that can be used with existing high-frequency alarms to notify deaf or hard of hearing individuals of an emergency safely and effectively.

## How it Works

The audio from the alarm goes through a high-pass filter. If audio over 3 kHz is detected, it will pass through this filter and a bright, non-flashing light will output.

Below are our initial calculations and schematics for the high-pass filter:

![Schematic](http://i.imgur.com/NpJeELF.jpg)
