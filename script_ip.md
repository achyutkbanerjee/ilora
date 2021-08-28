ILORA - Plotting introduction pathway
================
Achyut K Banerjee
August 21, 2021

**Premise:** To show the number of alien species introduced from each
continent (S1-S8) by the different introduction pathways (IP) to India,
a **chord diagram** is made. This data is a subset of the ILORA database
version 1.0.

**Data availability:** The associated data is available in
\[C:/Users/Achyut/Desktop/web/ilora\]

*Install and load package*

``` r
install.packages("circlize")  
library(circlize)
```

*Read and format data*

``` r
data<-read.csv("C:/Users/Achyut/Desktop/web/ilora/data_ip.csv",header = TRUE,
               na.strings = "",sep = ",",row.names = 1)  
data  
class(data)  
data1<-as.matrix(data)  
data1
```

*Define colours*

``` r
grid.col = c(S1 = "red", S2 = "green", 
             S3 = "blue", S4="cyan", S5="darkblue", S6="gold",
             S7="brown",S8="blueviolet",  
             IP1.2="grey",IP1.5="grey",
             IP1.6="grey",IP1.7="grey",IP2.1="grey",  
             IP2.others="grey",IP2.9="grey",
             IP3.4.5="grey")
```

*Make the diagram*

``` r
chordDiagram(data1, grid.col = grid.col)
```

**Alternative approach**

``` r
df = data.frame(from = rep(rownames(data1), times = ncol(data1)),
                to = rep(colnames(data1), each = nrow(data1)),
                value = as.vector(data1),
                stringsAsFactors = FALSE)  
df  
chordDiagram(df,grid.col = grid.col,directional = 1, direction.type = c("diffHeight", "arrows"),link.arr.type = "big.arrow",big.gap = 20)
```

**Changing legend style**

``` r
chordDiagram(df, grid.col = grid.col, directional = 1,
direction.type = c("diffHeight", "arrows"),
link.arr.type = "big.arrow",big.gap = 20,
annotationTrack = "grid",
preAllocateTracks = list(track.height = max(strwidth(unlist(dimnames(df))))))  

circos.track(track.index = 1, panel.fun = function(x, y) {  
  xlim = get.cell.meta.data("xlim")  
  xplot = get.cell.meta.data("xplot")  
  ylim = get.cell.meta.data("ylim")  
  sector.name = get.cell.meta.data("sector.index")  
  
  if(abs(xplot[2] - xplot[1]) < 10) {  
    circos.text(mean(xlim), ylim[1], sector.name, facing = "clockwise",  
                niceFacing = TRUE, adj = c(0, 0.5), col = "blue")  
  } else {  
    circos.text(mean(xlim), ylim[1], sector.name, facing = "inside",   
                niceFacing = TRUE, adj = c(0.5, 0), col= "blue")  
  }  
}, bg.border = NA)
```

**Saving the image as .tiff in desired resolution**

``` r
tiff("introduction.tiff", units="in", width=5, height=5, res=300)  

chordDiagram(df, grid.col = grid.col, directional = 1, direction.type = c("diffHeight", "arrows"),link.arr.type = "big.arrow",big.gap = 20, annotationTrack = "grid", preAllocateTracks = list(track.height = max(strwidth(unlist(dimnames(df))))))  

circos.track(track.index = 1, panel.fun = function(x, y) {  
  xlim = get.cell.meta.data("xlim")  
  xplot = get.cell.meta.data("xplot")  
  ylim = get.cell.meta.data("ylim")  
  sector.name = get.cell.meta.data("sector.index")  
  
  if(abs(xplot[2] - xplot[1]) < 10) {  
    circos.text(mean(xlim), ylim[1], sector.name, facing = "clockwise",  
                niceFacing = TRUE, adj = c(0, 0.5), col = "blue")  
  } else {  
    circos.text(mean(xlim), ylim[1], sector.name, facing = "inside",   
                niceFacing = TRUE, adj = c(0.5, 0), col= "blue")  
  }  
}, bg.border = NA) 

dev.off()
```

**END**

**References**

  - \[Circular visualization in R\]
    (<https://jokergoo.github.io/circlize_book/book/>)
  - \[Paper - bioRxiv preprint\]
    (<https://www.biorxiv.org/content/10.1101/2021.05.28.446252v1>)
