# strainselect: Select Bacterial Strains to Sequence Based on Their Metadata

Helps choosing which bacterial strains to sequence from a collection
described by categorical metadata (sampling context, matrix, region,
year...). Two methods are provided. The clustering method groups the
strains into a chosen number of clusters using the Gower distance and
hierarchical clustering, and selects the best clustered strain of each
cluster according to its silhouette width; it is suited when the number
of strains that can be sequenced is limited. The profile method groups
the strains that share exactly the same metadata and selects one strain
per group, so that every distinct profile is represented.

## Methods

Both methods start with
[`prepare_input()`](https://lguillier.github.io/strainselect_package/reference/prepare_input.md),
which cleans the table of metadata.

- The **clustering method** is suited when the number of strains that
  can be sequenced is limited:
  [`assess_gower()`](https://lguillier.github.io/strainselect_package/reference/assess_gower.md)
  computes Gower distances and a hierarchical clustering,
  [`cstats_table()`](https://lguillier.github.io/strainselect_package/reference/cstats_table.md)
  helps choosing the number of clusters, and
  [`select_silhouette()`](https://lguillier.github.io/strainselect_package/reference/select_silhouette.md)
  selects the best clustered strain of each cluster.

- The **profile method** is suited when the number of strains is not
  limited:
  [`prepare_upset()`](https://lguillier.github.io/strainselect_package/reference/prepare_upset.md)
  builds a binary table of modalities,
  [`define_profiles()`](https://lguillier.github.io/strainselect_package/reference/define_profiles.md)
  groups strictly identical strains, and
  [`select_profiles()`](https://lguillier.github.io/strainselect_package/reference/select_profiles.md)
  selects one strain per group.

See
[`vignette("get-started", package = "strainselect")`](https://lguillier.github.io/strainselect_package/articles/get-started.md)
for a complete example.

## See also

Useful links:

- <https://github.com/lguillier/strainselect_package>

- Report bugs at
  <https://github.com/lguillier/strainselect_package/issues>

## Author

**Maintainer**: Laurent Guillier <guillier.laurent@gmail.com>
([ORCID](https://orcid.org/0000-0002-7867-2937))

Authors:

- Marie Vallée <marie.vallee@anses.fr>
  ([ORCID](https://orcid.org/0000-0002-4233-8400))
