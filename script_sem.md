ILORA - Path analysis
================
Achyut K Banerjee
August 23, 2021

**Premise:** To do the path analysis for identifying variables’
influence on successful naturalization and invasion. This data is a
subset of the ILORA database version 1.0.

**Data availability:** The associated data is available in
\[C:/Users/Achyut/Desktop/web/ilora\]

*Install and load package*

``` r
library(lavaan)
library(semPlot)
```

*Read data and analyze the structure*

``` r
data_IN<-read.csv("C:/Users/Achyut/Desktop/web/ilora/data_sem.csv")#data for invasive and naturalized aliens (applicable for NA - Naturalized and casual aliens)#

#Build model relationship#
HS.model2.1 <- '
Status~GF+Seed+Height+Nat.range+Natu.range_scaled+Uses+MRT_scaled+Nat.con.new
MRT_scaled~Nat.range+Natu.range_scaled+Uses+Nat.con.new+GF+Seed+Height
Nat.range~GF+Seed+Height
Natu.range_scaled~GF+Seed+Height+Uses+Nat.range
Uses~Nat.range+Natu.range_scaled+Nat.con.new+GF+Seed+Height+MRT_scaled+LULC+Climate
Climate~GF+Seed+Height+Nat.range+Natu.range_scaled+MRT_scaled+Nat.con.new+Uses
LULC~GF+Seed+Height+Climate
Nat.con.new~GF+Seed+Height
'
#Fit the model#
fit2.1 <- sem(HS.model2.1, data=data_IN,ordered="Status")
fitMeasures(fit2.1, c("cfi","wrmr","rmsea"))
summary(fit2.1)
```

*Plot the path diagram*

``` r
pathdiagram<-semPaths(fit2.1,whatLabels="std", intercepts=FALSE, style="lisrel",
                      nCharNodes=0, 
                      nCharEdges=0,
                      curveAdjacent = TRUE,title=TRUE, layout="tree",curvePivot=TRUE)
```

**END**

**References**

  - \[The lavaan project\] (<https://www.lavaan.ugent.be/>)
  - \[Paper - Journal of Environmental Management\]
    (<https://doi.org/10.1016/j.jenvman.2021.113054>)
