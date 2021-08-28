ILORA - Plotting number of landscape classes for invasion categories
================
Achyut K Banerjee
August 22, 2021

**Premise:** To show the number of classes (land use and land cover,
ecoregion, anthrome, habitat) occupied by species of five invasion
categories, a **bar plot with standard error** is made. This data is a
subset of the ILORA database version 1.0.

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
library(Rmisc)
```

*Read and format data*

``` r
data <- read.csv("C:/Users/Achyut/Desktop/web/ilora/data_lae.csv")
data <- data.frame(data)
tgc <- summarySE(data, measurevar="value", groupvars=c("occupancy","group"))
tgc
Species.category <- factor(tgc$group,level=c('Invasive', 'Naturalized', 
                                              'Casual','Native','Cryptogenic'))
```

*Plot data*

``` r
p<-
  ggplot(tgc, aes(y=value, x=occupancy,fill=Species.category)) + 
  coord_flip()+
  xlab('')+
  ylab('Number of classes occupied')+
  theme_light()+
  geom_bar(position="dodge", stat="identity",width=0.5,color="black")+
  geom_errorbar(aes(ymin=value-se, ymax=value+se),
                width=.2,position = position_dodge(0.5))+
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
tiff("species_laeh.tiff", units="in", width=5, height=5, res=300,compression = "none")
p<-
  ggplot(tgc, aes(y=value, x=occupancy,fill=Species.category)) + 
  coord_flip()+
  xlab('')+
  ylab('Number of classes occupied')+
  theme_light()+
  geom_bar(position="dodge", stat="identity",width=0.5,color="black")+
  geom_errorbar(aes(ymin=value-se, ymax=value+se),
                width=.2,position = position_dodge(0.5))+
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
