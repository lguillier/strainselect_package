# Prepare the metadata table used for strain selection

Checks that strain identifiers are unique, keeps the metadata columns
used for the selection, optionally extracts the year and/or the month
from a date column, replaces missing values by `"unknown"` and converts
every column to a factor.

## Usage

``` r
prepare_input(
  data,
  col_select = seq_len(ncol(data)),
  id = 1,
  date = NULL,
  month = FALSE,
  year = TRUE,
  date_format = "%d/%m/%Y",
  m,
  a
)
```

## Arguments

- data:

  A data frame (or a matrix) with one row per strain.

- col_select:

  Names or positions of the metadata columns to keep. The identifier and
  date columns are always removed from this selection. Defaults to all
  columns.

- id:

  Name or position of the column containing the strain identifiers.

- date:

  Name or position of the date column, or `NULL` (default) if no date
  should be used. `0` is also accepted for "no date".

- month:

  If `TRUE`, a `MOIS` column with the month (`"01"` to `"12"`) is
  created from the date column.

- year:

  If `TRUE` (default), an `ANNEE` column with the year is created from
  the date column.

- date_format:

  Format of the dates, see
  [`strptime()`](https://rdrr.io/r/base/strptime.html). Defaults to
  `"%d/%m/%Y"` (e.g. `09/01/2020`). Ignored when the date column is
  already of class `Date` or `POSIXt`.

- m, a:

  Deprecated, use `month` and `year` instead.

## Value

A data frame with one row per strain (row names are the strain
identifiers) and one factor column per selected metadata, followed by
`ANNEE` and/or `MOIS` when a date column is used. Dates that cannot be
read give `"unknown"`.

## See also

Other data preparation:
[`salmonella_strains`](https://lguillier.github.io/strainselect_package/reference/salmonella_strains.md)

## Examples

``` r
raw_data <- salmonella_strains
prepared_data <- prepare_input(
  raw_data,
  col_select = c("CONTEXTE", "MATRICE1", "REGION", "SECTEUR", "LIEUPVT"),
  id = "IDENTIFIANT", date = "DATE_PRELEVEMENT", month = FALSE, year = TRUE
)
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
# the same with column positions
prepared_data <- prepare_input(raw_data, col_select = c(5, 8, 11, 12, 15, 22),
                               id = 1, date = 15)
#> no duplicate ID
#> selected metadata: CONTEXTE, MATRICE1, REGION, SECTEUR, LIEUPVT, ANNEE
```
