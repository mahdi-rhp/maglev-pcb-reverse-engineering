# Maglev PCB Reverse Engineering

Educational and research reverse-engineering study of a commercial top-suspension magnetic levitation device, carried out in a university context. The project documents the disassembly, component identification, and reconstruction of the device's control circuit as a schematic and a 2-layer PCB.

> **Status:** Analysis and design reconstruction only. The reconstructed PCB was never fabricated or tested, so its correctness has not been verified experimentally.

## Overview

The device levitates a lamp beneath an overhead assembly, and a touch button controls the lamp's light. In many levitation devices the magnets, coil, and electronics sit below the floating object; here they are placed above it, which is a simpler configuration for the control problem.

The goal was to understand the electronic design by analyzing a real product and to reconstruct its circuit for study purposes. The device is purely analog/discrete: it contains no microcontroller, so there is no firmware.

## Scope

**Done**
- Purchased and disassembled the device, documenting every step with photos and video
- Identified and listed all components
- Traced the PCB connections (pads, tracks, vias) and recorded them
- Reconstructed the circuit as a schematic and a 2-layer PCB layout in Altium Designer

**Not done**
- Fabrication of the reconstructed PCB
- Functional testing of the reconstructed design

## System architecture

The levitation assembly uses four permanent magnets placed in four directions, a coil with a dedicated core driven at high frequency, and multiple Hall-effect sensors that detect the position of the levitated object. The control path, as identified from the circuit, is:

```
Hall sensors → op-amps (comparison with reference voltage)
            → analog switch → SMD transistors → MOSFETs → coil
```

1. The Hall sensor outputs are compared by op-amps against a reference voltage.
2. The reference voltage can be adjusted manually using a multi-turn trimmer, which sets the levitation operating point.
3. The comparison results go to an analog switch.
4. The analog switch controls small SMD transistors.
5. These transistors drive four MOSFETs, which switch the current in the coil.

## Components

| Qty | Component | Description | Role in this design |
|---|---|---|---|
| 2 | LM324 | Quad operational amplifier | Compare Hall-sensor signals against the reference voltage |
| 1 | MC14066BDG | Quad bilateral analog switch | Passes the comparison results on to the transistor stage |
| 2 | TL431ASA-7 | Adjustable shunt voltage reference | Provide the reference voltage used in the comparison stage |
| 4 | SMD transistor, marking  (SOT-23) | Small-signal transistor | Driver stage controlled by the analog switch; drives the MOSFETs |
| 4 | MOSFET | Power switch | Switch the coil current |
| 1 | Multi-turn trimmer | Precision potentiometer | Manual adjustment of the reference voltage |
| – | Hall-effect sensors | Magnetic field sensors | Detect the position of the levitated object |


## Methodology

1. Disassembly documented with photos and video.
2. Component identification and listing, using a digital microscope for small SMD parts.
3. Connectivity tracing using continuity testing with a multimeter.
4. Hand-drawn sketch of the traced circuit.
5. Schematic and 2-layer PCB (placement, tracks, vias) recreated in Altium Designer.

## Tools

Multimeter, digital microscope, Altium Designer.

## Images

<!-- Original device with levitating lamp; tracing in Altium beside the microscope setup; 2D and 3D Altium views; microscope close-up of the board. Remove logos and brand names. -->

## Challenges and lessons learned

<!-- Fill in from your own experience. -->

## Disclaimer

This repository is an educational analysis of a legally purchased product. The Altium files are my own reconstruction based on analysis of the device; they are not the manufacturer's original design files, and they have not been fabricated or tested. They are shared for educational purposes only.
