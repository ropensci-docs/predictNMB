# Evaluates a cutpoint by returning the mean treatment cost per sample.

Evaluates a cutpoint by returning the mean treatment cost per sample.

## Usage

``` r
evaluate_cutpoint_cost(predicted, actual, pt, nmb)
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
  treatment costs.

## Value

Returns a `numeric` value representing the mean cost for that cutpoint
and data.

## Examples

``` r
evaluate_cutpoint_cost(
  predicted = runif(1000),
  actual = sample(c(0, 1), size = 1000, replace = TRUE),
  pt = 0.1,
  nmb = c(
    "qalys_lost" = 5,
    "low_risk_group_treatment_cost" = 0,
    "high_risk_group_treatment_cost" = 1,
    "low_risk_group_treatment_effect" = 0,
    "high_risk_group_treatment_effect" = 0.3,
    "outcome_cost" = 10
  )
)
#> [1] 4.365
```
