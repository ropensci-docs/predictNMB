# Screen many simulation inputs: a parent function to `do_nmb_sim()`

Runs
[`do_nmb_sim()`](https://docs.ropensci.org/predictNMB/reference/do_nmb_sim.md)
with a range of inputs.

## Usage

``` r
screen_simulation_inputs(
  sample_size,
  n_sims,
  n_valid,
  sim_auc,
  event_rate,
  cutpoint_methods = get_inbuilt_cutpoint_methods(),
  fx_nmb_training,
  fx_nmb_evaluation,
  pair_nmb_train_and_evaluation_functions = FALSE,
  meet_min_events = TRUE,
  min_events = NA,
  show_progress = FALSE,
  cl = NULL
)
```

## Arguments

- sample_size:

  A value (or vector of values): Sample size of training set. If
  missing, a sample size calculation will be performed and the
  calculated size will be used.

- n_sims:

  A value (or vector of values): Number of simulations to run.

- n_valid:

  A value (or vector of values): Sample size for evaluation set.

- sim_auc:

  A value (or vector of values): Simulated model discrimination (AUC).

- event_rate:

  A value (or vector of values): simulated event rate of the binary
  outcome being predicted.

- cutpoint_methods:

  cutpoint methods to include. Defaults to use the inbuilt methods. This
  doesn't change across calls to
  [`do_nmb_sim()`](https://docs.ropensci.org/predictNMB/reference/do_nmb_sim.md).

- fx_nmb_training:

  A function or `NMBsampler` (or list of) that returns named vector of
  NMB assigned to classifications use for obtaining cutpoint on training
  set.

- fx_nmb_evaluation:

  A function or `NMBsampler` (or list of) that returns named vector of
  NMB assigned to classifications use for obtaining cutpoint on
  evaluation set.

- pair_nmb_train_and_evaluation_functions:

  `logical`. Whether or not to pair the lists of functions passed for
  `fx_nmb_training` and `fx_nmb_evaluation`. If two treatment strategies
  are being used, it may make more sense to pair these because selecting
  a value-optimising or cost-minimising threshold using one strategy but
  evaluating another is likely unwanted.

- meet_min_events:

  Whether or not to incrementally add samples until the expected number
  of events (`sample_size * event_rate`) is met. (Applies to sampling of
  training data only.)

- min_events:

  A value: the minimum number of events to include in the training
  sample. If less than this number are included in sample of size
  `sample_size`, additional samples are added until the min_events is
  met. The default (`NA`) will use the expected value given the
  `event_rate` and the `sample_size`.

- show_progress:

  Logical. Whether to display a progress bar.

- cl:

  A cluster made using
  [`parallel::makeCluster()`](https://rdrr.io/r/parallel/makeCluster.html).
  If a cluster is provided, the simulation will be done in parallel.

## Value

Returns a `predictNMBscreen` object.

## Examples

``` r

# Screen for optimal cutpoints given increasing values of
# model discrimination (sim_auc)
# \donttest{
get_nmb <- function() c("TP" = -3, "TN" = 0, "FP" = -1, "FN" = -4)
sim_screen_obj <- screen_simulation_inputs(
  n_sims = 50, n_valid = 10000, sim_auc = seq(0.7, 0.9, 0.1),
  event_rate = 0.1, fx_nmb_training = get_nmb, fx_nmb_evaluation = get_nmb
)
# }
```
