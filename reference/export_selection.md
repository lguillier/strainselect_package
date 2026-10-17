# Export the strain selection with the original metadata

Adds the results of
[`select_strains()`](https://lguillier.github.io/strainselect_package/reference/select_strains.md)
(`cluster`, `optimal_group`, `selected`, `status`, `representative`,
`group_represented`) to the original metadata table and optionally
writes it to a CSV file.

## Usage

``` r
export_selection(x, data = NULL, id = 1, file = NULL, sep = ";")
```

## Arguments

- x:

  An object returned by
  [`select_strains()`](https://lguillier.github.io/strainselect_package/reference/select_strains.md).

- data:

  The original metadata table (e.g. the table given to
  [`prepare_input()`](https://lguillier.github.io/strainselect_package/reference/prepare_input.md)),
  or `NULL` to export only the metadata used for the selection.

- id:

  Name or position of the column of `data` containing the strain
  identifiers.

- file:

  Path of the CSV file to write, or `NULL` (default) to write nothing.

- sep:

  Field separator of the CSV file (`";"` by default).

## Value

A data frame with one row per strain (in the order of `data`): the
columns of `data` followed by the columns of the selection. It is
returned invisibly when `file` is given.

## See also

Other clustering method:
[`assess_gower()`](https://lguillier.github.io/strainselect_package/reference/assess_gower.md),
[`cstats_table()`](https://lguillier.github.io/strainselect_package/reference/cstats_table.md),
[`report_selection()`](https://lguillier.github.io/strainselect_package/reference/report_selection.md),
[`select_silhouette()`](https://lguillier.github.io/strainselect_package/reference/select_silhouette.md),
[`select_strains()`](https://lguillier.github.io/strainselect_package/reference/select_strains.md)

## Examples

``` r
prepared_data <- prepare_input(
  salmonella_strains,
  col_select = c("CONTEXTE", "MATRICE1", "REGION", "SECTEUR", "LIEUPVT"),
  id = "IDENTIFIANT", date = "DATE_PRELEVEMENT"
)
#> no duplicate ID
#> selected metadata: CONTEXTE, MATRICE1, REGION, SECTEUR, LIEUPVT, ANNEE
res <- select_strains(prepared_data, n_max = 20, seed = 1)
selection <- export_selection(res, data = salmonella_strains, id = "IDENTIFIANT")
# the strains to sequence, with all their metadata
head(selection[selection$selected, c("IDENTIFIANT", "REGION", "status")])
#>      IDENTIFIANT                     REGION   status
#> 6  2020LSAL00177                   Bretagne selected
#> 14 2020LSAL00454            Hauts de France selected
#> 20 2020LSAL00487              Ile de France selected
#> 22 2020LSAL00506                       <NA> selected
#> 27 2020LSAL00549 Provence Alpes Cote d Azur selected
#> 36 2020LSAL00660                  Occitanie selected
# write the table to a CSV file
export_selection(res, data = salmonella_strains, id = "IDENTIFIANT",
                 file = file.path(tempdir(), "selection.csv"))
#> selection written to /tmp/RtmpKHrqO4/selection.csv
```
