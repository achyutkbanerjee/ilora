ILORA - Plotting market dynamics
================
Achyut K Banerjee
August 22, 2021

**Premise:** To show the average market price of native and alien (four
categories) in India (online nurseries), a **violin plot** is made. This
data is a subset of the ILORA database version 1.0.

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
data <- read.csv("C:/Users/Achyut/Desktop/web/ilora/data_md.csv")
data <- data.frame(
  x=data$name, 
  y=data$value)
```

*Plot data*

``` r
p <- data %>%
  mutate(x = fct_relevel(x, 
                            "Native", "Cryptogenic", "Casual", 
                            "Naturalized", "Invasive")) %>%
  ggplot( aes(x=x, y=y, fill=x, color=x)) +
  geom_violin(width=1.2, size=0.2, color="black") +
  scale_fill_viridis(discrete=TRUE) +
  scale_color_viridis(discrete=TRUE) +
  theme_light()+
  coord_flip() +
  xlab("Invasion categories") +
  ylab("Average market price (INR)")+
  theme(
    panel.grid.major.x = element_line(color = "gray"),
    panel.border = element_blank(),
    axis.ticks.y = element_blank(),
    legend.position = "None",
    axis.text = element_text(size = 8,color = "black"),
    axis.title = element_text(size = 10)
  )
p + scale_fill_manual(values = c("Invasive" = "coral",
                                 "Naturalized" = "deepskyblue",
                                 "Casual" = "blue",
                                 "Native" = "forestgreen",
                                 "Cryptogenic"="cornsilk"))
```

*Save plot*

``` r
tiff("market_dynamics.tiff", units="in", width=6.5, height=3.5, res=300,compression = "none")
p <- data %>%
  mutate(x = fct_relevel(x, 
                            "Native", "Cryptogenic", "Casual", 
                            "Naturalized", "Invasive")) %>%
  ggplot( aes(x=x, y=y, fill=x, color=x)) +
  geom_violin(width=1.2, size=0.2, color="black") +
  scale_fill_viridis(discrete=TRUE) +
  scale_color_viridis(discrete=TRUE) +
  theme_light()+
  coord_flip() +
  xlab("Invasion categories") +
  ylab("Average market price (INR)")+
  theme(
    panel.grid.major.x = element_line(color = "gray"),
    panel.border = element_blank(),
    axis.ticks.y = element_blank(),
    legend.position = "None",
    axis.text = element_text(size = 8,color = "black"),
    axis.title = element_text(size = 10)
  )
p + scale_fill_manual(values = c("Invasive" = "coral",
                                 "Naturalized" = "deepskyblue",
                                 "Casual" = "blue",
                                 "Native" = "forestgreen",
                                 "Cryptogenic"="cornsilk"))
dev.off()
```

**END**

**References**

  - \[R Graph Gallery\]
    (<https://www.r-graph-gallery.com/89-box-and-scatter-plot-with-ggplot2.html>)
  - \[Paper - bioRxiv preprint\]
    (<https://www.biorxiv.org/content/10.1101/2021.05.28.446252v1>)
