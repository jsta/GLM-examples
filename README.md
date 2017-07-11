GLM examples
================

> Mirror of the GLM examples at: <http://aed.see.uwa.edu.au/research/models/GLM/Pages/set_up.html>

``` r
library(glmtools)
```

Warm Lake
---------

``` r
nml <- read_nml("release/warmlake/aed2/glm2.nml")
names(nml)
```

    ##  [1] "glm_setup"     "wq_setup"      "morphometry"   "time"         
    ##  [5] "output"        "init_profiles" "meteorology"   "bird_model"   
    ##  [9] "inflow"        "outflow"
