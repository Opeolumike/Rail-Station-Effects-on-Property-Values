# A Quasi-Experimental Evaluation of Rail Station Effects on Property Values in Devon

Evidence from the Okehampton and Marsh Barton station openings.

Code for the MSc dissertation of the same title (University of Exeter, 2026). The study tested whether the reopening of Okehampton station (November 2021) and the opening of Marsh Barton station (July 2023) changed nearby residential and commercial property values. It used a triple-difference hedonic design with ten control stations and wild cluster bootstrap inference, and found no statistically detectable capitalisation into property values following either station opening. The confidence interval remains compatible with both a small effect and no effect.

## Data

The data are on Zenodo: [10.5281/zenodo.24544649](https://doi.org/10.5281/zenodo.24544649). The files are restricted, so request access on the record. The record lists the terms of each source.

| Dataset | Source |
|---|---|
| Price Paid Data | HM Land Registry |
| UK House Price Index | Office for National Statistics and HM Land Registry |
| Energy Performance of Buildings Data | Ministry of Housing, Communities and Local Government |
| Non-domestic rating lists (2017 and 2023) | Valuation Office Agency |
| National Statistics Postcode Lookup | Office for National Statistics |
| Lower layer Super Output Area boundaries (2021) | Office for National Statistics |
| English Indices of Deprivation 2025 | Ministry of Housing, Communities and Local Government |
| NaPTAN | Department for Transport |
| Train schedules (CIF) | Network Rail |
| TIPLOC lookup | Vail Data |
| Pedestrian walk network | OpenStreetMap contributors |

## Reproducing the results

Run [`reproduce.ipynb`](reproduce.ipynb). It unzips the data into the repository, checks every file against `MANIFEST-SHA256.txt`, runs notebooks 01 to 06 in order and compares the new results with the originals.

- **Google Colab:** [open the notebook in Colab](https://colab.research.google.com/github/Opeolumike/Rail-Station-Effects-on-Property-Values/blob/main/reproduce.ipynb), put the five zips in a Google Drive folder named `zenodo_data`. If they are in a different Drive folder, type its name in the `DATA` box in step 1. Colab warns that the notebook was not written by Google, which it does for any notebook opened from GitHub. Click Run anyway, then allow access to Google Drive so step 1 can read the zips.
- **Own computer:**
  1. Create and activate a new Python environment, for example with conda: `conda create -n rail-repro -c conda-forge python=3.13`, then `conda activate rail-repro`. The verified run used Python 3.13.
  2. In that environment, install Jupyter, pandas and tqdm with pip:
     ```
     pip install jupyter pandas tqdm
     ```
     The notebooks install the other packages they need (geopandas, osmnx, statsmodels and so on) in their first cell with pip, so use pip here too rather than conda, to keep one installer.
  3. Clone the repository and put the five zips in a folder named `zenodo_data` inside it (ignored by git). If the zips are in another folder, set `DATA` in step 1 to its full path, with forward slashes, for example `C:/Users/me/zips`.
  4. Open `reproduce.ipynb` from the repository folder in Jupyter or VS Code, with the new environment as the kernel.

A full run takes some hours, mainly notebook 04.

## Notebooks

| Notebook | Purpose |
|---|---|
| `01_clean_tabular_data` | Cleans the Price Paid, House Price Index and rating list data for Devon |
| `02_spatial_bridge` | Matches sales to EPC records, geocodes properties and clips them to the station catchments |
| `03_geometric_foundation` | Joins properties to LSOAs and deprivation deciles |
| `04_network_analysis` | Snaps stations to the walk network, computes walking distances, isochrone bands and service frequency |
| `05_econometric_regression` | Estimates the triple-difference models with wild cluster bootstrap inference, robustness checks and figures |
| `06_final_layers` | Builds the map layers for the ArcGIS dashboard |

## Changes since submission

The tag `dissertation-submission` holds the notebooks exactly as submitted. Since then:

- Each notebook finds the repository folder instead of mounting Google Drive (cell 2).
- Notebook 04, cell 3: the OpenStreetMap download stays commented out, and the cell loads the walk network locked on 26 June 2026 instead.

No cells were added or removed, because the dissertation cites cells by number. The saved outputs are from the original 2026 run, so file paths printed in them show the original Google Drive location.

## Verified run

On 26 November 2026, a fresh Google Colab run of commit `59f2bf6` on the Zenodo files reproduced the regression results and sample sizes exactly. Versions: Python 3.13.18, pandas 2.2.3, numpy 2.4.6, statsmodels 0.15.0, scipy 1.16.3, geopandas 1.2.0, shapely 2.2.0, pyproj 3.8.0, fiona 1.10.1, pyarrow 23.0.1, fastparquet 2026.9.0, osmnx 2.2.0, networkx 3.7, matplotlib 3.10.0, contextily 1.7.1, tqdm 4.67.3.

Expected differences, all explained in step 4 of `reproduce.ipynb`:

- Two terms in the urban model (Treated x Near, Treated x Near x Post) cannot be estimated, so their z statistics are rounding noise.
- The attrition log keeps timestamped entries from earlier runs. Its walk network counts (37,362 nodes) come from an earlier download, while the locked network used for all routing has 37,221 nodes.

Notebook 04, cell 29 downloads rail lines live from OpenStreetMap for map layers only. It does not affect any result.

## Citation

Harvard (Cite Them Right):

Opeoluwa, M. (2026) *Code for: A Quasi-Experimental Evaluation of Rail Station Effects on Property Values in Devon* (Version 1.0.0) [Computer program]. Zenodo. Available at: https://doi.org/10.5281/zenodo.24549757

Opeoluwa, M. (2026) *Data for: A Quasi-Experimental Evaluation of Rail Station Effects on Property Values in Devon* (Version 1.0) [Dataset]. Zenodo. Available at: https://doi.org/10.5281/zenodo.24544649

"Cite this repository" on GitHub gives the code citation in APA and BibTeX (from `CITATION.cff`).

## Licence

Code: MIT (see `LICENSE`). Data: each source keeps its own terms, listed on the Zenodo record.
