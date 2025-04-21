---
title: "RNA-seq Part 1"
format: html
editor: visual
author: Sara Taloumis
execute:
  keep-md: true
---




## RNA-seq Part 1



::: {.cell}

```{.r .cell-code}
#install.packages("devtools")
library(devtools)
```

::: {.cell-output .cell-output-stderr}

```
Loading required package: usethis
```


:::
:::

::: {.cell}

```{.r .cell-code}
#devtools::install_github("danmaclean/rbioinfcookbook")
library(rbioinfcookbook)
```
:::

::: {.cell}

```{.r .cell-code}
#install.packages("forcats")

#if (!require("BiocManager", quietly = TRUE))
    #install.packages("BiocManager")

#BiocManager::install("edgeR")

#if (!require("BiocManager", quietly = TRUE))
    #install.packages("BiocManager")

#BiocManager::install("Biobase")

library(forcats)
library(edgeR)
```

::: {.cell-output .cell-output-stderr}

```
Loading required package: limma
```


:::
:::

::: {.cell}

```{.r .cell-code}
library(Biobase)
```

::: {.cell-output .cell-output-stderr}

```
Loading required package: BiocGenerics
```


:::

::: {.cell-output .cell-output-stderr}

```

Attaching package: 'BiocGenerics'
```


:::

::: {.cell-output .cell-output-stderr}

```
The following object is masked from 'package:limma':

    plotMA
```


:::

::: {.cell-output .cell-output-stderr}

```
The following objects are masked from 'package:stats':

    IQR, mad, sd, var, xtabs
```


:::

::: {.cell-output .cell-output-stderr}

```
The following objects are masked from 'package:base':

    anyDuplicated, aperm, append, as.data.frame, basename, cbind,
    colnames, dirname, do.call, duplicated, eval, evalq, Filter, Find,
    get, grep, grepl, intersect, is.unsorted, lapply, Map, mapply,
    match, mget, order, paste, pmax, pmax.int, pmin, pmin.int,
    Position, rank, rbind, Reduce, rownames, sapply, saveRDS, setdiff,
    table, tapply, union, unique, unsplit, which.max, which.min
```


:::

::: {.cell-output .cell-output-stderr}

```
Welcome to Bioconductor

    Vignettes contain introductory material; view with
    'browseVignettes()'. To cite Bioconductor, see
    'citation("Biobase")', and for packages 'citation("pkgname")'.
```


:::
:::

::: {.cell}

```{.r .cell-code}
genes <- count_dataframe[['gene']]
count_dataframe[['gene']] <- NULL
count_matrix <- as.matrix(count_dataframe)
rownames(count_matrix) <- genes
```
:::

::: {.cell}

```{.r .cell-code}
experiments_of_interest <- c("L1Larvae", "L2Larvae")
columns_of_interest <- which(pheno_data[['stage']] %in% experiments_of_interest)
```
:::

::: {.cell}

```{.r .cell-code}
grouping <- pheno_data[["stage"]] [columns_of_interest] |> forcats::as_factor()
```
:::

::: {.cell}

```{.r .cell-code}
#count_dge <- edgeR::DGEList(counts = counts_of_interest, group = grouping)
```
:::

::: {.cell}

```{.r .cell-code}
design <- model.matrix(~grouping)
#eset_dge <- edgeR::estimateDisp(count_dge, design)
#fit <- edgeR::glmQLFit(eset_dge, design)
#result <- edgeR::glmQLFTest(fit, coef=2)
#topTags(result)
```
:::



FBgn0027527- For the first gene, which is a protein coded gene that influences the phenotype in the fruit fly. It does tell us that there are some abnormal locomotor functions with this gene that can be fatal in the embryonic stage.

FBgn0037430- The expression of this gene is lethal late during the pupal stage and originates from the trichogen cell. This epidermal cell provides the phenotype for bristles or hair on the fly. This is a varying gene with either a very high or low expression rate. There were other recessive genes that were on the chart which were not physical but rather had a biological function. In this case, it told us it was a male.

FBgn0037424- This gene has a more biological process role which involves the function of the open tracheal system. There were no other phenotypes in this gene.

These genes all had different roles; they were listed from Osi20, Osi6, and Osi15. Some had more of a physical role than others but ultimately made up different parts of each fly which ultimately gives each fly its uniqueness. I thought it was cool that each block in the chart had a specific role in the fly's biological processes such as the development of the trachea, regulation of its body size, and eye development. Some of the data had a separate chart that showed different categories where each allele makes an impact. Such as biological development or membrane development.
