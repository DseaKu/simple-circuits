# Latch with two buttons (two transistors)

A bistable latch made of two NPN transistors (BC547).
Two push buttons set the state. The state holds after the buttons are released.

## Files

- `latch-two-buttons.kicad_pro` — KiCad project file
- `latch-two-buttons.kicad_sch` — schematic

## Circuit

- Q1 and Q2 are cross coupled. The collector of each transistor drives the base of the other through a 10k resistor (R3, R4).
- Each collector has a LED (D1 red, D2 green) with a 330 Ω resistor (R1, R2) to 5 V.
- SW1 (SET) pulls the base of Q2 to GND. Q2 turns off, Q1 turns on, and D1 lights.
- SW2 (RESET) pulls the base of Q1 to GND. Q1 turns off, Q2 turns on, and D2 lights.
- J1 is the 5 V supply input (pin 1 = VCC, pin 2 = GND).

## Behaviour

| Action | Q1 | Q2 | Lit LED |
|---|---|---|---|
| Press SET (SW1) | on | off | D1 (red) |
| Press RESET (SW2) | off | on | D2 (green) |
| Release both | keeps last state | keeps last state | keeps last state |

At power-up, the state is not defined. Press SET or RESET once to set a known state.

## Status

- Schematic: done. ERC runs with 0 violations.
- PCB: not started.
