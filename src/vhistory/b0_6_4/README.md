# Statistical analysis of interaction between temperature and enrichment in lake and stream fish communities

## Installation

The necessary R packages are:

* Rcpp 
* mvtnorm

## Structure of repository

* `cpp`: Folder containing an RCpp implementation of the differential-evolution Monte-Carlo sampler (DEMC).
* `data`: Folder containing the data used for the analysis.
* `f_HBM_v0_7.r`: File containing function definitions to analyse the chains generated by the DEMC sampler.
* `m1_con_load.r`: File containing the definition and formatting of variables and model for the analysis of the connectance.
* `m1_mTL_load.r`: File containing the definition and formatting of variables and model for the analysis of the maximum trophic level.
* `m2_demc_resume.r`: Script to resume the DEMC sampling from a pre-existing chain.
* `m2_demc.r`: Script to perform the DEMC sampling.  
* `m3_plot_robustness.r`: Script to generate the figures and model diagnostics for the prior robustness analysis.
* `m3_plot.r`: Script to generate the figures and model diagnostics.
* `m5_further_checks.r`: Script to perform further model and data checks (e.g. number of repeated sampling at a given site).
* `out_combined`: Folder containing figures that combine results from the connectance and maximum trophic level models.
* `out_combined_robustness`: Folder containing figures that combine results from the connectance and maximum trophic level models for the prior robustness analysis.
* `out_con`: Folder containing figures of results of the connectance model.
* `out_con_robustness`: Folder containing figures of results of the connectance model for the prior robustness analysis.
* `out_mTL`: Folder containing figures of results of the maximum trophic level model.
* `out_mTL_robustness`: Folder containing figures of results of the maximum trophic level model for the prior robustness analysis.

## Running the scripts

### 1. Run the DEMC sampler to estimate the posterior distribution. 

Prior to running the script `m2_demc.r`, make sure that the script loads the correct model by availing the relevant line of code in the script, e.g. for loading the connectance model:

```R 
source("m1_con_load.r")
``` 

Also make sure to change the name of the output file in the script if multiple chains are run, e.g. for saving the second chain use:

```R 
chainName = "chain_thinned_2"
``` 

The sampling can then be performed by running the command:

```Bash
Rscript m2_demc.r
```

Resulting chains will be stored in a folder specific to a give model, either connectance or maximum trophic level.

### 2. Generate results and figures.

This can be done by running the plotting scripts:

```Bash
Rscript m3_plot.r
```

Make sure that the right model is selected following the same procedure as described for the sampler. Resulting figures will be produced in the folder of the corresponding model.

Plots that combine results from both models can be generated by running:

```Bash
Rscript m4_plot_combined.r
```

For these scripts, no need to specify which model should be used as both are used.

### 3. Robustness to prior specifications

The analysis that assesses the robustness to prior specifications can be run in the same way as described before, expect that the script `m2_demc_resume.r`, `m3_plot_robustness.r`, and `m3_plot_combined_robustness.r` should be used in place of the scripts `m2_demc.r`, `m3_plot.r`, and `m3_plot_combined.r`.