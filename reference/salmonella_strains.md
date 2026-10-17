# Example metadata of 100 *Salmonella* strains

Metadata of 100 strains of *Salmonella enterica* serotype
1,4,\[5\],12:i:- (monophasic variant of Typhimurium) collected in France
in 2020, used in the examples of the package. Column names and values
are in French, as in the original database.

## Usage

``` r
salmonella_strains
```

## Format

A data frame with 100 rows (one per strain) and 22 columns:

- IDENTIFIANT:

  strain identifier (unique);

- SEROTYPE:

  serotype of the strain;

- COMMENTAIRE:

  free-text description of the sample;

- SAMPLETYPE:

  type of sample;

- CONTEXTE:

  sampling context (surveillance, product alert, control programme...);

- PAYS:

  country of sampling;

- MATRICE:

  sampled matrix, most detailed level;

- MATRICE1:

  sampled matrix, first level of grouping;

- MATRICE2:

  sampled matrix, second level of grouping;

- NOM_DEPARTEMENT:

  name of the French département of sampling;

- REGION:

  French region of sampling;

- SECTEUR:

  sector (human food, animal health and production, ecosystem...);

- NUMERO_DEPARTEMENT:

  number of the French département;

- CODE_POSTAL:

  postal code of the place of sampling;

- DATE_PRELEVEMENT:

  date of sampling (`dd/mm/yyyy`);

- DATE_RECEPTION:

  date of reception at the laboratory (`dd/mm/yyyy`);

- TYPE_ANALYSE:

  type of analysis;

- ATYPIQUE:

  flag for atypical strains;

- TYPE_DE_DONNEES:

  type of data;

- BOX_NUMBER:

  storage box of the strain;

- EMPLACEMENT:

  position of the strain in the box;

- LIEUPVT:

  place of sampling in the food chain (farm, slaughterhouse, industrial
  processing...).

## Source

Example data provided by the authors. The same table is available as a
CSV file: `system.file("data_test.csv", package = "strainselect")`.

## See also

Other data preparation:
[`prepare_input()`](https://lguillier.github.io/strainselect_package/reference/prepare_input.md)

## Examples

``` r
str(salmonella_strains[, c("IDENTIFIANT", "CONTEXTE", "REGION", "DATE_PRELEVEMENT")])
#> 'data.frame':    100 obs. of  4 variables:
#>  $ IDENTIFIANT     : chr  "2020LSAL00151" "2020LSAL00152" "2020LSAL00163" "2020LSAL00167" ...
#>  $ CONTEXTE        : chr  "Surveillance" "Surveillance" "Surveillance" "Surveillance" ...
#>  $ REGION          : chr  "Auvergne Rhone Alpes" "Auvergne Rhone Alpes" "Nouvelle Aquitaine" "Occitanie" ...
#>  $ DATE_PRELEVEMENT: chr  "09/01/2020" "09/01/2020" "07/01/2020" "14/01/2020" ...
```
