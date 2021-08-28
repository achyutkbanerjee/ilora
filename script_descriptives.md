ILORA - Descriptive statistics
================
Achyut K Banerjee
August 22, 2021

**Premise:** To compare minimum residence time (MRT) between different
invasion categories. This data is a subset of the ILORA database version
1.0.

**Data availability:** The associated data is available in
\[C:/Users/Achyut/Desktop/web/ilora\]

*Install and load package*

``` r
library(dplyr)
library("ggpubr")
library(car)
```

*Read and format data*

``` r
data <- read.csv("C:/Users/Achyut/Desktop/web/ilora/data_descrip.csv")
data$group<-as.factor(data$group)
levels(data$group)
```

*Descriptives*

``` r
group_by(data, group) %>%
  summarise(
    mean = mean(mrt, na.rm = TRUE),
    sd = sd(mrt, na.rm = TRUE)
  )
```

*Data visualization*

``` r
ggboxplot(data, x = "group", y = "mrt", 
          color = "group", palette = c("#00AFBB", "#E7B800", "#FC4E07"),
          order = c("In", "Nt", "CA"),
          ylab = "mrt", xlab = "cat")
```

*Comparison between categories*

``` r
#ANOVA#
res.aov <- aov(mrt ~ group, data = data)
summary(res.aov)
#Tukey's HSD#
TukeyHSD(res.aov)

#Checking assumptions#

#Homogeneity of variance#
leveneTest(mrt ~ group, data = data)
#Normality#
plot(res.aov, 2)
#Shapiro-Wilk Test_for normality#
aov_residuals <- residuals(object = res.aov )
shapiro.test(x = aov_residuals )
#Non-parametric Kruskal Wallis test#
kruskal.test(mrt ~ group, data = data)
```

**END**

**References**

  - \[Paper - Journal of Environmental Management\]
    (<https://doi.org/10.1016/j.jenvman.2021.113054>)
