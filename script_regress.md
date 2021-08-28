ILORA - Logistic regression
================
Achyut K Banerjee
August 22, 2021

**Premise:** To perform binary logistic regression considering the
variable ‘naturalized range size’ and testing their effects on invasion
success (invasive aliens-1, casual aliens-0). This data is a subset of
the ILORA database version 1.0.

**Data availability:** The associated data is available in
\[C:/Users/Achyut/Desktop/web/ilora\]

*Load data*

``` r
data <- read.csv("C:/Users/Achyut/Desktop/web/ilora/data_regress.csv")
data$group<-as.factor(data$group)
```

*Regress*

``` r
logistic_model <- glm(group ~ ., family = binomial("logit"), data, maxit = 100)
summary(logistic_model)
```

**END**

**References**

  - \[Paper - Journal of Environmental Management\]
    (<https://doi.org/10.1016/j.jenvman.2021.113054>)
