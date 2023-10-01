# Affinity hierarchies and amphiphilic proteins underlie the co-assembly of nucleolar and heterochromatin condensates

## Table of Contents  
[Overview](#overview)  
[System requirements](#system-requirements)  
[File description](#file-description)  
[How to run](#how-to-run)  

## Overview
The repository consists of scripts and code used to study the co-assembly of nucleolar and heterochromatin condensates. We use open source [LAMMPS](https://www.lammps.org/) package to to simulate four components of the nucleus: PCH (H) and ribosomal DNA (rD) as long polymers, and Fibrillarin (F) and an amphiphilic protein (X) as independent, single monomers.  
## System requirements
- LAMMPS is an open source software. To see system requirements for LAMMPS [click here](https://docs.lammps.org/Install.html).
- The analysis codes were tested on a Linux system (Ubuntu), but codes should work on MacOS or Windows system with corresponding C-compiler.


## File description
- system.data           - Initial input file with polymer configuration
- system_initial.in     - Initial Script file for LAMMPS to generate proteins molecules 
- system_final.in       - Main script file for LAMMPS to simulate four components: PCH, ribosomal DNA, Fibrillarin, and amphiphilic protein


## How to run
- Refer [LAMMPS documentation](https://docs.lammps.org/Install.html) for installation. Run LAMMPS using command (make sure that the configuration file system.data is present in the same directory)
```
./lmp_mpi -in system_initial.in >output_initial.out
mpirun -np 4 ./lmp_mpi -in system_final.in >output_final.out
```

Expected output: The simulation creates a position trajectory file in the lammpstrj format, employed for visualizing simulation results through [Ovito](https://www.ovito.org/) software. Additionally, the simulation produces an Analysis.txt file for calculating the distance between the center of mass of the PCH and Fibrillarin clusters.


Typical installation for LAMMPS software takes around 30 minutes. The initial simulation run takes less than 1 minute, while the final simulation run takes around 2 to 3 days.
