# LDEO-MEB Surface Ocean Multi-Driver Dataset (MEB_biomes)
This repository contains data and code for reproducing multi-drivers values for both the surface ocean carbonate system and temperature from forthcoming work from [LDEO-MEB](https://hurley.ldeo.columbia.edu/) lab group. These values are intended to help contextualize biology experiments that investigate ocean acidification and temperature change. Using data from five publicly available ESMs models, we provide mean monthly-resolution pre-industrial (1850s), modern (2000s), and future values (2090s) for all drivers. We divide the ocean up into 14 biomes to help constrain these data geospatially. Lastly, we compare these multi-driver values to both experiments in our lab group as well as the broader literature. 

All code here was written by [Henry Holm](https://github.com/hholm) and [Abby Shaum](https://github.com/AbbySh). If you have any questions or inquiries about these data, please do not hesitate to contact me at [hholm@ldeo.columbia.edu](mailto:hholm@ldeo.columbia.edu).

> **QUICK ACCESS - Mean Biome Values:** For those looking for the mean biome values featured in Holm *et al.* (both seasonal and annual) but not interested in reproducing the papers analysis/figures we have provided a [formatted excel file here.](https://github.com/hholm/MEB_biomes/raw/refs/heads/main/data/product_data_processed/Biome_Values_Holm_et_al.xlsx)

## Getting Started
Analysis and figures from Holm *et al.* can be reproduced in the following manner. ESM data was accessed and initially processed with Python. Final data processing and figure generation was performed in R and preserved in R markdown files. You will need a program that can run R code from markdown files such as R-Studio or similar IDE.

First, [clone this repository](https://docs.github.com/en/repositories/creating-and-managing-repositories/cloning-a-repository) to your computer using Git Bash, GitHub Desktop, or similar tool.

    git clone https://github.com
From here, if you are interested in reproducing the data analysis (biome means, literature comparison, lab data, ect) run R markdown files located in [**code/02_Biome_Calculations**](#code02_biome_calculations). However, the repository already contains all file outputs from these steps. Thus, if you are interested in quickly reproducing the figures associated with Holm et al. you can jump right to code found in [**code/03_Figure_Gen**](#code03_figure_gen).

## Reproducing Biome Values
The code for reproducing results of Holm *et al.* is divided up into three sections.

#### **code/01_LEAP_HPC_Code**
This folder contains Interactive Python Notebooks used to download relevant earth system model (ESM) data from the [LEAP Data Catalog](https://catalog.leap.columbia.edu/) on the LEAP Pangeo Server. While not reproducible locally, this code shows the process used for:

> 	 - **01_getting_ESM_output**: Initial access and re-gridding of ESM data
> 	 - **02_carbonate_system_calculation**: Full carbonate system calculation for all models using T, S, pH, and pCO2 
> 	 - **03_merge_ESMoutput_pyCO2sysoutput**: File merger with full carbonate system data.
> 	 - **04_decadal_means**: Subsetting data to monthly average over 3 select decades (1850s, 2000s, 2090s) and exporting.

The final output of this pipeline including 1x1 degree ocean maps can be found in **cmip6_drivers.zip** on Zenodo: [![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.22017672.svg)](https://doi.org/10.5281/zenodo.22017672).
#### **code/02_Biome_Calculations**

This folder contains code for re-calculation of biome average values (annual and seasonal) from CMIP6 data as well as comparison to OA-ICC (i.e. literature) values. If you do not wish to re-run this analysis all output files from these section are already contained in the repository.

> - **01_cmip6-biome-driver-calc** - This file downloads the re-gridded CMIP6 output and calculates biome means. The output of this are the following CSV's containing averages: `long_seas_biomes_values, wide_seas_biomes_values, wide_annual_biomes_values, long_annual_biomes_values`. Also produces some supplemental figures. 
> - **02_oa-icc-data-prep** - This file download OA-ICC data via their DOI's and produces a QC-ed merged file of all treatments used in said studies (`OA_ICC_data_merged`). Also produces some supplemental figures. 
> - **03_oa-icc-assign-biomes**- This file compares annual biome averages plus OA-ICC data to determine if treatments fall within ocean values and categorize them (`OA_ICC_data_final`). Also produces some supplemental figures. 

#### code/03_Figure_Gen

> - **01_maintext_figures_2_3** - Produces data Figures 2 and 3 from main text.
> - **02_maintext_figs_4_lab_calculations** - Calculates carbonate system in lab data, BATS data, and produces Figure 4 from the main text.
>
