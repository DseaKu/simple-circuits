# Latch with two buttons and a DC motor

The two-transistor latch from `latch-two-buttons`, with a small DC motor as output.

## Files

- `latch-two-buttons-motor.kicad_pro` — KiCad project file
- `latch-two-buttons-motor.kicad_sch` — schematic
- `latch-two-buttons-motor.pdf` — schematic exported as PDF (`make pdf`)
- `Makefile` — generic KiCad Makefile (`make help` lists the targets)

## Circuit

- Q1 and Q2 form the latch, as in `latch-two-buttons`.
- SET (SW1) turns Q1 on. RESET (SW2) turns Q2 on.
- Q3 (2N3906, PNP) is the high-side switch for the motor.
- R5 (1k) connects the Q1 collector to the Q3 base. Q3 turns on when Q1 is on.
- M1 (DC motor) is between the Q3 collector and GND.
- D3 (1N4001) is a flyback diode across the motor.
- J1 is the 5 V supply input.

## Behaviour

| Action | Q1 | Q3 | Motor |
|---|---|---|---|
| Press SET (SW1) | on | on | runs |
| Press RESET (SW2) | off | off | stops |

The motor keeps its state after the buttons are released.

## Assumptions

- Supply: 5 V.
- Motor: small DC motor with a current below 150 mA at 5 V. Check the motor data sheet before you use it.
- The 2N3906 is rated for 200 mA. For a larger motor, use a higher-current PNP transistor.

## Status

- Schematic: done. ERC runs with 0 violations.
- PCB: not started.
