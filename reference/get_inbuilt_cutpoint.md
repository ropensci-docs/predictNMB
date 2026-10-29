# Get a cutpoint using the methods inbuilt to predictNMB

Get a cutpoint using the methods inbuilt to predictNMB

## Usage

``` r
get_inbuilt_cutpoint(predicted, actual, nmb, method)
```

## Arguments

- predicted:

  A vector of predicted probabilities

- actual:

  A vector of actual outcomes

- nmb:

  A named vector containing NMB assigned to each classification

- method:

  A cutpoint selection method to be used methods that can be used as the
  method argument

## Value

Returns a selected cutpoint (numeric).

## Examples

``` r
## get the list of available methods:
get_inbuilt_cutpoint_methods()
#> [1] "all"              "none"             "value_optimising" "youden"          
#> [5] "cost_minimising"  "prod_sens_spec"   "roc01"            "index_of_union"  

## get the cutpoint that maximises the Youden index for a given set of
## probabilities and outcomes
get_inbuilt_cutpoint(
  predicted = runif(1000),
  actual = sample(c(0, 1), size = 1000, replace = TRUE),
  method = "youden"
)
#> [1] 0.2542118
```
