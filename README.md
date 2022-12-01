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
### Design 1: 
**Temperature Sensor (temp-sense-gen)**
A fully automated SoC generator that uses an all-digital temperature sensor architecture, that relies on a new subthreshold oscillator (achieved using the auxiliary cell “Header Cell“) for realizing synthesizable thermal sensors.

**Temperature Sensor Description**

![image](https://user-images.githubusercontent.com/110485513/200106266-2ca32b43-0c40-4acd-95d6-8627350b5f55.png)

### Circuit

![image](https://user-images.githubusercontent.com/110485513/200106392-6bbb2577-00c2-45ab-baab-f30d02525519.png)

# OpenFASOC Flow

![image](https://user-images.githubusercontent.com/110485513/200106800-f42f09d9-22e0-4604-96de-37f9a63781df.png)


The generator must first parse the user’s requirements into a high-level circuit description or verilog. User input parsing is implemented by reading from a JSON spec file directly in the temp-sense-gen repository. The JSON allows for specifying power, area, maximum error (temperature result accuracy), an optimization option (to choose which option to prioritize), and an operating temperature range (minimum and maximum operating temperature values). The operating temperature range and optimization must be specified, but other items can be left blank.

The generator uses this model file to automatically determine the number of headers and inverters, among other necessary modifications that can be made to meet spec. The generator references the model file in an iterative process until either meeting spec or failing. A verilog description is then produced by substituting specifics into several template verilog files.

# Verilog generation
Running make sky130hd_temp_verilog (temp for "temperature sensor") executes the temp-sense-gen.py script from temp-sense-gen/tools/. This file takes the input specifications from test.json and outputs Verilog files containing the description of the circuit.

![image](https://user-images.githubusercontent.com/110485513/200107537-867a419c-839d-438f-a973-03fa3e10d611.png)

To run the verilog generation, run the following command:

```make sky130hd_temp_verilog```

![tempver](https://user-images.githubusercontent.com/110485513/200107935-56d261bb-c4dd-4cc3-a0ad-fdf5dcea0040.png)

## Directories where the resulting verilog is Created:
The screenshot of the files created after running the make command is given below:

![src](https://user-images.githubusercontent.com/110485513/200108086-ecde591b-f4fd-49ea-a380-52406ca360c2.png)

### Design 2:
**PLL**
A phase-locked loop or phase lock loop (PLL) is a control system that generates an output signal whose phase is related to the phase of an input signal.
The phase difference of the reference and output clocks are captured by the embedded time-todigital converter (TDC), while the digital filter calculates the frequency control word for the digitally controlled oscillator (DCO). The input specification to the generator defines the nominal frequency range and in-band phase noise (PN). The PLL generator uses a physics-based mathematical model for characterization. We first build a mathematical relationship between DCO design parameters (number of aux-cells and stages) and the required DCO specifications. Using simulation results from a parametric sweep, we then find the effective ratio of drive strength and capacitance for each aux-cell. This ratio enables us to predict frequency and power results (frequency range, frequency resolution, frequency gain factor, and power consumption) given a set of input design parameters.


# Contributors
* Aashish Tiwary
* Kunal Ghosh
# Acknowledgments
Kunal Ghosh, Director, VSD Corp. Pvt. Ltd.

# Citations
Tutu Ajayi et al., ["An Open-source Framework for Autonomous SoC Design with Analog Block Generation,"](https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=9344104) 2020 IFIP/IEEE 28th International Conference on Very Large Scale Integration (VLSI-SOC), 2020, pp. 141-146.

# Contact Information
Aashish Tiwary, Postgraduate Student, International Institute of Information Technology, Bangalore aashish.tiwary@iiitb.ac.in Kunal Ghosh, Director, VSD Corp. Pvt. Ltd. kunalghosh@gmail.com




