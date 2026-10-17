# Package index

## Data and data preparation

- [`salmonella_strains`](https://lguillier.github.io/strainselect_package/reference/salmonella_strains.md)
  :

  Example metadata of 100 *Salmonella* strains

- [`prepare_input()`](https://lguillier.github.io/strainselect_package/reference/prepare_input.md)
  : Prepare the metadata table used for strain selection

## Strain selection in one step

Optimal number of strains, maximum number of strains, export and report.

- [`select_strains()`](https://lguillier.github.io/strainselect_package/reference/select_strains.md)
  : Select strains to sequence, with or without a maximum number of
  strains
- [`export_selection()`](https://lguillier.github.io/strainselect_package/reference/export_selection.md)
  : Export the strain selection with the original metadata
- [`report_selection()`](https://lguillier.github.io/strainselect_package/reference/report_selection.md)
  : Write an HTML report of the strain selection

## Clustering method, step by step

When the number of strains that can be sequenced is limited.

- [`assess_gower()`](https://lguillier.github.io/strainselect_package/reference/assess_gower.md)
  : Compute Gower distances and the hierarchical clustering tree
- [`cstats_table()`](https://lguillier.github.io/strainselect_package/reference/cstats_table.md)
  : Clustering statistics for an increasing number of clusters
- [`select_silhouette()`](https://lguillier.github.io/strainselect_package/reference/select_silhouette.md)
  : Select the best clustered strain of each cluster

## Profile method

When the number of strains to sequence is not limited.

- [`prepare_upset()`](https://lguillier.github.io/strainselect_package/reference/prepare_upset.md)
  : Build the binary table of metadata modalities
- [`define_profiles()`](https://lguillier.github.io/strainselect_package/reference/define_profiles.md)
  : Group strains with identical profiles
- [`select_profiles()`](https://lguillier.github.io/strainselect_package/reference/select_profiles.md)
  : Select one strain per group of identical profiles
