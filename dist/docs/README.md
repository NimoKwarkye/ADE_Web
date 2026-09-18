# ADE Simulator

ADE Simulator models one-dimensional advection, dispersion, and adsorption–desorption in porous media.
The C++ desktop and WebAssembly applications share the same ImGui interface and solver.

## Getting started

1. Install the Windows x64 MSI, or open the web app.
2. Create a project or open a saved project from the startup list. Use Import INI parameters for an INI file, or enter inputs in the tabbed Project configuration dialog. New projects require valid settings before Save and continue.
3. Press Run to compute. Transport plots update live; Stop cancels a running job.
4. Review Log for messages and Info for diagnostics. Use File → Save Project to keep your work.

## Files

Model parameters use INI; observation data and result exports use CSV.
In the browser, save results and use File → Download exported files before refreshing.
Browser storage for imported/exported files is temporary.
Saved projects retain parameters, observations and results on this device and browser.
Use File → Save Project before closing; clearing site data removes these projects.
File → Projects / New Project lets you save or discard changes before switching projects.

## Browser requirements

Use a modern browser supporting WebGL, WebAssembly threads, and service workers.
The first visit may reload once to enable cross-origin isolation.
Docked windows remain within the browser canvas.

## Research use

Review model assumptions, convergence and mass balance for each application.
Regression tests are not scientific validation for every scenario.

## Desktop package

The available package is ADE Simulator 0.1.13 for Windows x64.
It includes runtime dependencies and assets, requires administrator permission to install,
and is unsigned. SHA256SUMS.txt accompanies the installer.


## Organizing and moving projects

Add an optional description when creating a project. The library shows descriptions and local creation dates and times; search by name or description, or choose **Edit description** to update notes.

Choose **Download** to save a portable `.adeproject` backup containing the latest saved parameters, observations, results and project details (up to 48 MiB). Desktop users choose a folder; browsers download the file. **Import project from disk** creates a separate project from this file, preserving its original name, description and creation date. Save changes before downloading from the library.

The SVG trash button asks for confirmation before permanently deleting a project and its saved revisions on this device. Downloaded backups are kept. Browser storage remains local to the browser and site; use download/import to transfer projects between devices.


Version 0.1.13 fixes reopening and downloading saved results with extremely small, finite concentrations. Existing project files remain compatible; the fix preserves these values without rounding them to zero. Description dialogs retain a stable width while fitting their height to content.


## System projects

Projects included with the app are labeled **SYSTEM PROJECT**. They are maintained by application releases and can share names with your personal projects. Open them to explore or run the model, or download them normally. Choose **Make a copy**, or **File > Save personal copy** while working, to keep an editable project in your own library. Personal copies are preserved when the bundled originals are updated or removed. System descriptions and deletion are managed by releases.

System entries appear when the application maintainer includes bundled projects in a release.


### Project configuration

Configuration is a non-dockable modal with General, Discretization, Transport, Sorption, and Degradation tabs. General contains observation reset, noise controls, pore-volume units, and execution settings. Discretization contains space and time properties. New projects open this dialog automatically; validation errors must be corrected before Save and continue. Reopen it using Configuration > Project settings. Existing projects retain the normal File > Save Project workflow.


## Appearance

Use the sun/moon button at the top right of the project list to switch themes, or choose **Edit > Theme** within a project. The choice is saved immediately for this device and restored when the application or browser is reopened. Browser preferences belong to the current site and browser; clearing site data resets them.

Both themes define readable text, status messages, plot backgrounds, axes, legends, and distinct prediction/observation/analysis colors. The light theme uses pale slate surfaces, white plots, dark text, and blue accents. Theme changes do not modify saved projects.


## Calibration and appearance update

**Tools > Optimizer > Adaptive Simulated Annealing** opens a parameter-selection window with editable bounds and a Search settings tab. Load observations, choose the fitted parameters, review their bounds, and start the search. Adaptive proposals, reheating, and optional local refinement reduce wasted model evaluations. The Calibration view shows best SSE; Logs show termination and fitted values. Stop retains the best completed fit. Save the project to keep fitted parameters. Performance depends on the model and bounds; the search does not guarantee a global optimum.

The dark theme now uses neutral charcoal and gray surfaces. Light-theme backgrounds are darker so the lighter plot frames stand out; text and plot-series contrast remain checked in both modes.

## Parameter sweeps and Monte Carlo propagation

Tools > Custom Simulations now offers one/two-parameter SSE sweeps with linear or logarithmic ranges, plus Monte Carlo input-error propagation using independent truncated-normal draws. Results appear in Sensitivity. Monte Carlo displays breakthrough density and a pointwise 95% simulation interval; original settings and breakthrough results are retained. Browser exports support Select all, Deselect all and a single ZIP download of selected files. See [the analysis guide](parameter-analysis.md).
