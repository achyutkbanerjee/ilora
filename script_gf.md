ILORA - Plotting growth forms for invasion categories
================
Achyut K Banerjee
August 22, 2021

**Premise:** To show the number of species of four growth forms across
five invasion categories, a **bar plot** is made. This data is a subset
of the ILORA database version 1.0.

**Data availability:** The associated data is available in
\[C:/Users/Achyut/Desktop/web/ilora\]

*Install and load package*

``` r
library(ggplot2)
library(dplyr)
library(tidyr)
library(forcats)
library(hrbrthemes)
library(viridis)
```

*Read and format data*

``` r
data<-read.csv("C:/Users/Achyut/Desktop/web/ilora/data_scgf.csv")
data<-data.frame(data)
Species.category <- factor(data$group,level=c('Invasive', 'Naturalized', 
                                         'Casual','Native','Cryptogenic'))
```

*Plot data*

``` r
p<-ggplot(data, aes(y=value, x=individual,fill=Species.category)) + 
  coord_flip()+
  xlab('Growth forms')+
  ylab('Number of species')+
  theme_light()+
  geom_bar(position="dodge", stat="identity",width=0.5,color="black")+
  theme(
    panel.grid.major.y = element_blank(),
    panel.border = element_blank(),
    axis.ticks.y = element_blank(),
    axis.text = element_text(size = 12,color = "black"),
    axis.title = element_text(size = 15)
  )
p
p + scale_fill_manual(values = c("Invasive" = "coral",
                                 "Naturalized" = "deepskyblue",
                                 "Casual" = "blue",
                                 "Native" = "forestgreen",
                                 "Cryptogenic"="cornsilk"))
```

*Save plot*

``` r
tiff("growth_forms.tiff", units="in", width=5, height=5, res=300,compression = "none")
p<-ggplot(data, aes(y=value, x=individual,fill=Species.category)) + 
  coord_flip()+
  xlab('Growth forms')+
  ylab('Number of species')+
  theme_light()+
  geom_bar(position="dodge", stat="identity",width=0.5,color="black")+
  theme(
    panel.grid.major.y = element_blank(),
    panel.border = element_blank(),
    axis.ticks.y = element_blank(),
    axis.text = element_text(size = 12,color = "black"),
    axis.title = element_text(size = 15)
  )
p
p + scale_fill_manual(values = c("Invasive" = "coral",
                                 "Naturalized" = "deepskyblue",
                                 "Casual" = "blue",
                                 "Native" = "forestgreen",
                                 "Cryptogenic"="cornsilk"))
dev.off()
```

**END**

**References**

  - \[R Graph Gallery\] (<https://www.r-graph-gallery.com/barplot.html>)
  - \[Paper - bioRxiv preprint\]
    (<https://www.biorxiv.org/content/10.1101/2021.05.28.446252v1>)
