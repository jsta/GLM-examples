GLM examples
================

> Mirror of the GLM examples at: <http://aed.see.uwa.edu.au/research/models/GLM/Pages/set_up.html>

``` r
library(glmtools)
library(tidyr)
library(dplyr)
library(ggplot2)
```

Warm Lake
---------

``` r
glm_nml <- read_nml("release/warmlake/aed2/glm2.nml")
aed_nml <- read_nml("release/warmlake/aed2/aed2.nml")

names(glm_nml)
```

    ##  [1] "glm_setup"     "wq_setup"      "morphometry"   "time"         
    ##  [5] "output"        "init_profiles" "meteorology"   "bird_model"   
    ##  [9] "inflow"        "outflow"

``` r
(input_files <- c(glm_nml$meteorology$meteo_fl, 
                  glm_nml$inflow$inflow_fl, 
                  glm_nml$outflow$outflow_fl))
```

    ## [1] "met_hourly.csv"            "inflow_1.csv,inflow_2.csv"
    ## [3] "outflow.csv"

``` r
(start_end <- glm_nml$time[c("start", "stop")])
```

    ## $start
    ## [1] "1997-01-02 00:00:00"
    ## 
    ## $stop
    ## [1] "2001-09-30 00:00:00"

``` r
run_glm(sim_folder = "release/warmlake/aed2")
```

``` r
lake_csv <- read.csv("release/warmlake/aed2/lake.csv", 
                     stringsAsFactors = FALSE)
lake_csv$time <- as.POSIXct(lake_csv$time)
lake_csv <- gather(lake_csv, variable, value, -time)
lake_csv <- filter(lake_csv, 
               variable %in% c("Tot.Inflow.Vol", "Tot.Outflow.Vol", 
                               "Rain", "Evaporation"))

gg <- ggplot(data = lake_csv) + 
  geom_line(aes(x = time, y = value, color = variable))
```

``` r
out_file <- "release/warmlake/aed2/output.nc"
```

``` r
sim_vars(out_file)
```

