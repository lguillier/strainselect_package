# Write an HTML report of the strain selection

Renders an HTML report of a selection made with
[`select_strains()`](https://lguillier.github.io/strainselect_package/reference/select_strains.md):
parameters and summary, silhouette curve with the optimal number of
clusters and the maximum number of strains, list of the selected strains
(with their metadata), optimal groups that are not represented, sizes of
the clusters and description of the columns of the CSV file (which ones
were used for the selection). Requires the rmarkdown package and pandoc.

## Usage

``` r
report_selection(
  x,
  file = "strain_selection_report.html",
  data = NULL,
  id = 1,
  title = "Selection of strains to sequence",
  csv = TRUE
)
```

## Arguments

- x:

  An object returned by
  [`select_strains()`](https://lguillier.github.io/strainselect_package/reference/select_strains.md).

- file:

  Path of the HTML file to write.

- data:

  The original metadata table, or `NULL` to show only the metadata used
  for the selection (see
  [`export_selection()`](https://lguillier.github.io/strainselect_package/reference/export_selection.md)).

- id:

  Name or position of the column of `data` containing the strain
  identifiers.

- title:

  Title of the report.

- csv:

  If `TRUE` (default), the table of
  [`export_selection()`](https://lguillier.github.io/strainselect_package/reference/export_selection.md)
  is also written as a CSV file next to the report (same name, `.csv`
  extension).

## Value

The path of the HTML report, invisibly.

## See also

Other clustering method:
[`assess_gower()`](https://lguillier.github.io/strainselect_package/reference/assess_gower.md),
[`cstats_table()`](https://lguillier.github.io/strainselect_package/reference/cstats_table.md),
[`export_selection()`](https://lguillier.github.io/strainselect_package/reference/export_selection.md),
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
if (requireNamespace("rmarkdown", quietly = TRUE) && rmarkdown::pandoc_available()) {
  report_selection(res, file = file.path(tempdir(), "selection.html"),
                   data = salmonella_strains, id = "IDENTIFIANT")
}
#> selection written to /tmp/RtmpQPybmE/selection.csv
#> report written to /tmp/RtmpQPybmE/selection.html
```
