---
title: "RNA-seq Part 2"
format: html
editor: visual
author: Sara Taloumis
execute:
  keep-md: true
---




## RNA-seq Part 2



::: {.cell}

```{.r .cell-code}
#if (!require("BiocManager", quietly = TRUE))
   # install.packages("BiocManager")

#BiocManager::install("ComplexHeatmap")
```
:::

::: {.cell}

```{.r .cell-code}
#install.packages("viridisLite")
#install.packages("stringr")
#install.packages("RColorBrewer")
#install.packages("circlize")
```
:::

::: {.cell}

```{.r .cell-code}
library(ComplexHeatmap)
```

::: {.cell-output .cell-output-stderr}

```
Loading required package: grid
```


:::

::: {.cell-output .cell-output-stderr}

```
========================================
ComplexHeatmap version 2.22.0
Bioconductor page: http://bioconductor.org/packages/ComplexHeatmap/
Github page: https://github.com/jokergoo/ComplexHeatmap
Documentation: http://jokergoo.github.io/ComplexHeatmap-reference

If you use it in published research, please cite either one:
- Gu, Z. Complex Heatmap Visualization. iMeta 2022.
- Gu, Z. Complex heatmaps reveal patterns and correlations in multidimensional 
    genomic data. Bioinformatics 2016.


The new InteractiveComplexHeatmap package can directly export static 
complex heatmaps into an interactive Shiny app with zero effort. Have a try!

This message can be suppressed by:
  suppressPackageStartupMessages(library(ComplexHeatmap))
========================================
```


:::
:::

::: {.cell}

```{.r .cell-code}
library(viridisLite)
library(stringr)
library(RColorBrewer)
library(circlize)
```

::: {.cell-output .cell-output-stderr}

```
========================================
circlize version 0.4.16
CRAN page: https://cran.r-project.org/package=circlize
Github page: https://github.com/jokergoo/circlize
Documentation: https://jokergoo.github.io/circlize_book/book/

If you use it in published research, please cite:
Gu, Z. circlize implements and enhances circular visualization
  in R. Bioinformatics 2014.

This message can be suppressed by:
  suppressPackageStartupMessages(library(circlize))
========================================
```


:::
:::

::: {.cell}

```{.r .cell-code}
library(rbioinfcookbook)
```
:::

::: {.cell}

```{.r .cell-code}
mat <- log(as.matrix(at_tf_gex[ , 5:55]))
ecotype <- stringr::str_split(colnames(mat), ",", simplify = TRUE)[,1]
part <- stringr::str_split(colnames(mat), ",", simplify = TRUE)[,2]
```
:::

::: {.cell}

```{.r .cell-code}
data_col_func <- circlize::colorRamp2(seq(0, max(mat), length.out = 6), viridisLite::magma(6))

ecotype_colors <- c(RColorBrewer::brewer.pal(12, "Set3"), RColorBrewer::brewer.pal(5, "Set1"))
names(ecotype_colors) <- unique(ecotype)

part_colors <- RColorBrewer::brewer.pal(3, "Accent")
names(part_colors) <- unique(part)
```
:::

::: {.cell}

```{.r .cell-code}
top_annot <- HeatmapAnnotation("Ecotype" = ecotype, "Plant Part" = part, col = list("Ecotype" = ecotype_colors, "Plant Part" = part_colors), annotation_name_side = "left")

side_annot <- rowAnnotation(length = anno_points(at_tf_gex$Length, pch = 16, size = unit(1, "mm"), axis_param = list(at = seq(1, max(at_tf_gex$Length), length.out = 4)),))
```
:::

::: {.cell}

```{.r .cell-code}
ht_1 <- Heatmap(mat, name="log(TPM)", row_km = 6, col = data_col_func, top_annotation = top_annot, right_annotation = side_annot, cluster_columns = TRUE, column_split = ecotype, show_column_names = FALSE, column_title = " ")

ComplexHeatmap::draw(ht_1)
```

::: {.cell-output-display}
![](RNA-seq-part-2_files/figure-html/unnamed-chunk-9-1.png){width=672}
:::
:::
