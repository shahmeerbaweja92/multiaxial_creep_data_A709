# Alloy 709 Multiaxial Creep Simulation Dataset

This dataset contains multiaxial creep simulation results for Alloy 709 generated with a crystal-plasticity finite-element (CPFE) framework. The raw data comprise time-series outputs (`out.csv`) from approximately 172 simulations at **600, 700, 800, and 900 °C**. Each `out.csv` records creep–damage evolution, including creep strains and strain rates, stresses, the damage parameter `D`, and derived quantities (e.g., hydrostatic and von Mises stresses).

Directories are organized by temperature and case number (e.g., `600/600-7/out.csv`, `700/700-3/out.csv`).  
The case numbering corresponds to stress-state type:

- **Cases 1–4** → Uniaxial  
- **Cases 5–10** → Biaxial  
- **Cases ≥ 11** → Triaxial  

---

## Suffix Definitions

Suffixes in subfolder names further specify the stress mode:

- `_c` → Biaxial/Triaxial compression (pn/pnn)  
- `_c_ppn` → Mixed compressive–tensile triaxial (ppn)  
- `_c_pnp` → Mixed compressive–tensile triaxial (pnp)  
- *(no suffix)* → Tensile states  

---

## Processed Summary

A processed summary for 80 curated cases, **`tr_results_2.xlsx`**, provides the tabulated multiaxial creep rupture data (time to rupture, *tr*, in hours) corresponding to Appendix A of the manuscript  
*“Development of Predictive Model for Accurate Rupture Time from Multiaxial Creep in Alloy 709 with Physics-Based Simulations.”*  

Each row lists stress-state type, temperature, principal stresses (σ₁, σ₂, σ₃ in MPa), and *tr*.  
(Biaxial appendix entries are presented as rounded engineering values; raw `out.csv` files retain full precision.)

---

## Reuse and Applications

These data support reproduction of the paper’s tables and figures and can be reused for:

- Benchmarking effective-stress models  
- Validating invariant-based rupture-life predictions  
- Developing machine-learning surrogates for multiaxial creep  

---

## File Inventory

- `/600/.../out.csv` → Raw creep time series at 600 °C  
- `/700/.../out.csv` → Raw creep time series at 700 °C  
- `/800/.../out.csv` → Raw creep time series at 800 °C  
- `/900/.../out.csv` → Raw creep time series at 900 °C  
- `tr_results_2.xlsx` → Processed summary (80 rows; matches tabulated data in the Appendix)  
- `README.md` → Dataset description, structure, and column definitions  

---

## License

This dataset is distributed under the **Creative Commons Attribution 4.0 International (CC BY 4.0)** License.  
You are free to share and adapt the material with appropriate credit.  
[View the full license text](https://creativecommons.org/licenses/by/4.0/)
