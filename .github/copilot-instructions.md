# GitHub Copilot / AI Agent Instructions — clinicOpt

Purpose: Help AI coding agents become immediately productive in this repository.

- Quick start:
  - Create the conda environment: `conda create -n clinicOpt python=3.12 -y` and `conda activate clinicOpt`.
  - Install deps: `pip install -r requirements.txt` (see `requirements.txt`).

- Project shape and big picture:
  - This repo is a notebooks-first proof-of-concept for mobile clinic site selection and scheduling.
  - Primary notebooks: `clinicOptENAUTILUS_step00.ipynb`, `clinicOptENAUTILUS_step01.ipynb`, `clinicOptENAUTILUS_step02.ipynb` (root).
  - Data inputs/outputs live in the `data/` folder (CSV files such as `events.csv`, `sites.csv`, `proposedSites.csv`, `proposedSitesProcessed.csv`). Notebooks read/write these CSVs directly.
  - Helper notebooks are in `tools/` (e.g., `normalizeData.ipynb`, `convert2distanceMat.ipynb`) — treat them as utilities rather than production modules.

- Important patterns and conventions (discoverable from code):
  - The meat of this proejct are the three files: `clinicOptENAUTILUS_step00.ipynb`, `clinicOptENAUTILUS_step01.ipynb`, and `clinicOptENAUTILUS_step02.ipynb`.  Run these three files in order to run the main analysis of the paper. 
  - `clinicOptENAUTILUS_step00.ipynb` is the data preprocessing notebook 
  - `clinicOptENAUTILUS_step01.ipynb` creates a Pareto front of solutions to the problem, which is required for the MCDM method E-NAUTILUS. This includes the definition of the optimization problem for DESDEO  
  - `clinicOptENAUTILUS_step02.ipynb` is the main e-nautilus code. It goes through three iterations of e-nautilus, and the DM can choose their choosen solution by editing the `final_chosen_solution` variable in the notebook. 



- Environment & run/debug guidance:
  - Use conda with Python 3.12 as noted in `readme.md`.
  - Install requirements from `requirements.txt` before running notebooks.
  - For quick checks, open the target notebook in VS Code or Jupyter and run top cells to validate data loads.

- Integration points and external dependencies:
  - No external services; dependencies are Python packages listed in `requirements.txt` (e.g., `pandas`, `polars`, `folium`, `PyQt6`, `openpyxl`).
  - Primary cross-component communication is via CSV files in `data/`.

- How AI agents should make edits:
  - Prefer small, focused changes with contained tests or cell demonstrations in a copy of the target notebook.
  - When changing data schema (column names/types), update every notebook that reads the affected CSV and mention the change in the PR description.
  - Do not convert the repo to a script-based architecture without explicit approval — it is notebooks-first by design.

- File references/examples to inspect when working:
  - Data preprocessing example: `clinicOptENAUTILUS_step00.ipynb` (attendance estimation and `proposedSitesProcessed.csv` output).
  - Utility notebooks: `tools/normalizeData.ipynb`, `tools/convert2distanceMat.ipynb`.
  - Repo guide: `readme.md` (environment setup).

- Deliverable & PR notes for contributors (and the agent):
  - Keep PRs small and explain: environment changes, changed CSV schemas, and notebooks touched.
  - If adding new Python packages, update `requirements.txt` and explain why.

If any section is unclear or you want more examples (e.g., common DataFrame shapes or specific cell refs), tell me which area to expand.
