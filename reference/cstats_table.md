# Clustering statistics for an increasing number of clusters

Cuts the clustering tree into `step`, `2 * step`, ..., `k` clusters and
computes, for each number of clusters, the statistics of
[`fpc::cluster.stats()`](https://rdrr.io/pkg/fpc/man/cluster.stats.html).
The average silhouette width can be plotted to help choosing the number
of clusters.

## Usage

``` r
cstats_table(dist, tree, k, step, graph_silhouette = TRUE, l)
```

## Source

Adapted from the `cstats.table()` function and the silhouette plot of
Anastasia Reusova's tutorial: Reusova A. (2018). *Hierarchical
Clustering on Categorical Data in R*. Towards Data Science.
<https://medium.com/@anastasia.reusova/hierarchical-clustering-on-categorical-data-in-r-a27e578f2995>.
Code: <https://github.com/khunreus/cluster-categorical>.

## Arguments

- dist:

  A dissimilarity object, e.g. `gower_dist` returned by
  [`assess_gower()`](https://lguillier.github.io/strainselect_package/reference/assess_gower.md).

- tree:

  An `hclust` object, e.g. `aggl.clust.c` returned by
  [`assess_gower()`](https://lguillier.github.io/strainselect_package/reference/assess_gower.md).

- k:

  Largest number of clusters to test. Must be a multiple of `step`.

- step:

  Increment between two numbers of clusters tested.

- graph_silhouette:

  If `TRUE` (default), the average silhouette width is plotted against
  the number of clusters.

- l:

  Deprecated, use `step` instead.

## Value

A data frame with one row per number of clusters tested (row names
`Test <number of clusters>`) and the columns `cluster.number`, `n`,
`within.cluster.ss`, `average.within`, `average.between`, `wb.ratio`,
`dunn2`, `avg.silwidth` (see
[`fpc::cluster.stats()`](https://rdrr.io/pkg/fpc/man/cluster.stats.html)),
followed by cluster size columns. Values are rounded to 2 decimals.

## See also

Other clustering method:
[`assess_gower()`](https://lguillier.github.io/strainselect_package/reference/assess_gower.md),
[`select_silhouette()`](https://lguillier.github.io/strainselect_package/reference/select_silhouette.md)

## Examples

``` r
datafile <- system.file("data_test.csv", package = "strainselect")
raw_data <- read.csv(datafile, sep = ";", header = TRUE)
prepared_data <- prepare_input(raw_data, col_select = c(7, 10, 13, 14, 17, 24),
                               id = 1, date = 17)
#> no duplicate ID
#> selected metadata: CONTEXTE, MATRICE1, REGION, SECTEUR, LIEUPVT, ANNEE
gower <- assess_gower(prepared_data, graph = FALSE)
stats <- cstats_table(dist = gower$gower_dist, tree = gower$aggl.clust.c,
                      k = 50, step = 10)
#> testing 10 clusters
#> testing 20 clusters
#> testing 30 clusters
#> testing 40 clusters
#> testing 50 clusters

stats[, c("cluster.number", "avg.silwidth")]
#>         cluster.number avg.silwidth
#> Test 10             10         0.29
#> Test 20             20         0.41
#> Test 30             30         0.39
#> Test 40             40         0.49
#> Test 50             50         0.48
```
