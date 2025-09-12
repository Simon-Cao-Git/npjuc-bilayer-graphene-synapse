# Computational Workflow for Li Diffusion in Bilayer Graphene

This repository documents the computational work underlying the paper:  
**“Artificial synapse with tunable dynamic range for neuromorphic computing with ion intercalated bilayer graphene”** (npj *Unconventional Computing*). A citation to our paper will be added here once the final publication details are available. 

We supplement the experimental findings by investigating the energetics and diffusion properties of lithium (Li) in bilayer graphene using **density functional theory (DFT)**.  

---

## Methods Overview  

- **DFT Package:** VASP 5.4.4  
- **Pseudopotentials:** Projector Augmented-Wave (PAW) method with the PBE functional
  *Note: POTCAR files are not included in this repository, as they are proprietary to VASP.*
- **Dispersion Correction:** DFT-D3 (Grimme, zero-damping)  
- **Calculation Types:**  
  - **Single-point energies** (some after relaxation)  
  - **Climbing-Image Nudged Elastic Band (CI-NEB)** calculations for diffusion barriers  

---

## Workflow  

All calculations were carried out using a plane-wave kinetic energy cutoff of **400 eV**. Electronic self-consistency was considered achieved when the total energy difference between successive steps was less than **1×10⁻⁴ eV**. To prevent spurious interactions, a vacuum spacing of at least **15 Å** was applied along the non-periodic direction in all models. For nanoribbon geometries, all exposed edge carbon atoms were passivated with hydrogen.  

The Brillouin zone was sampled using Γ-centered grids.  
- **Bilayer graphene (3 × 3 supercell):** 15 × 15 × 1 mesh  
- **Bilayer graphene (6 × 6 supercell):** 4 × 4 × 1 mesh  
- **Bilayer graphene Nanoribbons:** 8 Γ-centered *k*-points along the periodic axis and Γ-only sampling in the transverse directions  

*Note: The exact sampling details for each calculation can also be found in the `KPOINTS` files within the subdirectories.*  

### Single-Point Calculations  
1. Whenever possible, structures were first relaxed prior to single-point evaluations.  
2. Structural relaxations employed the **conjugate gradient (CG)** algorithm, with all atomic positions relaxed until the residual forces were **≤ 0.01 eV/Å**.  
3. Final single-point energies were extracted from these minimized structures.  

### CI-NEB Calculations  
1. Both **initial** and **final** states were minimized to the same **≤ 0.01 eV/Å** force threshold.  
2. CI-NEB calculations were then performed to determine diffusion pathways and energy barriers.  
3. Depending on the complexity of the pathway, different NEB force thresholds were used, but in all cases convergence was achieved with forces **≤ 0.05 eV/Å**.   

---

## Repository Structure  

Subdirectories are organized according to the figures presented in the paper.  

Subdirectory names also indicates whether the calculation corresponds to a **single-point** run or a **NEB** (nudged elastic band) run, and includes a brief description for the focus of the figure and additional details such as:
- relative energies
- Number of NEB images  
- Force convergence thresholds  

For all runs, POSCAR, INCAR, KPOINTS, CONTCAR, OUTCAR (or OUTCAR.gz for larger files) are provided. For the convinience of the reader, for the single point runs relative energies are provided, and for the NEB runs the diffusion path movie.vasp (could be opened in VESTA) and neb.dat which contains the distance between images, the energy of each image, and the force along the band.

---

## Citations  

The following foundational methods and codes were used in this work:  

- Blöchl, P. E. *Projector augmented-wave method.* **Phys. Rev. B** 50, 17953–17979 (1994).  
- Kresse, G. & Hafner, J. *Ab initio molecular dynamics for liquid metals.* **Phys. Rev. B** 47, 558–561 (1993).  
- Kresse, G. & Furthmüller, J. *Efficiency of ab-initio total energy calculations for metals and semiconductors using a plane-wave basis set.* **Comput. Mater. Sci.** 6, 15–50 (1996).  
- Kresse, G. & Furthmüller, J. *Efficient iterative schemes for ab initio total-energy calculations using a plane-wave basis set.* **Phys. Rev. B** 54, 11169–11186 (1996).  
- Perdew, J. P., Burke, K. & Ernzerhof, M. *Generalized gradient approximation made simple.* **Phys. Rev. Lett.** 77, 3865–3868 (1996).  
- Grimme, S. *et al.* *A consistent and accurate ab initio parametrization of density functional dispersion correction (DFT-D) for the 94 elements H–Pu.* **J. Chem. Phys.** 132, 154104 (2010).  
- Henkelman, G., Uberuaga, B. P. & Jónsson, H. *A climbing image nudged elastic band method for finding saddle points and minimum energy paths.* **J. Chem. Phys.** 113, 9901–9904 (2000).  
