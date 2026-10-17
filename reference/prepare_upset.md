# Build the binary table of metadata modalities

Creates one column per modality of each metadata, filled with 1 when the
strain has this modality and 0 otherwise. The result can be used to draw
an UpSet plot (e.g. with
[`UpSetR::upset()`](https://rdrr.io/pkg/UpSetR/man/upset.html)) and to
define profiles with
[`define_profiles()`](https://lguillier.github.io/strainselect_package/reference/define_profiles.md).

## Usage

``` r
prepare_upset(prepared_data)
```

## Arguments

- prepared_data:

  A data frame with one row per strain, as returned by
  [`prepare_input()`](https://lguillier.github.io/strainselect_package/reference/prepare_input.md).

## Value

A data frame with the same row names as `prepared_data` and one numeric
(0/1) column per modality, named `"<metadata> _ <modality>"`. Modalities
appear in their order of first appearance.

## See also

Other profile method:
[`define_profiles()`](https://lguillier.github.io/strainselect_package/reference/define_profiles.md),
[`select_profiles()`](https://lguillier.github.io/strainselect_package/reference/select_profiles.md)

## Examples

``` r
datafile <- system.file("data_test.csv", package = "strainselect")
raw_data <- read.csv(datafile, sep = ";", header = TRUE)
prepared_data <- prepare_input(raw_data, col_select = c(7, 10, 13, 14, 17, 24),
                               id = 1, date = 17)
#> no duplicate ID
#> selected metadata: CONTEXTE, MATRICE1, REGION, SECTEUR, LIEUPVT, ANNEE
upset_data <- prepare_upset(prepared_data)
upset_data[1:5, 1:4]
#>               CONTEXTE _ Surveillance CONTEXTE _ Alerte Produit
#> 2020LSAL00151                       1                         0
#> 2020LSAL00152                       1                         0
#> 2020LSAL00163                       1                         0
#> 2020LSAL00167                       1                         0
#> 2020LSAL00176                       1                         0
#>               CONTEXTE _ Programmes de contrôle et d'éradication
#> 2020LSAL00151                                                  0
#> 2020LSAL00152                                                  0
#> 2020LSAL00163                                                  0
#> 2020LSAL00167                                                  0
#> 2020LSAL00176                                                  0
#>               CONTEXTE _ Etudes cliniques
#> 2020LSAL00151                           0
#> 2020LSAL00152                           0
#> 2020LSAL00163                           0
#> 2020LSAL00167                           0
#> 2020LSAL00176                           0
```
