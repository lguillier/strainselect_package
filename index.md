# strainselect

{strainselect} helps choosing which bacterial strains to sequence from a
collection described by metadata (sampling context, matrix, region,
sector, year…). It provides two methods:

- the **clustering method**, when the number of strains that can be
  sequenced is limited: strains are grouped into *k* clusters using the
  Gower distance and hierarchical clustering, and the best clustered
  strain of each cluster is selected, so that the selected strains are
  as different as possible;
- the **profile method**, when the number of strains to sequence is not
  limited: strains sharing exactly the same metadata are grouped, and
  one strain per group is selected, so that every distinct profile —
  including unique strains — is represented.

![image](https://user-images.githubusercontent.com/114993027/220967873-c8a4edaa-2d93-441c-b88e-7ec0a9bb674b.png)

image

## Documentation

📖 **Website: <https://lguillier.github.io/strainselect_package/>**

- [Get
  started](https://lguillier.github.io/strainselect_package/articles/get-started.html):
  both methods step by step;
- [Reference](https://lguillier.github.io/strainselect_package/reference/index.html):
  help pages of all functions.

## Installation

Install the development version from GitHub:

``` r

# install.packages("remotes")
remotes::install_github("lguillier/strainselect_package", build_vignettes = TRUE)
```

## Example

The package ships with an example table of 100 *Salmonella* strains
described by 24 variables. We base the selection on 6 of them and on the
year of sampling.

``` r

library(strainselect)

datafile <- system.file("data_test.csv", package = "strainselect")
raw_data <- read.csv(datafile, sep = ";")

prepared_data <- prepare_input(
  raw_data,
  col_select = c("CONTEXTE", "MATRICE1", "REGION", "SECTEUR", "LIEUPVT"),
  id = "IDENTIFIANT", date = "DATE_PRELEVEMENT", year = TRUE
)
#> no duplicate ID
#> selected metadata: CONTEXTE, MATRICE1, REGION, SECTEUR, LIEUPVT, ANNEE
head(prepared_data, 3)
#>                   CONTEXTE         MATRICE1               REGION
#> 2020LSAL00151 Surveillance     non spécifié Auvergne Rhone Alpes
#> 2020LSAL00152 Surveillance     non spécifié Auvergne Rhone Alpes
#> 2020LSAL00163 Surveillance Viande de canard   Nouvelle Aquitaine
#>                            SECTEUR                     LIEUPVT ANNEE
#> 2020LSAL00151          Eco-système     Source/captage de l'eau  2020
#> 2020LSAL00152          Eco-système     Source/captage de l'eau  2020
#> 2020LSAL00163 Alimentation humaine Transformation industrielle  2020
```

### Clustering method: a fixed number of strains

The average silhouette width helps choosing the number of clusters: look
for a maximum or a plateau.

``` r

gower <- assess_gower(prepared_data, graph = FALSE)
stats <- cstats_table(gower$gower_dist, gower$aggl.clust.c, k = 50, step = 5)
```

![](reference/figures/README-silhouette-1.png)

Then select one strain per cluster, here 20 strains:

``` r

selection <- select_silhouette(prepared_data, gower$gower_dist, k = 20, seed = 1)
head(selection[, c("cluster", "size", "selected")])
#>               cluster size      selected
#> 2020LSAL00151       1    4 2020LSAL00802
#> 2020LSAL00152       1    4 2020LSAL00802
#> 2020LSAL00163       2   25 2020LSAL00487
#> 2020LSAL00167       2   25 2020LSAL00487
#> 2020LSAL00176       3   11 2020LSAL00177
#> 2020LSAL00177       3   11 2020LSAL00177
unique(selection$selected)
#>  [1] "2020LSAL00802" "2020LSAL00487" "2020LSAL00177" "2020LSAL00854"
#>  [5] "2020LSAL00454" "2020LSAL00720" "2020LSAL00506" "2020LSAL00550"
#>  [9] "2020LSAL00660" "2020LSAL00668" "2020LSAL00724" "2020LSAL00790"
#> [13] "2020LSAL00912" "2020LSAL00792" "2020LSAL00866" "2020LSAL00892"
#> [17] "2020LSAL01016" "2020LSAL00994" "2020LSAL01040" "2020LSAL01188"
```

### Profile method: one strain per distinct profile

The binary table of modalities can be explored with an UpSet plot (here
the 12 most frequent modalities):

``` r

upset_data <- prepare_upset(prepared_data)
UpSetR::upset(upset_data, nsets = 12, order.by = "freq", nintersects = 20,
              mb.ratio = c(0.55, 0.45), text.scale = 1.1)
```

![](reference/figures/README-upset-1.png)

``` r

profiles <- define_profiles(upset_data)
selection <- select_profiles(profiles, prepared_data, seed = 1)
length(unique(selection$selected))   # number of strains to sequence
#> [1] 61
```

## Acknowledgements

[`cstats_table()`](https://lguillier.github.io/strainselect_package/reference/cstats_table.md)
and the Gower distance / hierarchical clustering workflow are adapted
from Anastasia Reusova’s tutorial [*Hierarchical Clustering on
Categorical Data in
R*](https://medium.com/@anastasia.reusova/hierarchical-clustering-on-categorical-data-in-r-a27e578f2995)
([code](https://github.com/khunreus/cluster-categorical)).

This work was supported by funding from the European Union’s Horizon
2020 Research and Innovation programme under grant agreement No 773830:
One Health European Joint Programme (project CARE: Cross-sectoral
framework for quality Assurance Resources for countries in the European
Union).
