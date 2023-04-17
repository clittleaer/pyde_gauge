# pyde_gauge
PYde gauge: Routines for processing and analyzing tide gauge sea level data, generally for comparison with model output

To start:
1. Run import_rlr_matlab.ipynb. Or use PSMSL_data and PSMSL_ids.csv files. 
2a. Run tg_processing. IB correction requires access to ERA-5 on NCAR RDS server.
2b. Or use the "pseudo_tg_locations.ipynb" notebook.
3. Run alt_processing and/or CESM LR/HR processing. 
4. Compare two datasets using the "comp_at_points.ipynb" notebook.

Capabilities -- available in some form

Tide Gauges:
1. Importing monthly tide gauges from PSMSL.
2. Filtering/Infilling/Sorting along coastlines.
3. IB “Correcting” (ERA-5 for now)
4. Removal of global mean from all tide gauges
5. Monthly processing; removing mean seasonal cycle.
6. Filtering problematic gauges (right now, using momlevel threshold of distance between tide gauge and altimetry/model)

Altimetry:
1. extraction of closest point (using momlevel)
2. removal of global mean
3. standard time series analysis techniques, as for TG's
4. pseudo TG code, to sample coastal points for gridded datasets

Datasets -- available in some form
 * TG (PSMSL)
 * Altimetry (MEASURES 1/6, global mean)
 * Global mean 93-(MEASURES)
 * CESM FOSI LR/HR: point and gridded, regrinding

<!-- Analysis example — just TG/ALT
Analysis from CESM HR/LR paper in prep (filtering)
Wavelets/power spectra/standard statistical analyses -->


Capabilities -- desired
1. Wrap and/or recode RLR script from PSMSL
2. Long-period tide “corrections”
3. Uncertainty in corrections (multiple datasets)
4. Correcting for “global mean” terms, including fingerprints (Using Fredrikse et al. 2021 Dataset) and VLM (using XXX)
5. Careful vetting of coastal locations where it makes sense to compare with models/altimetry. Ideally, these are locations right along the coastline and are not nestled back in and embayments or upriver.  Would you happen to have such a list already for US or global locations? Although there are probably a few clear TGs to avoid, sometimes it is not very clear. And you might want to avoid them for other reasons, e.g. VLM or gauge-related issues. My -- maybe idealistic -- vision is to have this be determined by the spatial coherence of TGs (which of course will be determined by the spatial/temporal scale you care about!).
6. Clustering/spatial averaging/coherence.
7. Time mean

Datasets -- desired
 * SEANOE dataset
 * TG (UHSLC): (I haven’t touched high frequency (sub-monthly) data in a while.)
 * TG NOAA
 * Altimetry (DUACS)
 * CESM coupled
 * MOM6
 * Generic CMIP6

For momlevel
 
* I agree that knowing the cell depth would be useful.  The analysis is fast, so one could simply repeat the analysis by passing an array of "deptho" to get the depth at the selected locations.
* The call from momlevel to Scikit could be adapted to return all of the nearest neighbor points within a threshold to compute a mean/variance.  A modest amount of work is needed, but it's not an intractable problem.
