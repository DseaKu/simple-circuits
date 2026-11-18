# Simple circuits

## About

Simple circuits is a collection of small electronic circuits. Each circuit has its own folder with a KiCad project, a schematic, and a Makefile. The Makefile runs the electrical rule check and exports the netlist, the PDF schematic, and the bill of materials. The folder `latch-two-buttons` is the first circuit and the template for the others.

## Circuits

- [latch-two-buttons](latch-two-buttons/) — Latch with SET and RESET buttons, two transistors.

## Folder layout

```
simple-circuits/
├── .gitignore
├── README.md
└── <circuit-name>/
    ├── <circuit-name>.kicad_pro
    ├── <circuit-name>.kicad_sch
    └── README.md
```

Build and export files (gerbers, drill files, BOM, and similar) are not tracked by git. The schematic PDF is tracked. See `.gitignore`.
