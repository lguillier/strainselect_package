# Prepare the metadata table used for strain selection

Checks that strain identifiers are unique, keeps the metadata columns
used for the selection, optionally extracts the year and/or the month
from a date column, replaces missing values by `"unknown"` and converts
every column to a factor.

## Usage

``` r
prepare_input(
  data,
  col_select = seq_along(data),
  id = 1,
  date = 0,
  month = FALSE,
  year = TRUE,
  m,
  a
)
```

## Arguments

- data:

  A data frame with one row per strain.

- col_select:

  Integer vector giving the positions of the metadata columns to keep.
  The identifier and date columns are always removed from this
  selection. Defaults to all columns.

- id:

  Position of the column containing the strain identifiers.

- date:

  Position of the date column (format `dd/mm/yyyy`), or `0` (default) if
  no date should be used.

- month:

  If `TRUE`, a `MOIS` column with the month (`"01"` to `"12"`) is
  created from the date column.

- year:

  If `TRUE` (default), an `ANNEE` column with the year is created from
  the date column.

- m, a:

  Deprecated, use `month` and `year` instead.

## Value

A data frame with one row per strain (row names are the strain
identifiers) and one factor column per selected metadata, followed by
`ANNEE` and/or `MOIS` when a date column is used.

## Examples

``` r
datafile <- system.file("data_test.csv", package = "strainselect")
raw_data <- read.csv(datafile, sep = ";", header = TRUE)
prepared_data <- prepare_input(raw_data, col_select = c(7, 10, 13, 14, 17, 24),
                               id = 1, date = 17, month = FALSE, year = TRUE)
#> no duplicate ID
#> selected metadata: CONTEXTE, MATRICE1, REGION, SECTEUR, LIEUPVT, ANNEE
head(prepared_data)
#>                   CONTEXTE         MATRICE1               REGION
#> 2020LSAL00151 Surveillance     non spécifié Auvergne Rhone Alpes
#> 2020LSAL00152 Surveillance     non spécifié Auvergne Rhone Alpes
#> 2020LSAL00163 Surveillance Viande de canard   Nouvelle Aquitaine
#> 2020LSAL00167 Surveillance Viande de canard            Occitanie
#> 2020LSAL00176 Surveillance    Gallus gallus   Nouvelle Aquitaine
#> 2020LSAL00177 Surveillance           Dindes             Bretagne
#>                                    SECTEUR
#> 2020LSAL00151                  Eco-système
#> 2020LSAL00152                  Eco-système
#> 2020LSAL00163         Alimentation humaine
#> 2020LSAL00167         Alimentation humaine
#> 2020LSAL00176 Santé et production animales
#> 2020LSAL00177 Santé et production animales
#>                                                     LIEUPVT ANNEE
#> 2020LSAL00151                       Source/captage de l'eau  2020
#> 2020LSAL00152                       Source/captage de l'eau  2020
#> 2020LSAL00163                   Transformation industrielle  2020
#> 2020LSAL00167                   Transformation industrielle  2020
#> 2020LSAL00176 Lieu d'exploitation, d'élevage, ou de culture  2020
#> 2020LSAL00177 Lieu d'exploitation, d'élevage, ou de culture  2020
```
