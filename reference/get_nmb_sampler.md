# Make a NMB sampler for use in `do_nmb_sim()` or `screen_simulation_inputs()`

Make a NMB sampler for use in
[`do_nmb_sim()`](https://docs.ropensci.org/predictNMB/reference/do_nmb_sim.md)
or
[`screen_simulation_inputs()`](https://docs.ropensci.org/predictNMB/reference/screen_simulation_inputs.md)

## Usage

``` r
get_nmb_sampler(
  outcome_cost,
  wtp,
  qalys_lost,
  high_risk_group_treatment_effect,
  high_risk_group_treatment_cost,
  low_risk_group_treatment_effect = 0,
  low_risk_group_treatment_cost = 0,
  use_expected_values = FALSE,
  nboot = 10000
)
```

## Arguments

- outcome_cost:

  The cost of the outcome. Must be provided if `wtp` and `qalys_lost`
  are not. Or can be used in addition to these arguments to represent
  additional cost to the health burden.

- wtp:

  Willingness-to-pay.

- qalys_lost:

  Quality-adjusted life years (QALYs) lost due to healthcare event being
  predicted.

- high_risk_group_treatment_effect:

  The effect of the treatment provided to patients given high risk
  prediction. Can be a number of a function. Provide a function to
  incorporate uncertainty.

- high_risk_group_treatment_cost:

  The cost of the treatment provided to patients given high risk
  prediction. Can be a number of a function. Provide a function to
  incorporate uncertainty.

- low_risk_group_treatment_effect:

  The effect of the treatment provided to patients given low risk
  prediction. Can be a number of a function. Provide a function to
  incorporate uncertainty. Defaults to 0 (no treatment).

- low_risk_group_treatment_cost:

  The cost of the treatment provided to patients given low risk
  prediction. Can be a number of a function. Provide a function to
  incorporate uncertainty. Defaults to 0 (no treatment).

- use_expected_values:

  Logical. If `TRUE`, gets the mean of many samples from the produced
  function and returns these every time. This is a sensible choice when
  using the resulting function for selecting the cutpoint. See
  `fx_nmb_training`. Defaults to `FALSE`.

- nboot:

  The number of samples to use when creating a function that returns the
  expected values. Defaults to 10000.

## Value

Returns a `NMBsampler` object.

## Examples

``` r
get_nmb_training <- get_nmb_sampler(
  outcome_cost = 100,
  high_risk_group_treatment_effect = function() rbeta(1, 1, 2),
  high_risk_group_treatment_cost = 10,
  use_expected_values = TRUE
)
get_nmb_evaluation <- get_nmb_sampler(
  outcome_cost = 100,
  high_risk_group_treatment_effect = function() rbeta(1, 1, 2),
  high_risk_group_treatment_cost = 10
)

get_nmb_training()
#>         TP         FP         TN         FN 
#>  -76.48267  -10.00000    0.00000 -100.00000 
get_nmb_training()
#>         TP         FP         TN         FN 
#>  -76.48267  -10.00000    0.00000 -100.00000 
get_nmb_training()
#>         TP         FP         TN         FN 
#>  -76.48267  -10.00000    0.00000 -100.00000 
get_nmb_evaluation()
#>         TP         FP         TN         FN 
#>  -70.09922  -10.00000    0.00000 -100.00000 
get_nmb_evaluation()
#>         TP         FP         TN         FN 
#>  -70.59073  -10.00000    0.00000 -100.00000 
get_nmb_evaluation()
#>         TP         FP         TN         FN 
#>  -71.53738  -10.00000    0.00000 -100.00000 
```
