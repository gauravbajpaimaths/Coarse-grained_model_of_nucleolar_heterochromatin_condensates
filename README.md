# Affinity Hierarchies and Amphiphilic Proteins Underlie the Co-Assembly of Nucleolar and Heterochromatin Condensates

The updated source code and input files can be downloaded from this link:  
[Coarse-grained_model_of_nucleolar_heterochromatin_condensates-2.0.0.zip](https://github.com/user-attachments/files/20303025/Coarse-grained_model_of_nucleolar_heterochromatin_condensates-2.0.0.zip)

---

## Table of Contents  
- [Overview](#overview)  
- [System Requirements](#system-requirements)  
- [File Description](#file-description)  
- [How to Run](#how-to-run)  

---

## Overview

This repository contains all input scripts and data files used to simulate the **co-assembly of nucleolar and heterochromatin condensates** using the molecular dynamics engine [LAMMPS](https://www.lammps.org/).

The model represents four key nuclear components:
- **PCH (Heterochromatin)** – modeled as a long polymer chain  
- **Ribosomal DNA (rDNA)** – modeled as another long polymer chain  
- **Fibrillarin (F)** – modeled as free monomers  
- **Pitchoune (X)** – modeled as independent amphiphilic monomers  

The simulations explore how **molecular interactions, spatial confinement**, and **relative affinities** among components lead to phase-separated nuclear compartments.

---

## System Requirements

- **LAMMPS** (Large-scale Atomic/Molecular Massively Parallel Simulator)  
  - Official install guide: [https://docs.lammps.org/Install.html](https://docs.lammps.org/Install.html)  
  - MPI-enabled build recommended for parallel execution

- **Operating system:**  
  - Tested on **Ubuntu Linux**  
  - Should also work on macOS or Windows with compatible C/C++ compilers and MPI setup

- **Visualization tool:**  
  - [OVITO](https://www.ovito.org/) for viewing `.lammpstrj` trajectory files

---

## File Description

- `system.data`  
  Initial configuration file containing the bead-spring polymer setup

- `system_initial.in`  
  LAMMPS script to initialize the system by adding Fibrillarin and Pitchoune molecules and confining them

- `system.in`  
  Main LAMMPS script to simulate the system dynamics, compute observables (e.g., center-of-mass distances, cluster sizes, radius of gyration), and save output

- `README.md`  
  This documentation file

---

## How to Run

1. **Install LAMMPS** following the [official instructions](https://docs.lammps.org/Install.html).

2. **Run the simulations** (make sure `system.data`, `system_initial.in`, and `system.in` are in the same directory):

```bash
# Step 1: Run initial setup to place proteins and perform initial minimization
./lmp_mpi -in system_initial.in > output_initial.out

# Step 2: Run the full dynamics simulation (multi-core recommended)
mpirun -np 4 ./lmp_mpi -in system.in > output_final.out
