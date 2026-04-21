
## Terms
RPM: Reference point method 
PF: Pareto front

| Acronym | Definition                |
| ------- | ------------------------- |
| RPM     | Reference Point Method    |
| PF      | Pareto Front              |


## Files

- `s0_estimateAttendance.ipynb` Calculates expected attendance for sites
- `s1_probDefAndRPM.ipynb`: Defines the problem and runs RPM to get its PF
- `s2_ENAUTILUS.ipynb`: Uses PF from previous step to run the E-NAUTILUS method 

## Data 
```
.
├── proposedSites.csv               # Input to preprocessing 
├── sites.csv                       # Input to preprocessing
├── adjacencyMatrixDist.csv         # Input to preprocessing
├── proposedSitesProcessed.csv      # Output of preprocessing (DO NOT EDIT!)
├── cities.csv                    
├── city_distances.csv
├── events.csv
├── MHC Trip Summary.xlsx           # Refernece source for sites.csv
└── adjacencyMatrixTravelTime.csv   # O
```


- `proposedSites.csv`: Sites that the clinic is interested in visiting. It may or may not have been visited.
- `sites.csv`: Comprehensive list of sites that have been visited or are under consideration. Compiled from `MHC Trip Summary.xlsx`
- `proposedSitesProcessed.csv`: Contains `proposedSites.csv` plus expected attendance. Expected attendance is either the median attendance from previous visits, or median historical attenance from sites of the same type
- `cities.csv`: List of cities
- `events.csv`: Historical record of past instances of sites being visited. Should I rename this visits perhaps? 
- `MHC Trip Summary.xlsx`: Main data source of the MHC events from the past
- `city_distances.csv`: Enumeration of each pairing of cities and their distance and duration. Raw input to the adjacency matrices
- `adjacencyMatrixDist.csv`: Adjacency matrix for the different cities in km 
- `adjacencyMatrixTravelTime.csv`: Adjacency matrix for the different cities in travel time 

