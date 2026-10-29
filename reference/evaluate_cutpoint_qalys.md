# Evaluates a cutpoint by returning the mean QALYs lost per sample.

Evaluates a cutpoint by returning the mean QALYs lost per sample.

## Usage

``` r
evaluate_cutpoint_qalys(predicted, actual, pt, nmb)
```

## Arguments

- predicted:

  A vector of predicted probabilities.

- actual:

  A vector of actual outcomes.

- pt:

  The probability threshold to be evaluated.

- nmb:

  A named vector containing NMB assigned to each classification and the
  treatment effects and QALYS lost due to the event of interest.

## Value

Returns a `numeric` value representing the mean QALYs for that cutpoint
and data.

## Examples

``` r
evaluate_cutpoint_qalys(
  predicted = runif(1000),
  actual = sample(c(0, 1), size = 1000, replace = TRUE),
  pt = 0.1,
  nmb = c(
    "qalys_lost" = 5,
    "low_risk_group_treatment_effect" = 0,
    "high_risk_group_treatment_effect" = 0.5
  )
)
#> [1] -1.2725
```
