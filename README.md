# Hierarchical Interactions Between Nucleolar and Heterochromatin Condensates Are Mediated by a Dual-Affinity Protein

The updated source code and input files can be downloaded from the link below:  
[Coarse-grained_model_of_nucleolar_heterochromatin_condensates-2.0.0.zip](https://github.com/user-attachments/files/20303025/Coarse-grained_model_of_nucleolar_heterochromatin_condensates-2.0.0.zip)

---

## Table of Contents  
- [Overview](#overview)  
- [System Requirements](#system-requirements)  
- [File Description](#file-description)  
- [How to Run](#how-to-run)  
- [Output Files](#output-files)  
- [Estimated Time](#estimated-time)

---

## Overview

This repository contains LAMMPS input scripts and data files for simulating the **hierarchical co-assembly of nucleolar and heterochromatin condensates**, focusing on the role of a **dual-affinity amphiphilic protein (Pitchoune)**.

The model includes four nuclear components:
- **PCH (heterochromatin)** – long polymer chain
- **rDNA (ribosomal DNA)** – optional long polymer chain
- **Fibrillarin** – free monomers
- **Pitchoune (X)** – amphiphilic monomers with affinity to both heterochromatin and nucleolar components

Two model variants are provided:
- **Plus rDNA** – includes rDNA chains  
- **Minus rDNA** – simulates a system without rDNA  

---

## System Requirements

- **LAMMPS** (Large-scale Atomic/Molecular Massively Parallel Simulator)  
  - Installation guide: [https://docs.lammps.org/Install.html](https://docs.lammps.org/Install.html)  
  - MPI-enabled build recommended for faster simulations

- **Tested on:**  
  - Ubuntu Linux (recommended)  
  - Should also run on macOS or Windows with compatible compilers and MPI setup

- **Visualization:**  
  - Use [OVITO](https://www.ovito.org/) to view `.lammpstrj` trajectory files

---

## File Description

| File Name                        | Description                                                    |
|----------------------------------|----------------------------------------------------------------|
| `system.data`                    | Initial configuration file containing polymer bead setup       |
| `system_initial_plus_rDNA.in`    | LAMMPS script to initialize system **with rDNA**               |
| `system_initial_minus_rDNA.in`   | LAMMPS script to initialize system **without rDNA**            |
| `system_final_plus_rDNA.in`      | Final production simulation script **with rDNA**               |
| `system_final_minus_rDNA.in`     | Final production simulation script **without rDNA**            |

---

## How to Run

1. **Install LAMMPS** (see: [https://docs.lammps.org/Install.html](https://docs.lammps.org/Install.html))

2. **Choose a variant:**  
   - With rDNA: use `*_plus_rDNA.in` scripts  
   - Without rDNA: use `*_minus_rDNA.in` scripts

3. **Run simulations:**

```bash
# Step 1: Initialization (place Fibrillarin and Pitchoune)
./lmp_mpi -in system_initial_plus_rDNA.in > output_initial.out

# Step 2: Final production run
mpirun -np 4 ./lmp_mpi -in system_final_plus_rDNA.in > output_final.out
