# Simple circuits

A collection of simple electronic circuits. Each circuit has its own folder with its KiCad project.

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

Build and export files (gerbers, drill files, BOM, PDF, and similar) are not tracked by git. See `.gitignore`.
