# Parameter sweeps and Monte Carlo propagation

Both workflows are under **Tools > Custom Simulations** and display their output in the **Sensitivity** plot view, alongside the original breakthrough and mass-balance information. Dialogs are modal. Closing a dialog does not start an analysis.

## Parameter sweep (SSE)

Load observations, select one or two parameters, and specify minimum, maximum and **Steps (sample count)**. Steps includes both endpoints: 21 steps means 21 model runs for one parameter, or 441 for two parameters with 21 steps each. The maximum grid is 10,000 runs. A logarithmic range samples geometrically and requires a strictly positive minimum. All ranges must respect the model's physical bounds.

Each run evaluates predictions at the observation times and sums the squared concentration residuals (unweighted SSE). One parameter produces a line plot; two produce a heatmap whose axes are the actual parameter values. Logarithmic spacing is represented by logarithmic axes and the correct cell boundaries. Hover a cell for its parameter values and SSE. Lower SSE means a better match. This is a parameter sweep, not a normalized sensitivity coefficient or an optimizer.

## Monte Carlo propagation

Select parameters and enter their means and standard deviations, the number of samples (2–10,000), and a random seed. Box–Muller draws are independent across selected parameters. A zero standard deviation fixes a selected parameter at its mean. Unselected parameters keep their original values.

Draws outside physical bounds are rejected and resampled, rather than folded or clipped. Therefore these are **truncated normal distributions**: the entered mean and SD describe the normal before truncation, and the accepted distribution may have different moments near a physical boundary. Excessive rejection produces a useful error instead of an unbounded loop. The log reports rejected draws.

A baseline run establishes the display coordinate range, followed by the requested number of sampled runs. Observations are optional and do not limit the simulated breakthrough resolution. Each curve is linearly interpolated to 201 common time or pore-volume coordinates; values increment a 201 × 128 concentration histogram. In pore-volume mode, each sampled run uses its own pore-volume coordinates. Curves are never extrapolated; coverage is reported when fewer runs reach part of the display range.

The density uses an inverted grayscale palette for light/dark themes. **Log density**, enabled by default, displays log(1 + count), so zero remains zero and dense plateaus do not hide lower-density regions. Counts are retained unchanged. Toggle it off to show raw counts. The median and 2.5th/97.5th percentile curves use the underlying interpolated samples, not histogram bins. This is a **95% pointwise simulation interval**, conditional on the supplied independent input distributions, not a simultaneous confidence band or a calibrated estimate of parameter uncertainty. Sparse samples and incomplete coverage make the percentiles less stable.

## Model state, cancellation and errors

Analyses use isolated copies and the configured solver interface, so original parameters, observations, breakthrough curves and mass balances remain unchanged on completion, Stop or failure. Stop retains completed runs; unfinished sweep cells remain blank. Results replace the previous analysis only when the workflow returns successfully and are currently session-only. Solver errors are displayed in Logs. Scenarios and flow interruptions remain active: an explicit scenario override takes precedence over a selected parameter from that scenario's time onward.

## Browser file selection

The project importer accepts multiple project archives. **File > Download exported files** provides checkboxes, **Select all**, **Deselect all**, and **Download selected**. One file downloads directly; multiple files download as one ZIP with export subfolders preserved, avoiding browser restrictions on repeated automatic downloads. Browser exports are temporary until downloaded.
