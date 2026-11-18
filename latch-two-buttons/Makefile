# Generic KiCad Makefile for one circuit folder.
# Finds the project files by extension, so it works in any circuit folder.
# Copy this file into a new circuit folder and run: make

KICAD_CLI ?= kicad-cli
OUT       ?= build

# First matching file of each type in this folder
SCH := $(firstword $(wildcard *.kicad_sch))
PCB := $(firstword $(wildcard *.kicad_pcb))

GERBER_LAYERS := F.Cu,B.Cu,F.Paste,B.Paste,F.SilkS,B.SilkS,F.Mask,B.Mask,Edge.Cuts

.PHONY: help all check erc netlist pdf bom drc gerbers drill release clean

help:
	@echo "Targets:"
	@echo "  make erc      Run the schematic ERC (fails on violations)"
	@echo "  make netlist  Export the netlist (XML)"
	@echo "  make pdf      Plot the schematic to PDF, next to the schematic"
	@echo "  make bom      Export the bill of materials (CSV)"
	@echo "  make drc      Run the PCB DRC (fails on violations)"
	@echo "  make gerbers  Export the gerber files"
	@echo "  make drill    Export the drill files"
	@echo "  make release  gerbers + drill"
	@echo "  make all      erc, netlist, pdf, bom"
	@echo "  make clean    Delete the $(OUT)/ folder"
	@echo ""
	@echo "Schematic: $(or $(SCH),none found)"
	@echo "PCB:       $(or $(PCB),none found)"

all: erc netlist pdf bom

check:
	@test -n "$(SCH)" || (echo "No .kicad_sch file in this folder" && exit 1)

$(OUT):
	mkdir -p $(OUT)

erc: check | $(OUT)
	$(KICAD_CLI) sch erc --severity-all --exit-code-violations --format json --output $(OUT)/erc.json $(SCH)

netlist: check | $(OUT)
	$(KICAD_CLI) sch export netlist --format kicadxml --output $(OUT)/netlist.xml $(SCH)

pdf: check
	$(KICAD_CLI) sch export pdf --output $(basename $(SCH)).pdf $(SCH)

bom: check | $(OUT)
	$(KICAD_CLI) sch export bom --output $(OUT)/bom.csv $(SCH)

check-pcb:
	@test -n "$(PCB)" || (echo "No .kicad_pcb file in this folder" && exit 1)

drc: check-pcb | $(OUT)
	$(KICAD_CLI) pcb drc --severity-all --exit-code-violations --format json --output $(OUT)/drc.json $(PCB)

gerbers: check-pcb | $(OUT)
	mkdir -p $(OUT)/gerbers
	$(KICAD_CLI) pcb export gerbers --layers $(GERBER_LAYERS) --output $(OUT)/gerbers/ $(PCB)

drill: check-pcb | $(OUT)
	mkdir -p $(OUT)/gerbers
	$(KICAD_CLI) pcb export drill --output $(OUT)/gerbers/ $(PCB)

release: gerbers drill

clean:
	rm -rf $(OUT)
