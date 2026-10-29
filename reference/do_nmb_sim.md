# Do the predictNMB simulation, evaluating the net monetary benefit (NMB) of the simulated model.

Do the predictNMB simulation, evaluating the net monetary benefit (NMB)
of the simulated model.

## Usage

``` r
do_nmb_sim(
  sample_size,
  n_sims,
  n_valid,
  sim_auc,
  event_rate,
  cutpoint_methods = get_inbuilt_cutpoint_methods(),
  fx_nmb_training,
  fx_nmb_evaluation,
  meet_min_events = TRUE,
  min_events = NA,
  show_progress = FALSE,
  cl = NULL
)
```

## Arguments

- sample_size:

  Sample size of training set. If missing, a sample size calculation
  will be performed and the calculated size will be used.

- n_sims:

  Number of simulations to run.

- n_valid:

  Sample size for evaluation set.

- sim_auc:

  Simulated model discrimination (AUC).

- event_rate:

  Simulated event rate of the binary outcome being predicted. Also known
  as prevalence.

- cutpoint_methods:

  A value or vector of cutpoint methods to include. Defaults to use the
  inbuilt methods:

  - "all" = treat all patients (cutpoint = 0)

  - "none" = treat no patients (cutpoint = 1)

  - "value_optimising" = select the cutpoint that maximises NMB

  - "youden" = select cutpoint based on the Youden index, also known as
    the J-index (sensitivity + specificity - 1)

  - "cost_minimising" = select the cutpoint that minimises expected
    value of costs

  - "prod_sens_spec" = product of sensitivity and specificity
    (sensitivity \* specificity)

  - "roc01" = selects the closest threshold to the (0,1) point on the
    ROC curve

  User-defined cutpoint methods can be used by passing the name of a
  function that takes the following arguments:

  - `predicted` (predicted probabilities)

  - `actual` (the actual, binary outcome)

  - `nmb` (a named vector containing NMB values assigned to each
    predicted class (i.e. c("TP" = -3, "TN" = 0, "FP" = -1, "FN" = -4)))

  See
  [`?get_thresholds`](https://docs.ropensci.org/predictNMB/reference/get_thresholds.md)
  for an example of a user-defined cutpoint function.

- fx_nmb_training:

  Function or `NMBsampler` that returns a named vector of NMB assigned
  to classifications used for obtaining cutpoint on training set.

- fx_nmb_evaluation:

  Function or `NMBsampler` that returns a named vector of NMB assigned
  to classifications used for obtaining cutpoint on evaluation set.

- meet_min_events:

  Whether or not to incrementally add samples until the expected number
  of events (`sample_size * event_rate`) is met. (Applies to sampling of
  training data only.)

- min_events:

  The minimum number of events to include in the training sample. If
  less than this number are included in sample of size `sample_size`,
  additional samples are added until the `min_events` is met. The
  default (`NA`) will use the expected value given the `event_rate` and
  the `sample_size`.

- show_progress:

  Logical. Whether to display a progress bar. Requires the `pbapply`
  package.

- cl:

  A cluster made using
  [`parallel::makeCluster()`](https://rdrr.io/r/parallel/makeCluster.html).
  If a cluster is provided, the simulation will be done in parallel.

## Value

Returns a `predictNMBsim` object.

## Details

This function runs a simulation for a given set of inputs that represent
a healthcare setting using model-guided interventions.  
  
The arguments `fx_nmb_training` and `fx_nmb_evaluation` should be
functions that capture the treatment being used, its costs and
effectiveness, and the costs of the outcome being treated/prevented.  
  
Both of these are functions that return a named vector of NMB values
when called and are used for obtaining and evaluating cutpoints,
respectively. For example, the following function returns the
appropriately named vector.  
  
`get_nmb <- function() c("TP" = -3, "TN" = 0, "FP" = -1, "FN" = -4)`

There is a helper function,
[`get_nmb_sampler()`](https://docs.ropensci.org/predictNMB/reference/get_nmb_sampler.md),
to help you create these.

## Examples

``` r
# \donttest{
get_nmb <- function() c("TP" = -3, "TN" = 0, "FP" = -1, "FN" = -4)
do_nmb_sim(
  sample_size = 200, n_sims = 50, n_valid = 10000, sim_auc = 0.7,
  event_rate = 0.1, fx_nmb_training = get_nmb, fx_nmb_evaluation = get_nmb
)
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
