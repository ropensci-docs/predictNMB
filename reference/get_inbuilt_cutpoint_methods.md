# Get a vector of all the inbuilt cutpoint methods

Get a vector of all the inbuilt cutpoint methods

## Usage

``` r
get_inbuilt_cutpoint_methods()
```

## Value

Returns a vector cutpoint methods that can be used in
[`do_nmb_sim()`](https://docs.ropensci.org/predictNMB/reference/do_nmb_sim.md).

## Examples

``` r
get_inbuilt_cutpoint_methods()
#> [1] "all"              "none"             "value_optimising" "youden"          
#> [5] "cost_minimising"  "prod_sens_spec"   "roc01"            "index_of_union"  
```
