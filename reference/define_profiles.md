# Group strains with identical profiles

Concatenates the columns of the binary table into one profile per strain
and gives the same group number to strains with identical profiles.

## Usage

``` r
define_profiles(data, sep = "")
```

## Arguments

- data:

  A data frame with one row per strain, typically the binary table
  returned by
  [`prepare_upset()`](https://lguillier.github.io/strainselect_package/reference/prepare_upset.md).

- sep:

  Separator used between values when building the profiles (none by
  default).

## Value

A data frame with the same row names as `data` and three columns:

- profiles:

  the profile of the strain (concatenated values);

- group:

  an integer identifying the group of identical profiles;

- names:

  the strain identifier.

## See also

Other profile method:
[`prepare_upset()`](https://lguillier.github.io/strainselect_package/reference/prepare_upset.md),
[`select_profiles()`](https://lguillier.github.io/strainselect_package/reference/select_profiles.md)

## Examples

``` r
raw_data <- salmonella_strains
prepared_data <- prepare_input(raw_data, col_select = c(7, 10, 13, 14, 17, 24),
                               id = 1, date = 17)
#> no duplicate ID
#> selected metadata: CONTEXTE, MATRICE1, REGION, SECTEUR, LIEUPVT, ANNEE
upset_data <- prepare_upset(prepared_data)
upset_profiles <- define_profiles(upset_data)
# number of distinct profiles
max(upset_profiles$group)
#> [1] 61
```