<script data-pagedtable-source type="application/json">
{"columns":[{"label":["name"],"name":[1],"type":["chr"],"align":["left"]},{"label":["unit"],"name":[2],"type":["chr"],"align":["left"]},{"label":["longname"],"name":[3],"type":["chr"],"align":["left"]}],"data":[{"1":"CAR_atm_ch4_exch","2":"mmol/m**2/d","3":"CH4 exchange across atm/water interface"},{"1":"CAR_atm_co2_exch","2":"mmol/m**2/d","3":"CO2 exchange across atm/water interface"},{"1":"CAR_ch4","2":"mmol/m**3","3":"methane"},{"1":"CAR_ch4ox","2":"mmol/m**3/d","3":"methane oxidation rate"},{"1":"CAR_dic","2":"mmol/m**3","3":"dissolved inorganic carbon"},{"1":"CAR_pCO2","2":"atm","3":"pCO2"},{"1":"CAR_pH","2":"-","3":"pH"},{"1":"CAR_sed_dic","2":"mmol/m**2/d","3":"CO2 exchange across sed/water interface"},{"1":"evap","2":"m/s","3":"evaporation"},{"1":"extc_coef","2":"unknown","3":"extc_coef"},{"1":"hice","2":"meters","3":"Height of Ice"},{"1":"hsnow","2":"meters","3":"Height of Snow"},{"1":"hwice","2":"meters","3":"Height of WhiteIce"},{"1":"I_0","2":"10E-6m","3":"Shortwave"},{"1":"NIT_amm","2":"mmol/m**3","3":"ammonium"},{"1":"NIT_denit","2":"mmol/m**3/d","3":"de-nitrification rate"},{"1":"NIT_nit","2":"mmol/m**3","3":"nitrate"},{"1":"NIT_nitrif","2":"mmol/m**3/d","3":"nitrification rate"},{"1":"NIT_sed_amm","2":"mmol/m**2/d","3":"ammonium sediment flux"},{"1":"NIT_sed_nit","2":"mmol/m**2/d","3":"nitrate sediment flux"},{"1":"NS","2":"","3":"Number of Layers"},{"1":"OGM_CDOM","2":"/m","3":"Chromophoric DOM (CDOM)"},{"1":"OGM_doc","2":"mmol/m**3","3":"dissolved organic carbon"},{"1":"OGM_don","2":"mmol/m**3","3":"dissolved organic nitrogen"},{"1":"OGM_dop","2":"mmol/m**3","3":"dissolved organic phosphorus"},{"1":"OGM_poc","2":"mmol/m**3","3":"particulate organic carbon"},{"1":"OGM_pon","2":"mmol/m**3","3":"particulate organic nitrogen"},{"1":"OGM_pop","2":"mmol/m**3","3":"particulate organic phosphorus"},{"1":"OXY_atm_oxy_exch","2":"mmol/m**2/d","3":"O2 exchange across atm/water interface"},{"1":"OXY_oxy","2":"mmol/m**3","3":"oxygen"},{"1":"OXY_sat","2":"%","3":"oxygen saturation"},{"1":"OXY_sed_oxy","2":"mmol/m**2/d","3":"O2 exchange across sed/water interface"},{"1":"PHS_frp","2":"mmol/m**3","3":"phosphorus"},{"1":"PHS_frp_ads","2":"mmol/m**3","3":"adsorbed phosphorus"},{"1":"PHS_sed_frp","2":"mmol/m**2/d","3":"PO4 exchange across sed/water interface"},{"1":"PHY_crypto","2":"mmol/m**3","3":"phytoplankton crypto"},{"1":"PHY_crypto_IN","2":"mmol/m**3","3":"phytoplankton crypto_IN"},{"1":"PHY_crypto_IP","2":"mmol/m**3","3":"phytoplankton crypto_IP"},{"1":"PHY_crypto_NtoP","2":"-","3":"internal n:p ratio"},{"1":"PHY_CUP","2":"mmol/m**3/d","3":"carbon uptake"},{"1":"PHY_diatom","2":"mmol/m**3","3":"phytoplankton diatom"},{"1":"PHY_diatom_IN","2":"mmol/m**3","3":"phytoplankton diatom_IN"},{"1":"PHY_diatom_IP","2":"mmol/m**3","3":"phytoplankton diatom_IP"},{"1":"PHY_diatom_NtoP","2":"-","3":"internal n:p ratio"},{"1":"PHY_GPP","2":"mmol/m**3/d","3":"gross primary production"},{"1":"PHY_green","2":"mmol/m**3","3":"phytoplankton green"},{"1":"PHY_green_IN","2":"mmol/m**3","3":"phytoplankton green_IN"},{"1":"PHY_green_IP","2":"mmol/m**3","3":"phytoplankton green_IP"},{"1":"PHY_green_NtoP","2":"-","3":"internal n:p ratio"},{"1":"PHY_IN","2":"mmol/m**3","3":"total phy nitrogen"},{"1":"PHY_IP","2":"mmol/m**3","3":"total phy phosphorus"},{"1":"PHY_NCP","2":"mmol/m**3/d","3":"net community production"},{"1":"PHY_NPR","2":"-","3":"phytoplankton p/r ratio (net)"},{"1":"PHY_NUP","2":"mmol/m**3/d","3":"nitrogen uptake"},{"1":"PHY_PAR","2":"W/m**2","3":"photosynthetically active radiation"},{"1":"PHY_PPR","2":"-","3":"phytoplankton p/r ratio (gross)"},{"1":"PHY_PUP","2":"mmol/m**3/d","3":"phosphorous uptake"},{"1":"PHY_TCHLA","2":"ug/L","3":"total chlorophyll-a"},{"1":"PHY_TPHYS","2":"mmol/m**3","3":"total phytoplankton"},{"1":"precip","2":"m/s","3":"precipitation"},{"1":"rad","2":"unknown","3":"solar radiation"},{"1":"rho","2":"unknown","3":"density"},{"1":"salt","2":"g/kg","3":"salinity"},{"1":"SDF_Fsed_amm","2":"mmol/m**2","3":"sedimentation rate of ammonia"},{"1":"SDF_Fsed_ch4","2":"mmol/m**2","3":"sedimentation rate of ch4"},{"1":"SDF_Fsed_dic","2":"mmol/m**2","3":"sedimentation rate of carbon"},{"1":"SDF_Fsed_doc","2":"mmol/m**2","3":"sedimentation rate of doc"},{"1":"SDF_Fsed_don","2":"mmol/m**2","3":"sedimentation rate of don"},{"1":"SDF_Fsed_dop","2":"mmol/m**2","3":"sedimentation rate of dop"},{"1":"SDF_Fsed_feii","2":"mmol/m**2","3":"sedimentation rate of iron"},{"1":"SDF_Fsed_frp","2":"mmol/m**2","3":"sedimentation rate of phosphorus"},{"1":"SDF_Fsed_nit","2":"mmol/m**2","3":"sedimentation rate of nitrate"},{"1":"SDF_Fsed_oxy","2":"mmol/m**2","3":"sedimentation rate of oxygen"},{"1":"SDF_Fsed_poc","2":"mmol/m**2","3":"sedimentation rate of poc"},{"1":"SDF_Fsed_pon","2":"mmol/m**2","3":"sedimentation rate of pon"},{"1":"SDF_Fsed_pop","2":"mmol/m**2","3":"sedimentation rate of pop"},{"1":"SDF_Fsed_rsi","2":"mmol/m**2","3":"sedimentation rate of silica"},{"1":"SIL_rsi","2":"mmol/m**3","3":"silica"},{"1":"SIL_sed_rsi","2":"mmol/m**2/d","3":"Si exchange across sed/water interface"},{"1":"temp","2":"celsius","3":"temperature"},{"1":"Tot_V","2":"m3","3":"lake volume"},{"1":"TRC_ret","2":"sec","3":"tracer"},{"1":"TRC_ss1","2":"mmol/m**3","3":"tracer"},{"1":"u_mean","2":"m/s","3":"mean velocity"},{"1":"u_orb","2":"m/s","3":"orbital velocity"},{"1":"V","2":"m3","3":"layer volume"},{"1":"wind","2":"m/s","3":"wind"},{"1":"ZOO_grz","2":"mmolC/m**3/d","3":"net zooplankton grazing"},{"1":"ZOO_mort","2":"mmolC/m**3/d","3":"net zooplankton mortality"},{"1":"ZOO_resp","2":"mmolC/m**3/d","3":"net zooplankton respiration"},{"1":"ZOO_zoo01","2":"mmolC/m**3","3":"zooplankton"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[3],"max":[3]},"pages":{}}}
  </script>

``` r
plot_var(out_file, "precip")
```

![](README_files/figure-markdown_github-ascii_identifiers/unnamed-chunk-7-1.png)

``` r
ggplot(data = filter(lake_csv, variable == "Rain")) + 
  geom_point(aes(x = time, y = value))
```

![](README_files/figure-markdown_github-ascii_identifiers/unnamed-chunk-7-2.png)
