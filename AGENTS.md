
## Terms

| Acronym | Definition                        |
| ------- | --------------------------------- |
| RPM     | Reference Point Method            |
| PF      | Pareto Front                      |
| MHC     | Mobile Healthwise Clinic          |
| SVI     | Social Vulnerability Index        |
| DM      | Decision Maker                    |

## Methods

Three methods are implemented, each building on the last in terms of DM interaction:

| Method     | Notebook                              | DM Interaction         | Objectives |
| ---------- | ------------------------------------- | ---------------------- | ---------- |
| NSGA-III   | `methods/NSGAIII/clinicOptNSGAIII.ipynb` | None (inspect PF manually) | 3 |
| RPM        | `methods/RPM/clinicOptRPM.ipynb`      | Provide reference point | 4          |
| E-NAUTILUS | `methods/ENAUTILUS/s3_ENAUTILUS.ipynb` | Iterative (3 rounds)  | 5          |

### Objectives

| Symbol | Description                                   | Direction | NSGA-III | RPM | E-NAUTILUS |
| ------ | --------------------------------------------- | --------- | :------: | :-: | :--------: |
| f_1    | Total patients served                         | Maximize  | x        | x   | x          |
| f_2    | Number of under-attended/overstaffed events   | Minimize  | x        | x   | x          |
| f_3    | Total costs (gas + driver pay)                | Minimize  | x        | x   | x          |
| f_4    | % of regional population with clinic access   | Maximize  |          | x   | x          |
| f_5    | Cumulative SVI of covered population          | Maximize  |          |     | x          |

## Files

### ENAUTILUS pipeline (run in order)
- `methods/ENAUTILUS/s1_estimateAttendance.ipynb`: Estimates expected attendance for proposed sites
- `methods/ENAUTILUS/s2_probDefAndRPM.ipynb`: Defines the DESDEO problem and generates a PF using RPM; saves result as a `.pkl` file
- `methods/ENAUTILUS/s3_ENAUTILUS.ipynb`: Loads the saved PF and runs E-NAUTILUS interactively; DM selects preferred solutions over multiple rounds

### Standalone methods
- `methods/NSGAIII/clinicOptNSGAIII.ipynb`: Standalone NSGA-III run; produces full PF for manual inspection
- `methods/RPM/clinicOptRPM.ipynb`: Standalone RPM run; DM provides a reference point and receives nearby solutions; results shown on a Folium map

### Tools / exploratory
- `tools/attendancePlayground.ipynb`
- `tools/convert2distanceMat.ipynb`
- `tools/normalizeData.ipynb`
- `tools/schedulePlayground.ipynb`

## Data

```
data/
├── MHC Trip Summary.xlsx           # Primary source of truth for historical site visits
├── proposedSites.csv               # Sites the clinic is considering visiting
├── proposedSitesProcessed.csv      # proposedSites.csv + estimated attendance (DO NOT EDIT)
├── sites.csv                       # Comprehensive list of visited/candidate sites
├── events.csv                      # Historical record of past site visits
├── cities.csv                      # City list with lat/long and population
├── city_distances.csv              # Raw pairwise city distance/duration data
├── adjacencyMatrixDist.csv         # Adjacency matrix: distances in miles
├── adjacencyMatrixTravelTime.csv   # Adjacency matrix: travel time in minutes
└── pf_*.pkl                        # Cached Pareto fronts from RPM runs
```

### File descriptions

- `MHC Trip Summary.xlsx`: Excel source data compiled into `sites.csv` and `events.csv`
- `proposedSites.csv`: Sites under consideration; may or may not have been visited before
- `proposedSitesProcessed.csv`: Output of attendance estimation preprocessing — do not edit manually
- `sites.csv`: All sites visited or under consideration
- `events.csv`: Historical record of each instance a site was visited (consider renaming to `visits.csv`)
- `cities.csv`: Cities in the service region
- `city_distances.csv`: Raw input used to build the two adjacency matrices
- `adjacencyMatrixDist.csv`: City-to-city driving distances (miles); used for cost calculations
- `adjacencyMatrixTravelTime.csv`: City-to-city travel times (minutes); used for food desert coverage constraint
- `pf_*.pkl`: Serialized Pareto front outputs from RPM, used as input to E-NAUTILUS

## Framework

All methods use [DESDEO](https://desdeo.readthedocs.io/) for problem definition and solving. Problems are defined using `Problem`, `Objective`, `Variable`/`TensorVariable`, `Constant`/`TensorConstant`, and `Constraint` objects. Results are visualized with Matplotlib (NSGA-III) and Folium interactive maps (RPM, E-NAUTILUS).
