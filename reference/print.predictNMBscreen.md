# Print a summary of a predictNMBscreen object

Print a summary of a predictNMBscreen object

## Usage

``` r
# S3 method for class 'predictNMBscreen'
print(x, ...)
```

## Arguments

- x:

  A `predictNMBscreen` object.

- ...:

  Optional, ignored arguments.

## Value

`print(x)` returns `x` invisibly.

## Examples

``` r
# \donttest{
get_nmb <- function() c("TP" = -3, "TN" = 0, "FP" = -1, "FN" = -4)
sim_screen_obj <- screen_simulation_inputs(
  n_sims = 50, n_valid = 10000, sim_auc = seq(0.7, 0.9, 0.1),
  event_rate = 0.1,
  fx_nmb_training = get_nmb, fx_nmb_evaluation = get_nmb
)
print(sim_screen_obj)
#> predictNMBscreen object
#> 
#> There were combinations screened
#> 
#> There was only one input ( sim_auc ) that was screened for multiple values:
#> $sim_auc
#> [1] 0.7 0.8 0.9
#> 
# }
```
