# ADE Simulator

ADE Simulator models one-dimensional advection, dispersion, and adsorption–desorption in porous media.
The C++ desktop and WebAssembly applications share the same ImGui interface and solver.

## Getting started

1. Install the Windows x64 MSI, or open the web app.
2. Load an INI file with Tools → Load Model Parameters, or set inputs in Config.
3. Press Run to compute. Transport plots update live; Stop cancels a running job.
4. Review Log for messages and Info for diagnostics.

## Files

Model parameters use INI; observation data and result exports use CSV.
In the browser, save results and use File → Download exported files before refreshing.
Browser storage for imported/exported files is temporary.

## Browser requirements

Use a modern browser supporting WebGL, WebAssembly threads, and service workers.
The first visit may reload once to enable cross-origin isolation.
Docked windows remain within the browser canvas.

## Research use

Review model assumptions, convergence and mass balance for each application.
Regression tests are not scientific validation for every scenario.

## Desktop package

The available package is ADE Simulator 0.1.0 for Windows x64.
It includes runtime dependencies and assets, requires administrator permission to install,
and is unsigned. SHA256SUMS.txt accompanies the installer.
