# Returns a `ggplot2` theme that reduces clutter in an `autoplot()` of a `predictNMBsim` object.

Returns a `ggplot2` theme that reduces clutter in an
[`autoplot()`](https://ggplot2.tidyverse.org/reference/autoplot.html) of
a `predictNMBsim` object.

## Usage

``` r
theme_sim()
```

## Value

Returns a `ggplot2` theme.

## Examples

``` r
# \donttest{
get_nmb <- function() c("TP" = -3, "TN" = 0, "FP" = -1, "FN" = -4)
sim_obj <- do_nmb_sim(
  sample_size = 200, n_sims = 50, n_valid = 10000, sim_auc = 0.7,
  event_rate = 0.1, fx_nmb_training = get_nmb, fx_nmb_evaluation = get_nmb
)

autoplot(sim_obj) + theme_sim()

# }
```
