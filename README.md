
Chemical Reactor Simulation Tool

A Python-based GUI application for analyzing and comparing the performance of Continuous Stirred Tank Reactors (CSTR) and Plug Flow Reactors (PFR).

Features

- Calculate reaction rate constant using the Arrhenius equation
- Calculate reactor residence time
- Calculate CSTR conversion
- Calculate PFR conversion
- Compare CSTR and PFR performance
- Plot temperature vs conversion
- Determine the minimum temperature required for a target conversion
- Calculate the required reactor volume for a target conversion
- Reset all inputs and results using the GUI

Technologies Used

- Python
- Tkinter
- Matplotlib
- Math module

Engineering Concepts

The project uses chemical reaction engineering concepts such as:

- Arrhenius equation
- Reaction rate constant
- Residence time
- CSTR material balance
- PFR material balance
- Conversion
- Reactor design calculations

How It Works

The user enters:

- Temperature
- Reactor volume
- Flow rate
- Target conversion

The program then calculates the reaction rate constant and residence time and uses them to determine the conversion for both CSTR and PFR reactors.

The application also provides graphical comparison and basic reactor design calculations.

How to Run

1. Install Python.
2. Install Matplotlib:

pip install matplotlib

3. Run the program:

python chemical reactor simulation.py

Project Purpose

This project was developed to combine Python programming with chemical engineering concepts, providing a simple interactive tool for reactor analysis and design.

Author

Hemanth