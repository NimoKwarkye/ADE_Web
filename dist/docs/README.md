# ADE Simulator

ADE Simulator models one-dimensional advection, dispersion, and adsorption–desorption in porous media.
The C++ desktop and WebAssembly applications share the same ImGui interface and solver.

## Getting started

1. Install the Windows x64 MSI, or open the web app.
2. Create a project or open a saved project from the startup list. Use Import INI parameters for an INI file, or set inputs in Config.
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

The available package is ADE Simulator 0.1.6 for Windows x64.
It includes runtime dependencies and assets, requires administrator permission to install,
and is unsigned. SHA256SUMS.txt accompanies the installer.


## Organizing and moving projects

Add an optional description when creating a project. The library shows descriptions and local creation dates and times; search by name or description, or choose **Edit description** to update notes.

Choose **Download** to save a portable `.adeproject` backup containing the latest saved parameters, observations, results and project details (up to 48 MiB). Desktop users choose a folder; browsers download the file. **Import project from disk** creates a separate project from this file, preserving its original name, description and creation date. Save changes before downloading from the library.

The SVG trash button asks for confirmation before permanently deleting a project and its saved revisions on this device. Downloaded backups are kept. Browser storage remains local to the browser and site; use download/import to transfer projects between devices.


Version 0.1.6 fixes reopening and downloading saved results with extremely small, finite concentrations. Existing project files remain compatible; the fix preserves these values without rounding them to zero. Description dialogs retain a stable width while fitting their height to content.
