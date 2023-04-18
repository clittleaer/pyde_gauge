# pyde_gauge
PYde gauge: Routines for processing and analyzing tide gauge sea level data, generally for comparison with model output

## Setting up
Clone this repo to your local directory, then create your own branch to work in:
```
git clone https://github.com/clittleaer/pyde_gauge.git
cd pyde_gauge
git checkout -b <nameofyourbranch>
```

To start:
1a. Run import_rlr_matlab.ipynb. 
1b. Or, just use provided PSMSL_data and PSMSL_ids.csv files. 
2a. Run tg_processing. IB correction requires access to ERA-5 on NCAR RDS server.
3. Run alt_processing and CESM HR processing. 
4. Compare two datasets using the "comp_at_points.ipynb" notebook.
5. Use the "pseudo_tg_locations.ipynb" notebook.
6. Run alt_processing and CESM HR processing, but use the pseudo_tg_inputs.

Beta version TG capabilities:
1. Importing monthly tide gauges from PSMSL.
2. IB “Correcting” (ERA-5 for now) if you have access to NCAR RDA data
3. Monthly processing; removing mean seasonal cycle.

Beta version altimetry:
1. extraction of closest point (using momlevel)
2. standard time series analysis techniques, as for TG's
3. pseudo TG code, to sample coastal points for gridded datasets

 * TG (PSMSL)
 * Altimetry (MEASURES 1/6, global mean)
 * CESM FOSI HR: point and 
 
 
Additional capabilities to be introduced soon -- I have available in some form

Tide Gauges:
1. Filtering/Infilling/Sorting along coastlines.
2. Removal of global mean from all tide gauges
3. Filtering problematic gauges (right now, using momlevel threshold of distance between tide gauge and altimetry/model)
 * Global mean 93-(MEASURES)

CESM and altimetry
gridded, regridding
CESM fosi, multiple cycles, LR and HR, and coupled simulations.

<!-- Analysis example — just TG/ALT
Analysis from CESM HR/LR paper in prep (filtering)
Wavelets/power spectra/standard statistical analyses -->

Capabilities -- desired
1. Wrap and/or recode RLR script from PSMSL
2. Long-period tide “corrections”
3. Uncertainty in IB/GM corrections (multiple datasets)
4. Correcting for “global mean” terms, including fingerprints (Using Fredrikse et al. 2021 Dataset) and VLM (using XXX)
5. Careful vetting of coastal locations where it makes sense to compare with models/altimetry. Ideally, these are locations right along the coastline and are not nestled back in and embayments or upriver.  
* My -- maybe idealistic -- vision is to have this be determined by the spatial coherence of TGs (which of course will be determined by the spatial/temporal scale you care about!).
6. Clustering/spatial averaging/coherence.
7. Time mean

Datasets -- desired
 * SEANOE dataset
 * TG (UHSLC): (I haven’t touched high frequency (sub-monthly) data in a while.)
 * TG NOAA
 * Altimetry (DUACS)
 * MOM6
 * Generic CMIP6

For momlevel
 
* I agree that knowing the cell depth would be useful.  The analysis is fast, so one could simply repeat the analysis by passing an array of "deptho" to get the depth at the selected locations.
* The call from momlevel to Scikit could be adapted to return all of the nearest neighbor points within a threshold to compute a mean/variance.  A modest amount of work is needed, but it's not an intractable problem.
