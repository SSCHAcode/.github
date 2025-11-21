# Release 1.5

We are thrilled to announce the release of version 1.5 of our code, featuring significant enhancements and exciting improvements:

The release 1.5 finally solves all the compatibility issues with the most recent version of python, allowing it to run on python 3.13. This involves a new build system based on meson which should make installation much easier.


# Release Notes – Version 1.5

## Highlights
- **Meson build system**
  - Migration to the **Meson build** system.
  - Dropped the deprecated installation via `numpy.distutils`.
  - Full compatibility with **Python 3.13** and **spglib ≥ 2.2**.

## New Features
- **LO–TO splitting in interpolation**
  - Added support for **LO–TO splitting** in the `Interpolate` method.
  - Enables computation of harmonic free energies for **polar materials** on dense **q-grids**.
- **Local cluster submission**
   - Comply with the new clusters that require 2FA by allowing a SSCHA job to run directly on a cluster and submit and manage other jobs without requiring an active ssh connection to the cluster.  This can be achieved with the LocalCluster class.

## Enhancements
- **Acoustic Sum Rule for 1D systems**
  - Implemented enforcement of the **acoustic sum rule** for **1D materials**.
  
Tons of minor bugfixes and small improvements!

You can update with the following command
```
pip install -U cellconstructor python-sscha tdscha --no-cache
```
Note: it is important to update both cellconstructor and python-sscha, as they both require to be at the latest version to interoperate.


We're excited about this release and the opportunities it offers. Your feedback is invaluable to us, and we look forward to your continued support and engagement with our code.

Thank you for being a part of this journey.

Best regards,
Lorenzo Monacelli, on behalf of the developers


