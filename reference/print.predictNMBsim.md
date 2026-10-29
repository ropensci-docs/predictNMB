# Print a summary of a predictNMBsim object

Print a summary of a predictNMBsim object

## Usage

``` r
# S3 method for class 'predictNMBsim'
print(x, ...)
```

## Arguments

- x:

  A `predictNMBsim` object.

- ...:

  Optional, ignored arguments.

## Value

`print(x)` returns `x` invisibly.

## Examples

``` r
# \donttest{
get_nmb <- function() c("TP" = -3, "TN" = 0, "FP" = -1, "FN" = -4)
sim_obj <- do_nmb_sim(
  sample_size = 200, n_sims = 50, n_valid = 10000, sim_auc = 0.7,
  event_rate = 0.1, fx_nmb_training = get_nmb, fx_nmb_evaluation = get_nmb
)
print(sim_obj)
#> predictNMB object
#> 
#> Training data sample size:  200
#> Minimum number of events in training sample:  20
#> Evaluation data sample size:  10000
#> Number of simulations:  50
#> Simulated AUC:  0.7
#> Simulated event rate:  0.1
# }
```
