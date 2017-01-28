# <a name="top"></a>AlarmAll
An alternate alarm system for people with hearing loss that integrates with existing alarms. Created at McHacks 2017.

## <a name="toc"></a>Table of Contents

## <a name="toc"></a> Existing Alarm Systems

Most alarm systems operate at high frequencies. For people with hearing loss, their hearing loss usually starts with high frequencies, usually [after 3 kHz](http://www.noisehelp.com/high-frequency-hearing-loss.html). To prevent this, there are very bright flashing lights, but that may trigger epilepsy in some individuals. Our goal is an easy-to-implement circuit that can be used with existing high-frequency alarms to notify deaf or hard of hearing individuals of an emergency safely and effectively.

[Back to Top] (#top)

## <a name="toc"></a> How it Works

The audio from the alarm goes through a high-pass filter. If audio over 3 kHz is detected, it will pass through this filter and a bright, non-flashing light will output.

[Back to Top] (#top)

### Initial Circuit Analysis/Simulation

#### Calculations/Schematic

Below are our initial calculations and schematics for the high-pass filter:

![Schematic](http://i.imgur.com/NpJeELF.jpg)

[Back to Top] (#top)

#### Bode Plot

After running PSpice on the circuit, we get the following Bode plot:

![Bode Plot](http://i.imgur.com/pRQAaEb.png)

[Back to Top] (#top)

### Addition of Op-Amp

However, we quickly realized that as the frequencies get higher, we will have a 0 volt output. In order to correct this, we added an opamp with a gain of 5.

[Back to Top] (#top)

#### Calculations/Schematic

Below are our calculations with a schematic:

![Op Amp Schematic](http://i.imgur.com/prgfTyo.jpg)

EDIT: The schematic is incorrect, here is the correct schematic:
![Corrected Schematic](http://i.imgur.com/xCA3YSW.jpg)

[Back to Top] (#top)

#### Bode Plot

Below is the Bode plot with the op-amp:

![Op Amp Bode Plot](http://i.imgur.com/qU692iu.png)

[Back to Top] (#top)

### Gain Corrections

#### Full Schematic

Using the Bode plot, we determined that the gain was too high. We then experimented with different resistor values and determined that the following setup was ideal:

![Full Schematic](http://i.imgur.com/mw1xjTD.png)

[Back to Top] (#top)

#### Bode Plot

With this setup, we get a near ideal Bode plot:

![Ideal Op Amp Bode Plot](http://i.imgur.com/VnWHBVS.png)

[Back to Top] (#top)
