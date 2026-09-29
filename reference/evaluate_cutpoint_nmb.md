# Evaluates a cutpoint by returning the mean NMB per sample.

Evaluates a cutpoint by returning the mean NMB per sample.

## Usage

``` r
evaluate_cutpoint_nmb(predicted, actual, pt, nmb)
```

## Arguments

- predicted:

  A vector of predicted probabilities.

- actual:

  A vector of actual outcomes.

- pt:

  The probability threshold to be evaluated.

- nmb:

  A named vector containing NMB assigned to each classification.

## Value

Returns a `numeric` value representing the NMB for that cutpoint and
data.

## Examples

``` r
evaluate_cutpoint_nmb(
  predicted = runif(1000),
  actual = sample(c(0, 1), size = 1000, replace = TRUE),
  pt = 0.1,
  nmb = c("TP" = -3, "TN" = 0, "FP" = -1, "FN" = -4)
)
#> [1] -1.889
```
