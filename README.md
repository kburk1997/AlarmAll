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

## <a name="inside"></a> Inside this Repository

This repository structure is as follows:

* `schematic` - All schematic files for this project.
* `code` - All Arduino/Raspberry Pi code for this project.
* `pictures` - Contains the following subfolders:
   * `analysis` - All pencil-and-paper circuit analysis calculations and sketches.
   * `pspice` - Contains the following subfolders:
     * `schematic-photos` - All schematic screenshots.
     * `bode` - All PSpice Bode plot screenshots.
   * `circuit` - All photos of the actual circuit.
   * `results` - All Discovery Board screenshots.
 
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

Since all Bode plots and Pspice results were correct, we began to build the circuit.

[Back to Top] (#top)
