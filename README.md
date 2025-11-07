# Alloy 709 Multiaxial Creep Simulation Dataset

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.16895991.svg)](https://doi.org/10.5281/zenodo.16895991)


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

## Curated Rupture Summary

The file **`tr_results_2.xlsx`** provides a **curated rupture-summary** of 80 selected simulations that correspond directly to the multiaxial creep-rupture data reported in **Appendix B** of the manuscript:

*“Development of Predictive Model for Accurate Rupture Time from Multiaxial Creep in Alloy 709 with Physics-Based Simulations.”*

Each row lists the stress-state type, temperature, principal stresses (σ₁, σ₂, σ₃ in MPa), and the time-to-rupture (*tr*, in hours), where *tr* is extracted from the final simulation time step and converted from seconds to hours.

> **Note:** In the manuscript Appendix, the biaxial and triaxial stress values are presented in rounded engineering form for clarity (e.g., 171.2 MPa, 32.0 MPa, 8.0 MPa).  
> The `tr_results_2.xlsx` summary table and all `out.csv` raw time-series files in this dataset retain the **full floating-point precision** from the CPFE simulations.

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

## Column Definitions

### `tr_results_2.xlsx`
| Column | Unit | Meaning |
|---|---|---|
| `case` | – | Simulation case identifier (e.g., `12_c_ppn`) |
| `T_C` | °C | Test temperature |
| `sigma_1`, `sigma_2`, `sigma_3` | MPa | Principal stresses |
| `tr` | h | Time to rupture |

### `out.csv` (Raw Time Series)
May include variables such as:
- `time` (s) → simulation time  
- `D` (–) → grain-boundary damage (approaches 1 at rupture)  
- `avgcreep_xx, yy, zz` → creep strain components  
- `avgstress_xx, yy, zz` (MPa) → stress tensor components  
- `sigma_h_max/min` (MPa) → hydrostatic stress extrema  
- `sigma_vm_max/min` (MPa) → von Mises stress extrema  
- `strain_rate_*` (1/s) → instantaneous creep strain rate

---

## 6) Quick Start

### Python (pandas)

```python
import pandas as pd

# **Cases 1–4** → Uniaxial  
# **Cases 5–10** → Biaxial  
# **Cases ≥ 11** → Triaxial 

# Set temperature (°C) and case number (1–19)
T = 900
case_num = 12

# Select suffix based on stress state:
# ""        → tensile (uniaxial / biaxial / triaxial, where available)
# "_c"      → compression-dominant triaxial (pnn)
# "_c_ppn"  → mixed triaxial (ppn)
# "_c_pnp"  → mixed triaxial (pnp)
suffix = "_c_ppn"   # <-- change based on case mode

# Construct folder path (after extracting A709_data.zip)
case_folder = f"A709_data/{T}/{T}-{case_num}{suffix}"

# Load raw time-series data
raw = pd.read_csv(f"{case_folder}/out.csv")

# Convert time to hours
raw["time_hr"] = raw["time"] / 3600.0

# Example plot: damage vs time
raw.plot(
    x="time_hr",
    y="D",
    logy=True,
    xlabel="Time (hours)",
    ylabel="Damage D",
    title=f"Damage evolution: case {T}-{case_num}{suffix}"
)
```

---

## License

This dataset is distributed under the **Creative Commons Attribution 4.0 International (CC BY 4.0)** License.  
You are free to share and adapt the material with appropriate credit.  
[View the full license text](https://creativecommons.org/licenses/by/4.0/)

---

## Citation

If you use this dataset, please cite:

Baweja, S. (2025). *Multiaxial Simulation Data* [Data set]. Zenodo.  
https://doi.org/10.5281/zenodo.16895991
