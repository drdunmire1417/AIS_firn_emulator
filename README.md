# AIS_firn_emulator
data/code relating to paper titled: Future (2015-2100) ice-shelf firn air depletion from a statistical firn emulator

Here are the steps I took through this project with related code and output references. All code is stored here and output is stored on Zenodo at:............

**1) Run SNOWPACK model:**

The publicly available SNOWPACK model can be found at: https://github.com/snowpack-model/snowpack

**2) Read SNOWPACK output:**

In this step, I created pickle files for each site with condensed SNOWPACK output of necessary information (date, density, air content)

Code: read_SNOWPACK_output.ipynb

**3) Calculate FAC for each timestep at each site from SNOWPACK output:**

In this step, I used the pickle files from step 1) to create a netcdf with monthly FAC and CESM2 climate conditions (precipitation, 2m air temperature, 10m wind)

Code: SNOWPACK_FAC.ipynb

**4) Create firn emulator:**

In this step I use the netcdf files from step 2) to train and test a firn emulator for each of the thickness-permeability relationships (TP1, TP2, TP3).

Code: create_emulator.ipynb

**5) Get CMIP6 model output:**

Here I get precipitation, 2m air temperature, and 10m wind speed output from 32 CMIP6 models and create a netcdf file for each model/scenario (ssp1, ssp3, ssp5) with monthly output. I also have a script regrid all CMIP6 models to the ERA5 grid and combine them into a single netcdf file. This new consolidated netcdf file (sspX_allCMIP6.nc) contains yearly total precipitation (pr), average annual 10m windspeed (ws), average annual 2m air temperature (ta) and summer air temperature (ta_s) for each CMIP6 model.

Code: get_scenario_CMIP6.ipynb, combine_allCMIP6.ipynb

**6) Run emulator on ERA5 (historical) and CMIP6 (future) models:**

Here we use our emulator to predict FAC during the historical era using ERA5 and into the future for each CMIP6 model with each emission scenario (SSP1, SSP3, SSP5).

Code: run_emulator_historical.ipynb, run_emulator_future.ipynb

**7) Analysis:**

Here I include code used to calculate the average ice-shelf FAC and to make the manuscript figures
