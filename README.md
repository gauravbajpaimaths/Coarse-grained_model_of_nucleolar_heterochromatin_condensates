# Hierarchical Interactions Between Nucleolar and Heterochromatin Condensates Are Mediated by a Dual-Affinity Protein

## Table of Contents  
- [Overview](#overview)  
- [System Requirements](#system-requirements)  
- [File Description](#file-description)  
- [How to Run](#how-to-run)  
- [Output Files](#output-files)  
- [Estimated Time](#estimated-time)

---

## Overview

This repository contains LAMMPS input scripts and data files for simulating the **hierarchical co-assembly of nucleolar and heterochromatin condensates**, with a focus on the role of a **dual-affinity amphiphilic protein (Pitchoune)**.

The model includes four nuclear components:
- **PCH (Heterochromatin)** – modeled as a 10,000-bead polymer chain  
- **rDNA (Ribosomal DNA)** – represented as a 2000-bead **middle segment** of the PCH chain in the `+rDNA` case  
- **Fibrillarin** – modeled as free monomers  
- **Pitchoune (X)** – an amphiphilic monomer that interacts with both chromatin and nucleolar components

Two variants of the simulation are provided:
- **+rDNA**: includes the middle 2000-bead rDNA segment  
- **–rDNA**: treats the full 10,000-bead polymer as PCH without rDNA

---

## System Requirements

- **LAMMPS** (Large-scale Atomic/Molecular Massively Parallel Simulator)  
  - Installation: [https://docs.lammps.org/Install.html](https://docs.lammps.org/Install.html)  
  - MPI-enabled build is recommended for faster simulations

- **Operating system:**  
  - Tested on **Ubuntu Linux**  
  - Should also run on macOS or Windows with compatible compilers and MPI setup

- **Visualization:**  
  - Use [OVITO](https://www.ovito.org/) to view `.lammpstrj` trajectory files

---

## File Description

| File Name                        | Description |
|----------------------------------|-------------|
| `system.data` | Initial configuration file defining a 10,000-bead polymer chain representing PCH. In the `+rDNA` variant, the middle 2000 beads (bead IDs 4001–6000) are relabeled as rDNA. |
| `system_initial_plus_rDNA.in` | LAMMPS script to initialize the system **with rDNA**. It adds Fibrillarin and Pitchoune monomers and assigns bead type 2 to the rDNA segment. A short energy minimization and relaxation are performed. |
| `system_initial_minus_rDNA.in` | Initialization script **without rDNA**. All 10,000 beads remain as heterochromatin (PCH). Fibrillarin and Pitchoune are added similarly. |
| `system_final_plus_rDNA.in` | Production simulation script for the `+rDNA` system. Includes detailed pairwise interactions, Langevin thermostat, NVE integration, and observables such as COM distance, cluster size, and radius of gyration. |
| `system_final_minus_rDNA.in` | Production simulation script for the `–rDNA` system. Same analysis as above, but without distinguishing rDNA. |

---

## How to Run

1. **Install LAMMPS** by following the [installation instructions](https://docs.lammps.org/Install.html)

2. **Choose a variant to simulate:**
   - **With rDNA**: use the `*_plus_rDNA.in` files  
   - **Without rDNA**: use the `*_minus_rDNA.in` files

3. **Run the simulation:**

```bash
# Step 1: Run initial setup
./lmp_mpi -in system_initial_plus_rDNA.in > output_initial.out

# Step 2: Run production dynamics
mpirun -np 4 ./lmp_mpi -in system_final_plus_rDNA.in > output_final.out
