# Select the best clustered strain of each cluster

Cuts the strains into `k` clusters with
[`factoextra::hcut()`](https://rpkgs.datanovia.com/factoextra/reference/hcut.html)
and selects, in each cluster, the strain with the largest silhouette
width. When several strains share the largest silhouette width, one of
them is chosen at random.

## Usage

``` r
select_silhouette(
  prepared_data,
  dist,
  k,
  isdiss = inherits(dist, "dist"),
  hc_func = "hclust",
  hc_method = "complete",
  seed = NULL
)
```

## Arguments

- prepared_data:

  A data frame with one row per strain, as returned by
  [`prepare_input()`](https://lguillier.github.io/strainselect_package/reference/prepare_input.md).
  Its rows must be in the same order as in `dist`.

- dist:

  A dissimilarity object, e.g. `gower_dist` returned by
  [`assess_gower()`](https://lguillier.github.io/strainselect_package/reference/assess_gower.md).

- k:

  Number of clusters, i.e. number of strains to select. Must be between
  2 and the number of strains minus 1.

- isdiss:

  Logical, whether `dist` is a dissimilarity object (default: `TRUE`
  when `dist` inherits from `"dist"`).

- hc_func:

  Hierarchical clustering function passed to
  [`factoextra::hcut()`](https://rpkgs.datanovia.com/factoextra/reference/hcut.html):
  `"hclust"` (default), `"agnes"` or `"diana"`.

- hc_method:

  Agglomeration method passed to
  [`factoextra::hcut()`](https://rpkgs.datanovia.com/factoextra/reference/hcut.html),
  `"complete"` by default.

- seed:

  An integer passed to
  [`set.seed()`](https://rdrr.io/r/base/Random.html) to make the choice
  between ex aequo strains reproducible, or `NULL` (default) to leave
  the random number generator untouched.

## Value

`prepared_data` with three additional columns:

- cluster:

  the cluster of the strain;

- size:

  the number of strains in this cluster;

- selected:

  the identifier of the strain selected for this cluster.

The selected strains are given by `unique(result$selected)`.

## See also

Other clustering method:
[`assess_gower()`](https://lguillier.github.io/strainselect_package/reference/assess_gower.md),
[`cstats_table()`](https://lguillier.github.io/strainselect_package/reference/cstats_table.md)

## Examples

``` r
datafile <- system.file("data_test.csv", package = "strainselect")
raw_data <- read.csv(datafile, sep = ";", header = TRUE)
prepared_data <- prepare_input(raw_data, col_select = c(7, 10, 13, 14, 17, 24),
                               id = 1, date = 17)
#> no duplicate ID
#> selected metadata: CONTEXTE, MATRICE1, REGION, SECTEUR, LIEUPVT, ANNEE
gower <- assess_gower(prepared_data, graph = FALSE)
selection <- select_silhouette(prepared_data, dist = gower$gower_dist, k = 20,
                               seed = 1)
# the 20 strains to sequence
unique(selection$selected)
#>  [1] "2020LSAL00802" "2020LSAL00487" "2020LSAL00177" "2020LSAL00854"
#>  [5] "2020LSAL00454" "2020LSAL00720" "2020LSAL00506" "2020LSAL00550"
#>  [9] "2020LSAL00660" "2020LSAL00668" "2020LSAL00724" "2020LSAL00790"
#> [13] "2020LSAL00912" "2020LSAL00792" "2020LSAL00866" "2020LSAL00892"
#> [17] "2020LSAL01016" "2020LSAL00994" "2020LSAL01040" "2020LSAL01188"
```
