# Hierarchical interactions between nucleolar and heterochromatin condensates are mediated by a dual-affinity protein

## Table of Contents  
- [Overview](#overview)  
- [System Requirements](#system-requirements)  
- [File Description](#file-description)  
- [How to Run](#how-to-run)  
- [Output Files](#output-files)  
- [Estimated Time](#estimated-time)

---

## Overview

This repository contains LAMMPS input scripts and data files for simulating the **co-assembly of nucleolar and heterochromatin condensates**, focusing on the role of a **dual-affinity protein (Pitchoune)**.

The model includes four nuclear components:
- **PCH (Heterochromatin)** – a 10,000-bead polymer chain
- **rDNA (Ribosomal DNA)** – optional region of 2000 beads (IDs 4001–6000) relabeled from the PCH chain
- **Fibrillarin** – added as free monomers
- **Pitchoune (X)** – added as dual-affinity monomers

Two simulation variants are provided:
- **+rDNA**: includes rDNA by relabeling part of the polymer
- **–rDNA**: rDNA is retained in the chain but all its interactions are turned off, so the entire polymer behaves as PCH

---

## System Requirements

- **LAMMPS** – [Installation guide](https://docs.lammps.org/Install.html)  
  MPI-enabled build is recommended for multi-core performance.

- **Platform Compatibility:**  
  Tested on **Ubuntu Linux**. Should also work on macOS or Windows with compatible compilers and MPI setup.

- **Visualization:**  
  [OVITO](https://www.ovito.org/) – to visualize `.lammpstrj` trajectory files

---

## File Description

| File Name                        | Description |
|----------------------------------|-------------|
| `system.data`                    | Initial configuration with only the 10,000-bead PCH polymer chain. No rDNA, Fibrillarin, or Pitchoune are included at this stage. |
| `system_initial_plus_rDNA.in`    | Initialization script to add Fibrillarin and Pitchoune monomers, and relabel the middle 2000 beads (IDs 4001–6000) as rDNA (type 2). Applies confinement, minimization, and writes the modified system to `system_after_initial.data`. |
| `system_initial_minus_rDNA.in`   | Same as above, but **without** rDNA relabeling—all 10,000 beads remain as PCH. Adds Fibrillarin and Pitchoune. |
| `system_final_plus_rDNA.in`      | Final production simulation script (with rDNA). Loads `system_after_initial.data`, defines interactions and observables, and runs dynamics. |
| `system_final_minus_rDNA.in`     | Final simulation script for the –rDNA system. Similar setup without rDNA-specific interactions. |

---

## How to Run

1. **Install LAMMPS** following the [official guide](https://docs.lammps.org/Install.html)

2. **Choose a model variant:**
   - Use `*_plus_rDNA.in` for simulations with rDNA
   - Use `*_minus_rDNA.in` for simulations without rDNA

3. **Run simulations:**

```bash
# Step 1: Run initialization to add fibrillarin, pitchoune, and optionally rDNA
./lmp_mpi -in system_initial_plus_rDNA.in > output_initial.out

# Step 2: Run production dynamics on the initialized system
mpirun -np 4 ./lmp_mpi -in system_final_plus_rDNA.in > output_final.out
