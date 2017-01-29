# <a name="top"></a>AlarmAll
An alternate alarm system for people with hearing loss that integrates with existing alarms. Created at McHacks 2017.
## <a name="toc"></a>Table of Contents
* [Inside this Repository](#inside)
* [Existing Alarm Systems](#existing)
* [How it Works](#works)
* [Engineering Process/Specs](#process)
  * [Initial Circuit Analysis/Simulation](#initial)
    * [Calculations/Schematic](#calculations1)
    * [Bode Plot](#bode1)
  * [Addition of Op-Amp](#opamp)
    * [Calculations/Schematic](#calculations2)
    * [Bode Plot](#bode2)
  * [Gain Corrections](#corrections)
    * [Full Schematic](#schematic)
    * [Bode Plot](#bode3)
  * [Circuit Construction](#circuit)
  * [Debugging Fun Facts](#debugging)
    * [All Attempted Bug Fixes](#fixes)
    * [% Error Table](error)

## <a name="inside"></a> Inside this Repository

This repository structure is as follows:

* `schematic` - All schematic files for this project.
* `pictures` - Contains the following subfolders:
   * `analysis` - All pencil-and-paper circuit analysis calculations and sketches.
   * `pspice` - Contains the following subfolders:
     * `schematic-photos` - All schematic screenshots.
     * `bode` - All PSpice Bode plot screenshots.
   * `circuit` - All photos of the actual circuit. 
[Back to Top] (#top)


## <a name="existing"></a> Existing Alarm Systems

Most alarm systems operate at high frequencies. For people with hearing loss, their hearing loss usually starts with high frequencies, usually [after 3 kHz](http://www.noisehelp.com/high-frequency-hearing-loss.html). To prevent this, there are very bright flashing lights, but that may trigger epilepsy in some individuals. Our goal is an easy-to-implement circuit that can be used with existing high-frequency alarms to notify deaf or hard of hearing individuals of an emergency safely and effectively.

[Back to Top] (#top)

## <a name="works"></a> How it Works

The audio from the alarm goes through a high-pass filter. If audio over 3 kHz is detected, it will pass through this filter and a bright, non-flashing light will output.

[Back to Top] (#top)

## <a name="process"></a> Engineering Process/Specs

Below describes, in detail, the process of building the project. Calculations, schematics, simulation screenshots, Bode plots, circuit pictures, and Discovery Board screenshots are all included.

[Back to Top] (#top)

### <a name="initial"></a> Initial Circuit Analysis/Simulation

#### <a name="calculations1"></a> Calculations/Schematic

Below are our initial calculations and schematics for the high-pass filter:

![Schematic](http://i.imgur.com/NpJeELF.jpg)

[Back to Top] (#top)

#### <a name="bode1"></a> Bode Plot

After running PSpice on the circuit, we get the following Bode plot:

![Bode Plot](http://i.imgur.com/pRQAaEb.png)

[Back to Top] (#top)

### <a name="opamp"></a> Addition of Op-Amp

However, we quickly realized that as the frequencies get higher, we will have a 0 volt output. In order to correct this, we added an opamp with a gain of 5.

[Back to Top] (#top)

#### <a name="calculations2"></a> Calculations/Schematic

Below are our calculations with a schematic:

![Op Amp Schematic](http://i.imgur.com/prgfTyo.jpg)

EDIT: The schematic is incorrect, here is the correct schematic:
![Corrected Schematic](http://i.imgur.com/xCA3YSW.jpg)

[Back to Top] (#top)

#### <a name="bode2"></a> Bode Plot

Below is the Bode plot with the op-amp:

![Op Amp Bode Plot](http://i.imgur.com/qU692iu.png)

[Back to Top] (#top)

### <a name="corrections"></a> Gain Corrections

#### <a name="schematic"></a> Full Schematic

Using the Bode plot, we determined that the gain was too high. We then experimented with different resistor values and determined that the following setup was ideal:

![Full Schematic](http://i.imgur.com/mw1xjTD.png)

[Back to Top] (#top)

#### <a name="bode3"></a> Bode Plot

With this setup, we get a near ideal Bode plot:

![Ideal Op Amp Bode Plot](http://i.imgur.com/VnWHBVS.png)

[Back to Top] (#top)

### <a name="circuit"></a> Circuit Construction

Since all Bode plots and Pspice results were correct, we began to build the circuit. However, the circuit ended up not working. Through hours of tedious debugging, we determined our Discovery Board was failing and we had no other alternative (since Arduino, Pi, etc. cannot produce the analog sine wave we need).

Here is our actual circuit:

![Circuit](http://i.imgur.com/dLGPXNU.jpg)

[Back to Top] (#top)

### <a name="debugging"></a> Debugging Fun Facts

####  <a name="fixes"></a> All Attempted Bug Fixes

Here is a list of actual attempted bug fixes:
* First we removed the opamp and tested the circuit with a unity gain. It still wasn't working according to the unity gain Bode plot.
* We tried recalculating resistor and capacitor values. Those were correct.
* If we held the wire, the circuit would magically work. That doesn't happen anymore.
* We tried taping everything down with masking tape to no avail.
* We tried turning the Discovery Board on and off. Several times.
* We stripped wires with our teeth because we suspected the provided wires were incompatible.
* We changed breadboards. Twice.
* We inserted the wires through a juice box straw to attempt to get voltage across a wire. It didn't work.

[Back to Top] (#top)

#### <a name="error"></a> % error

Here was our % error table for the unity gain:

|Frequency (Hz) | PSpice Output (dB) | Measured Output (dB) | % Error |
|---|---|---|---|
|10|-49.21|-50.46|2.54%|
|100|-29.426|-4.61245|84.33%|
|1000|-5.3652|-0.819|84.73%|
|3000|1.58|0|100%|
|10000|4.1649|n/a|n/a|

Here was our % error table for the circuit with the opamp:

|Frequency (Hz) | PSpice Output (dB) | Measured Output (dB) | % Error |
|---|---|---|---|
|10|-44.757|-17.2024|62%|
|100|-24.862|-4.61245|81%|
|1000|-5.3269|11.607|318%|
|3000|1.4862|n/a|n/a|
|10000|4.1994|n/a|n/a|

[Back to Top] (#top)
