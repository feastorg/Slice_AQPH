# Slice Template

Template for creating BREAD slices.

## Introduction

[Short introduction on the project.]

## Usage

[Explain how to use the project. Include examples and screenshots if applicable.]

## pH front end

The pH electrode connects to the BNC (J2). U2 (CA3140) amplifies its EMF and
U4 (TL081H) inverts it about a 1.98 V offset taken from the -5 V rail. The
result reaches the Nano's A0 through R7 (4.7 kΩ); D2 (BAT54) clamps A0 to
ground if U4 swings negative.

| | |
| --- | --- |
| Span | pH 0-14 over 0-60 °C |
| U2 gain | 3.99 at RV1 mid-travel (the nominal setting) |
| Trim (RV1) | gain 3.81-4.19 (-4.6 % / +5.0 %) |
| A0 at nominal gain | 0.48-3.50 V at 0 °C, 0.34-3.64 V at 25 °C, 0.14-3.83 V at 60 °C (pH 0 is the low end) |
| Resolution | 48.3 counts/pH at 25 °C on the 10-bit 0-5 V ADC (44.2 at 0 °C, 54.0 at 60 °C) |
| Bandwidth | -3 dB at 0.53 Hz with a 100 MΩ electrode |

At maximum trim A0 reaches 0 V only past an EMF of 475 mV, beyond pH 0 at
60 °C (463 mV); pH 14 at 60 °C reads 3.92 V. These are nominal figures:
before calibration the op-amps' offsets and input current can move A0 by up
to about ±90 mV (about ±0.4 pH).

**Electrode.** Use a combination glass electrode of at most 500 MΩ near room
temperature. U2's input current (10 pA typical, 50 pA maximum at 25 °C in
the CA3140 data sheet) flows through the electrode's resistance: up to
25 mV of offset at 500 MΩ, and it grows with temperature, as does the
resistance of a cold electrode.
C5 (2.2 nF across U2's input) is a C0G part, KEMET C0805C222J5GACTU, with
an insulation resistance of at least 100 GΩ at 25 °C; with the electrode it
forms a divider that reads 0.1 % low on a 100 MΩ electrode and 1 % low on
1 GΩ, which the calibration takes out.
Calibrate with two buffers (pH 7 and pH 4 or 10) at the working temperature,
and correct the slope for temperature in firmware (0.198 mV/K per pH).

**No electrode.** With the BNC open, U2's input floats on C5 (2.2 nF) and its
input current walks it to one rail (about 5 mV/s at 10 pA, about 18 mV/s at
A0). A0 then sits either at about -0.2 V, held by D2 (the ADC reads 0), or
near the +5 V rail at U4's positive limit (close to full scale); which one
depends on the part. Treat readings below 0.1 V or above 4.9 V as no electrode or over-range.

The SPICE check in `hardware/sim/` (`python3 hardware/sim/check.py`)
checks the span, gain, trim cap, bandwidth and clamp figures against the
schematic.

## Documentation

Please refer to the [docs](/docs) for more info.

---

<div align="center">
  <p>
    <img src="https://img.shields.io/badge/Developed_by-UWO--FAST--et--al-orange" alt="Developed by UWO-FAST et al.">
    <img src="https://img.shields.io/badge/Powered_by-Open_Source-blue" alt="Powered by Open Source">
  </p>
</div>