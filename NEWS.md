# strainselect (development version)

* The package has a DOI on Zenodo (10.5281/zenodo.23439526): badge in the
  README, DOI in `citation("strainselect")` and `CITATION.cff`.

# strainselect 0.2.0

* New `select_strains()`: the clustering method in one step. It finds the
  optimal number of clusters (largest average silhouette width) and selects
  the strains taking into account the maximum number of strains that can be
  sequenced (`n_max`): optimal strains completed with supplementary strains
  when `n_max` is larger than the optimum (`fill = TRUE`), or the best
  coverage with `n_max` strains and the list of the optimal groups that are
  not represented when it is smaller. `print()` and `plot()` methods.
  With `method = "profile"`, the same logic applies to the profile method:
  groups of identical strains sorted by decreasing size, one strain in each
  of the `n_max` largest groups when `n_max` is smaller than the number of
  groups, and supplementary strains added turn by turn (from the largest
  group to the smallest) when it is larger.
* New `export_selection()`: the original metadata table with the selection
  (`cluster`, `optimal_group`, `selected`, `status`, `representative`,
  `group_represented`), optionally written to a CSV file.
* New `report_selection()`: HTML report of the selection (summary,
  silhouette curve, selected strains, optimal groups not represented,
  clusters, columns of the CSV file used or not for the selection), written
  with the CSV file of the selection.
* `prepare_input()` accepts column **names** as well as positions for
  `col_select`, `id` and `date`, with a clear error for unknown columns.
* `prepare_input()` reads dates with the new `date_format` argument
  (`"%d/%m/%Y"` by default) and accepts `Date` columns; unreadable dates give
  `"unknown"`. `date = NULL` is the new default for "no date" (`0` still works).
* New dataset `salmonella_strains` (the example table, available as soon as
  the package is loaded); the examples, the vignette and the README use it.
  The CSV file `data_test.csv` is kept to show the expected input format.
* The columns `REF_PARTENAIRE` and `LABORATORY_CODE` (partner laboratory
  information) are removed from the example data, which now has 22 columns.
  The examples use column names rather than positions.
* `citation("strainselect")` gives the reference of the package; a
  `CITATION.cff` file adds a "Cite this repository" button on GitHub.
* The old `How_to_use_Strainselect/` folder and `.Rhistory` are removed from
  the repository: their content is now in the "Get started" vignette.

# strainselect 0.1.0

## Breaking changes

* `prepare_input()`: the arguments `m` and `a` are renamed `month` and
  `year`; `cstats_table()`: the argument `l` is renamed `step`. The old names
  still work but give a deprecation warning.
* `prepare_input()` no longer keeps the identifier column in the selected
  metadata when `col_select` includes it (it was used in the distances).
* `cstats_table()` returns the table of statistics (it returned `NULL` or
  only the plot), and its rows are named `Test <number of clusters>`.

## New features

* `select_silhouette()` and `select_profiles()` gain a `seed` argument to
  make the selection reproducible.
* `select_silhouette()` checks that `k` is between 2 and the number of
  strains minus 1.

## Bug fixes and improvements

* The package can be installed and used without loading its dependencies
  first; `select_silhouette()` and `define_profiles()` no longer depend on
  global objects; `select_profiles()` fills the `size` column.
* `prepare_upset()`, `define_profiles()`, `select_profiles()` and
  `select_silhouette()` are vectorised (about 2000 times faster on 3000
  strains, same results).
* Information is displayed with `message()` and can be silenced with
  `suppressMessages()`.
* The example data `data_test.csv` is encoded in UTF-8.
* Complete documentation of the functions, a "Get started" vignette, unit
  tests for every function and continuous integration on GitHub.

# strainselect 0.0.0.9000

* First version.
