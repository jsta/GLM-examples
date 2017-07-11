GLM examples
================

> Mirror of the GLM examples at: <http://aed.see.uwa.edu.au/research/models/GLM/Pages/set_up.html>

``` r
library(glmtools)
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
(input_files <- c(glm_nml$meteorology$meteo_fl, glm_nml$inflow$inflow_fl, glm_nml$outflow$outflow_fl))
```

    ## [1] "met_hourly.csv"            "inflow_1.csv,inflow_2.csv"
    ## [3] "outflow.csv"

``` r
run_glm(sim_folder = "release/warmlake/aed2")
```
