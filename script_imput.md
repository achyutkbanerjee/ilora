ILORA - Imputation of missing data
================
Achyut K Banerjee
August 22, 2021

**Premise:** To impute missing data of herbaceous species. Seed weight
and height have been standardized (see below) across different growth
forms. This data is a subset of the ILORA database version 1.0, and used
in the path analysis.

**Data availability:** The associated data is available in
\[C:/Users/Achyut/Desktop/web/ilora\]

*Install and load package*

``` r
install.packages("missForest")
library("missForest")
install.packages("mice")
library(mice)
```

*Read and format data*

``` r
data<-read.csv("C:/Users/Achyut/Desktop/web/ilora/data_herb_imput.csv")
md.pattern(data)
##visualization of missing data##
mice_plot <- aggr(data, col=c('navyblue','yellow'),
                  numbers=TRUE, sortVars=TRUE,
                  labels=names(data), cex.axis=.7,
                  gap=3, ylab=c("Missing data","Pattern"))
##imputation##
herb.imp <- missForest(data, verbose = TRUE, maxiter = 100,variablewise = TRUE,ntree = 20)
herb.imp$OOBerror
herb.imp$ximp
##write the imputed data##
write.csv(herb.imp$ximp,file = "herb_imp.csv")
```

**Premise\_2:** To standardize plant height across different growth
forms (applicable for seed weight also). This data is a subset of the
ILORA database version 1.0, and used in the path analysis.

**Data availability:** The associated data is available in
\[C:/Users/Achyut/Desktop/web/ilora\]

*Standardize plant height*

``` r
height<-read.csv("C:/Users/Achyut/Desktop/web/ilora/data_height_standard.csv")
height$herb_scaled<-scale(height$height_H)
height$shrub_scaled<-scale(height$height_S)
height$tree_scaled<-scale(height$height_T)
height$vine_scaled<-scale(height$height_V)
write.csv(height,"height_scaled.csv")
```

**END**

**References**

  - \[Paper - Journal of Environmental Management\]
    (<https://doi.org/10.1016/j.jenvman.2021.113054>)
