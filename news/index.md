# Changelog

## strainselect (development version)

- [`prepare_input()`](https://lguillier.github.io/strainselect_package/reference/prepare_input.md)
  accepts column **names** as well as positions for `col_select`, `id`
  and `date`, with a clear error for unknown columns.
- [`prepare_input()`](https://lguillier.github.io/strainselect_package/reference/prepare_input.md)
  reads dates with the new `date_format` argument (`"%d/%m/%Y"` by
  default) and accepts `Date` columns; unreadable dates give
  `"unknown"`. `date = NULL` is the new default for “no date” (`0` still
  works).
- The old `How_to_use_Strainselect/` folder and `.Rhistory` are removed
  from the repository: their content is now in the “Get started”
  vignette.

## strainselect 0.1.0

### Breaking changes

- [`prepare_input()`](https://lguillier.github.io/strainselect_package/reference/prepare_input.md):
  the arguments `m` and `a` are renamed `month` and `year`;
  [`cstats_table()`](https://lguillier.github.io/strainselect_package/reference/cstats_table.md):
  the argument `l` is renamed `step`. The old names still work but give
  a deprecation warning.
- [`prepare_input()`](https://lguillier.github.io/strainselect_package/reference/prepare_input.md)
  no longer keeps the identifier column in the selected metadata when
  `col_select` includes it (it was used in the distances).
- [`cstats_table()`](https://lguillier.github.io/strainselect_package/reference/cstats_table.md)
  returns the table of statistics (it returned `NULL` or only the plot),
  and its rows are named `Test <number of clusters>`.

### New features

- [`select_silhouette()`](https://lguillier.github.io/strainselect_package/reference/select_silhouette.md)
  and
  [`select_profiles()`](https://lguillier.github.io/strainselect_package/reference/select_profiles.md)
  gain a `seed` argument to make the selection reproducible.
- [`select_silhouette()`](https://lguillier.github.io/strainselect_package/reference/select_silhouette.md)
  checks that `k` is between 2 and the number of strains minus 1.

### Bug fixes and improvements

- The package can be installed and used without loading its dependencies
  first;
  [`select_silhouette()`](https://lguillier.github.io/strainselect_package/reference/select_silhouette.md)
  and
  [`define_profiles()`](https://lguillier.github.io/strainselect_package/reference/define_profiles.md)
  no longer depend on global objects;
  [`select_profiles()`](https://lguillier.github.io/strainselect_package/reference/select_profiles.md)
  fills the `size` column.
- [`prepare_upset()`](https://lguillier.github.io/strainselect_package/reference/prepare_upset.md),
  [`define_profiles()`](https://lguillier.github.io/strainselect_package/reference/define_profiles.md),
  [`select_profiles()`](https://lguillier.github.io/strainselect_package/reference/select_profiles.md)
  and
  [`select_silhouette()`](https://lguillier.github.io/strainselect_package/reference/select_silhouette.md)
  are vectorised (about 2000 times faster on 3000 strains, same
  results).
- Information is displayed with
  [`message()`](https://rdrr.io/r/base/message.html) and can be silenced
  with [`suppressMessages()`](https://rdrr.io/r/base/message.html).
- The example data `data_test.csv` is encoded in UTF-8.
- Complete documentation of the functions, a “Get started” vignette,
  unit tests for every function and continuous integration on GitHub.

## strainselect 0.0.0.9000

- First version.
