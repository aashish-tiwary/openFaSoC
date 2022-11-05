# openFaSoC
FASoC: Fully-Autonomous SoC Synthesis using Customizable Cell-Based Synthesizable Analog Circuits
OpenFASOC is focused on open-source automate analog generation from user specification to GDSII with fully open-sourced tools. This project is led by a team of researchers at the University of Michigan is inspired from FASoC whcih sits on proprietary tools. (for more info visit https://fasoc.engin.umich.edu/)
# Prerequisites
Install all the prerequisites using dependencies.sh script provided in the home location of this project (where this readme.rst file is found). Supports CentOS7 and Ubuntu20. (Or) Please install the following tools by building the tools manually from their code base with the recommended commit ids for a stable functioning of the flow:

**Magic (version:8.3.334)**

**Netgen (version:1.5.240)**

**Klayout (version:0.27.10-1)**

Please use this command to build preferably: ./build.sh -option '-j8' -noruby -without-qt-multimedia -without-qt-xml -without-qt-svg

**Yosys (version:0.22+70)**

**OpenROAD (version:2.0_5525)**

**Open_pdks (version:1.0.353)**
open_pdks is required to run drc/lvs check and the simulations

After open_pdks is installed, please update the open_pdks key in common/platform_config.json with the installed path, down to the sky130A folder
Other notice:

**Python 3.7** is used in this generator.
All the required tools need to be loaded into the environment before running this generator.

# Design Generation
## Generators
**Temperature Sensor (temp-sense-gen)**
A fully automated SoC generator that uses an all-digital temperature sensor architecture, that relies on a new subthreshold oscillator (achieved using the auxiliary cell “Header Cell“) for realizing synthesizable thermal sensors.

**Temperature Sensor Description**

![image](https://user-images.githubusercontent.com/110485513/200106266-2ca32b43-0c40-4acd-95d6-8627350b5f55.png)

