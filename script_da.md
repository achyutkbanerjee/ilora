ILORA - Plotting data availability
================
Achyut K Banerjee
August 22, 2021

**Premise:** To show the percentage data availability for each of the 13
variables, a **lollipop chart** is made. This data is a subset of the
ILORA database version 1.0.

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
data <- read.csv("C:/Users/Achyut/Desktop/web/ilora/data_da.csv")
data <- data.frame(
  x=data$Variable, 
  y=data$Availability
)
```

*Plot data*

``` r
p <- data %>%
  mutate(x = fct_relevel(x, 
                         "Sp.Categorization", "General.Information", "Native.Range", 
                         "Introduction","Economic.Uses", "Market.Dynamics","Habitat",
                         "Naturalized.Range","Occurrence","LULC",
                         "Anthromes","Ecoregions","Climate")) %>%
  ggplot(aes(x=x, y=y)) +
  xlab('Variable')+
  ylab('Data availability (%)')+
  geom_segment( aes(x=x, xend=x, y=0, yend=y), color="black") +
  geom_point( color="red", size=4, alpha=0.6) +
  theme_light() +
  coord_flip() +
  theme(
    panel.grid.major.y = element_blank(),
    panel.border = element_blank(),
    axis.ticks.y = element_blank(),
    axis.text = element_text(size = 12,color = "black"),
    axis.title = element_text(size = 15)
  )
p
```

*Save plot*

``` r
tiff("data_availability.tiff", units="in", width=5, height=5, res=300,compression = "none")
p <- data %>%
  mutate(x = fct_relevel(x, 
                         "Sp.Categorization", "General.Information", "Native.Range", 
                         "Introduction","Economic.Uses", "Market.Dynamics","Habitat",
                         "Naturalized.Range","Occurrence","LULC",
                         "Anthromes","Ecoregions","Climate")) %>%
  ggplot(aes(x=x, y=y)) +
  xlab('Variable')+
  ylab('Data availability (%)')+
  geom_segment( aes(x=x, xend=x, y=0, yend=y), color="black") +
  geom_point( color="red", size=4, alpha=0.6) +
  theme_light() +
  coord_flip() +
  theme(
    panel.grid.major.y = element_blank(),
    panel.border = element_blank(),
    axis.ticks.y = element_blank(),
    axis.text = element_text(size = 12,color = "black"),
    axis.title = element_text(size = 15)
  )
p
dev.off()
```

**END**

**References**

  - \[R Graph Gallery\]
    (<https://www.r-graph-gallery.com/300-basic-lollipop-plot.html>)
  - \[Paper - bioRxiv preprint\]
    (<https://www.biorxiv.org/content/10.1101/2021.05.28.446252v1>)
