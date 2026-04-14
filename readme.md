# clinicOpt 

Proof of concept project for optimizing the site selection for a mobile clinic. 

## Prerequisites
- Anaconda or Miniconda installed: https://docs.conda.io/en/latest/miniconda.html

## Create the Anaconda environment 
```
conda create -n clinicOpt python=3.12 -y
conda activate clinicOpt
```

If `pip` is not available in the environment, install it:

```
conda install pip -y
```

## Install DESDEO 
Follow the install directions for DESDEO found [here](https://desdeo.readthedocs.io/en/latest/howtoguides/installing/) to install DESDEO in your Anaconda environment. I've successfully used this exact [version  of DESDEO](https://github.com/industrial-optimization-group/DESDEO/tree/1ee72385720217c11daea82b056fede685fbc603).


## Install remaining Python dependencies

Install the project's dependencies from `requirements.txt`:
```
pip install -r requirements.txt
```

## Running the E-NAUTILUS code
Run E-NAUTILUS by running these three Jupyter Notebooks in order: 
- `clinicOptENAUTILUS_step00.ipynb` is the data preprocessing notebook 
- `clinicOptENAUTILUS_step01.ipynb` creates a Pareto front of solutions to the problem, which is required for the MCDM method E-NAUTILUS. This includes the definition of the optimization problem for DESDEO  
- `clinicOptENAUTILUS_step02.ipynb` is the main e-nautilus code. It goes through three iterations of e-nautilus, and the DM can choose their choosen solution by editing the `final_chosen_solution` variable in the notebook. 


