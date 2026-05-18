# Structural Analysis Pipeline for LRP8 $V_H/V_L$ Domains

This repository contains structural bioinformatics pipeline developed in Google Colab to analyze, modify, and evaluate the structural characteristics of Single-Chain Variable Fragments (scFvs) targeting **endothelial surface LRP8 receptor**. 

The workflow handles everything from structural ensemble alignment to post-translational modification (PTM) modeling, interactive 3D visualization, and quantitative structural biophysics metrics (SASA and residue proximity).

---

##  Features & Workflow

The pipeline is organized into five-step:

1. **Loading and RMSD-Based Selection:** Extracts AlphaFold-predicted models directly from a compressed ZIP archive, performs an all-to-all structural alignment using Biopython's `Superimposer`, and mathematically determines the most representative central model based on minimal root-mean-square deviation (RMSD).
2. **Post-Translational Modification (PTM) Modeling:** Utilizes `Gemmi` to programmatically mutate and model specific chemical modifications (such as **tryptophan oxidation** or **asparagine deamidation**) to assess structural stability and degradation risks.
3. **Interactive 3D Visualization:** Renders interactive, hardware-accelerated 3D representations of the native and modified variable domains ($V_H/V_L$) within the notebook using `py3Dmol`.
4. **Solvent Accessible Surface Area (SASA) Analysis:** Computes absolute and relative surface accessibility of target residues via `FreeSASA` to determine if susceptible patches are buried or solvent-exposed.
5. **Proximity Analysis:** Employs Biopython's `NeighborSearch` ($K\text{-d}$ tree) to map spatial contact networks and identify neighboring residues within a defined Angstrom ($\text{Å}$) radius of critical sites.

---

##  Data Outputs

The pipeline automates data extraction and saves analytical results directly into clean, structured tables for downstream processing:
* **`sasa_analysis_results.csv`**: Contains per-residue solvent accessibility calculations.
* **`proximity_analysis_results.csv`**: Maps localized spatial neighbors and atomic distances around key target sites.

---

##  Environment Setup & Dependencies

The notebook is optimized to dynamically bootstrap its own environment on Google Colab. The pipeline integrates the following stack:

### Core Core & Scientific Libraries
* `NumPy` & `Pandas` – High-performance matrix operations and data framing.
* `Matplotlib` & `Seaborn` – High-quality statistical data visualization.
* `openpyxl` – Export engine for tabular formatting.

### Structural Biology Engines
* **[Biopython (Bio.PDB)](https://biopython.org/)** – Structural parsing, hierarchical navigation (Structure/Model/Chain/Residue/Atom), coordinate superimposition, and spatial neighbor searching.
* **[Gemmi](https://gemmi.readthedocs.io/)** – Ultra-fast, macromolecular library used for precision structural manipulation and PTM editing.
* **[FreeSASA](https://freesasa.github.io/)** – Fast and exact analytical calculation of solvent-accessible surface areas.
* **[OpenMM](https://openmm.org/)** – Molecular mechanics simulation toolkit (environment infrastructure companion).
* **[Py3Dmol](https://3dmol.csb.pitt.edu/)** – Object-oriented, WebGL-based molecular visualization.

To run this locally or inspect the notebook dependencies, ensure you install:
```bash
pip install openmm py3Dmol gemmi freesasa biopython openpyxl
