# Package index

## Data and data preparation

- [`salmonella_strains`](https://lguillier.github.io/strainselect_package/reference/salmonella_strains.md)
  :

  Example metadata of 100 *Salmonella* strains

- [`prepare_input()`](https://lguillier.github.io/strainselect_package/reference/prepare_input.md)
  : Prepare the metadata table used for strain selection

## Clustering method

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
