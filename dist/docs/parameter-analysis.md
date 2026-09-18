# Parameter sweeps and Monte Carlo propagation

Both workflows are under **Tools > Custom Simulations** and display their output in the **Sensitivity** plot view, alongside the original breakthrough and mass-balance information. Dialogs are modal. Closing a dialog does not start an analysis.

## Parameter sweep (SSE)

Load observations, select one or two parameters, and specify minimum, maximum and **Steps (sample count)**. Steps includes both endpoints: 21 steps means 21 model runs for one parameter, or 441 for two parameters with 21 steps each. The maximum grid is 10,000 runs. A logarithmic range samples geometrically and requires a strictly positive minimum. All ranges must respect the model's physical bounds.

Each run evaluates predictions at the observation times and sums the squared concentration residuals (unweighted SSE). One parameter produces a line plot; two produce a heatmap whose axes are the actual parameter values. Logarithmic spacing is represented by logarithmic axes and the correct cell boundaries. Hover a cell for its parameter values and SSE. Lower SSE means a better match. This is a parameter sweep, not a normalized sensitivity coefficient or an optimizer.

## Monte Carlo propagation

Select parameters and enter their means and standard deviations, the number of samples (2–100,000), and a random seed. Box–Muller draws are independent across selected parameters. A zero standard deviation fixes a selected parameter at its mean. Unselected parameters keep their original values.

Draws outside physical bounds are rejected and resampled, rather than folded or clipped. Therefore these are **truncated normal distributions**: the entered mean and SD describe the normal before truncation, and the accepted distribution may have different moments near a physical boundary. Excessive rejection produces a useful error instead of an unbounded loop. The log reports rejected draws.

A baseline run establishes the display coordinate range, followed by the requested number of sampled runs. Observations are optional and do not limit the simulated breakthrough resolution. Each curve is linearly interpolated to 201 common time or pore-volume coordinates; values increment a concentration histogram at those 201 coordinates. In pore-volume mode, each sampled run uses its own pore-volume coordinates. Curves are never extrapolated; coverage is reported when fewer runs reach part of the display range.

The density uses an inverted grayscale palette for light/dark themes. **Log density**, enabled by default, displays log(1 + count), so zero remains zero and dense plateaus do not hide lower-density regions. Counts are retained unchanged. Toggle it off to show raw counts. For requested sample counts up to 10,000, the median and 2.5th/97.5th percentiles are calculated exactly from retained interpolated samples (with a 128-bin density display). Above 10,000, samples feed a streaming 256-bin histogram and percentile estimates are interpolated within its bins. The concentration range expands as needed, merging aligned bins without losing counts. The displayed bin width indicates the approximation resolution. Large runs do not retain the full ensemble. This is a **95% pointwise simulation interval**, conditional on the supplied independent input distributions, not a simultaneous confidence band or a calibrated estimate of parameter uncertainty. Sparse samples and incomplete coverage make the percentiles less stable.

## Model state, cancellation and errors

Analyses use isolated copies and the configured solver interface, so original parameters, observations, breakthrough curves and mass balances remain unchanged on completion, Stop or failure. Stop retains completed runs; unfinished sweep cells remain blank. Each workflow retains its latest successful result separately. Save the project using the Save icon beside Run to persist both analyses, including partial results after Stop. Reopening restores the results; a selector switches between them when both are available. Older projects remain compatible. Solver errors are displayed in Logs. Scenarios and flow interruptions remain active: an explicit scenario override takes precedence over a selected parameter from that scenario's time onward.

## Browser file selection

The project importer accepts multiple project archives. **File > Download exported files** provides checkboxes, **Select all**, **Deselect all**, and **Download selected**. One file downloads directly; multiple files download as one ZIP with export subfolders preserved, avoiding browser restrictions on repeated automatic downloads. Browser exports are temporary until downloaded.

## Completed curves and exports

The breakthrough plot in the Sensitivity view overlays up to 100 completed runs, refreshed while the analysis runs. A bounded representative sample is used after the first 100 runs; each preview retains at most 201 points. The Completed runs checkbox hides or shows these curves. These previews are independent of the samples or bins used for percentile calculations.

The data export dialog offers parameter-sweep and Monte Carlo exports. Sweep CSV includes parameter coordinates, SSE and completion status. Monte Carlo CSV files include the lower/median/upper interval, contributing-run counts, calculation method and raw density counts. Both can export their retained breakthrough previews, with time and pore-volume coordinates. Metadata records the analysis settings and approximation details. Browser users then download these files through File > Download exported files.
