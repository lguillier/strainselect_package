# Select one strain per group of identical profiles

Selects at random one strain in each group defined by
[`define_profiles()`](https://lguillier.github.io/strainselect_package/reference/define_profiles.md).

## Usage

``` r
select_profiles(profiles, prepared_data, seed = NULL)
```

## Arguments

- profiles:

  A data frame returned by
  [`define_profiles()`](https://lguillier.github.io/strainselect_package/reference/define_profiles.md).

- prepared_data:

  A data frame with one row per strain, as returned by
  [`prepare_input()`](https://lguillier.github.io/strainselect_package/reference/prepare_input.md),
  with rows in the same order as `profiles`.

- seed:

  An integer passed to
  [`set.seed()`](https://rdrr.io/r/base/Random.html) to make the random
  choice of the representative strains reproducible, or `NULL` (default)
  to leave the random number generator untouched.

## Value

`prepared_data` with three additional columns:

- group:

  the group of identical profiles of the strain;

- size:

  the number of strains in this group;

- selected:

  the identifier of the strain selected for this group.

The selected strains are given by `unique(result$selected)`.

## See also

Other profile method:
[`define_profiles()`](https://lguillier.github.io/strainselect_package/reference/define_profiles.md),
[`prepare_upset()`](https://lguillier.github.io/strainselect_package/reference/prepare_upset.md)

## Examples

``` r
datafile <- system.file("data_test.csv", package = "strainselect")
raw_data <- read.csv(datafile, sep = ";", header = TRUE)
prepared_data <- prepare_input(raw_data, col_select = c(7, 10, 13, 14, 17, 24),
                               id = 1, date = 17)
#> no duplicate ID
#> selected metadata: CONTEXTE, MATRICE1, REGION, SECTEUR, LIEUPVT, ANNEE
upset_profiles <- define_profiles(prepare_upset(prepared_data))
selection <- select_profiles(upset_profiles, prepared_data, seed = 1)
# one strain per distinct profile
length(unique(selection$selected))
#> [1] 61
```
