# Create table summaries of `predictNMBsim` objects.

Create table summaries of `predictNMBsim` objects.

## Usage

``` r
# S3 method for class 'predictNMBsim'
summary(
  object,
  what = c("nmb", "inb", "cutpoints"),
  inb_ref_col = NULL,
  agg_functions = list(median = function(x) {
     round(stats::median(x), digits = 2)

    }, `95% CI` = function(x) {
     paste0(round(stats::quantile(x, probs = c(0.025,
    0.975)), digits = 1), collapse = " to ")
 }),
  rename_vector,
  ...
)
```

## Arguments

- object:

  A `predictNMBsim` object.

- what:

  What to summarise: one of "nmb", "inb" or "cutpoints". Defaults to
  "nmb".

- inb_ref_col:

  Which cutpoint method to use as the reference strategy when
  calculating the incremental net monetary benefit. See `do_nmb_sim` for
  more information.

- agg_functions:

  A named list of functions to use to aggregate the selected values.
  Defaults to the median and 95% interval.

- rename_vector:

  A named vector for renaming the methods in the summary. The values of
  the vector are the default names and the names given are the desired
  names in the output.

- ...:

  Additional, ignored arguments.

## Value

Returns a `tibble`.

## Details

Table summaries will be based on the `what` argument. Using "nmb"
returns the simulated values for NMB, with no reference group; "inb"
returns the difference between simulated values for NMB and a set
strategy defined by `inb_ref_col`; "cutpoints" returns the cutpoints
selected (0, 1).

## Examples

``` r

# perform simulation with do_nmb_sim()
# \donttest{
get_nmb <- function() c("TP" = -3, "TN" = 0, "FP" = -1, "FN" = -4)
sim_obj <- do_nmb_sim(
  sample_size = 200, n_sims = 50, n_valid = 10000, sim_auc = 0.7,
  event_rate = 0.1, fx_nmb_training = get_nmb, fx_nmb_evaluation = get_nmb,
  cutpoint_methods = c("all", "none", "youden", "value_optimising")
)
summary(
  sim_obj,
  rename_vector = c(
    "Value_Optimising" = "value_optimising",
    "Treat_None" = "none",
    "Treat_All" = "all",
    "Youden_Index" = "youden"
  )
)
#> # A tibble: 4 × 3
#>   method           median `95% CI`    
#>   <chr>             <dbl> <chr>       
#> 1 Treat_All         -1.2  -1.2 to -1.2
#> 2 Treat_None        -0.4  -0.4 to -0.4
#> 3 Value_Optimising  -0.4  -0.4 to -0.4
#> 4 Youden_Index      -0.63 -0.9 to -0.5
# }
```
