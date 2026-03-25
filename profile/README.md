# Release 1.6

## Overview
SSCHA 1.6 introduces major optimizations and new computational capabilities that deliver substantial speedups for both standard SSCHA minimization and the calculation of the free energy Hessian (now possible with fourth order on large systems without requiring prohibitive memory and time, and also parallelized), as well as for the TDSCHA spectral function.
The two major updates come from the packages CellConstructor and tdscha. This release introduces major performance optimizations and new computational capabilities, most notably the **q-space implementations** of the Lanczos and Hessian algorithms that dramatically accelerate calculations for periodic systems.


## Highlights 

### 🚀 Performance Improvements
- **QSpaceLanczos: Q-Space Spectral Calculations**. A new module implementing the TDSCHA Lanczos algorithm in the Bloch (q-space) basis, exploiting momentum conservation for massive performance gains (N_q^2 compared to version 1.5).
- **QSpaceHessian: Fast Free Energy Hessian**. The **fastest and most memory-efficient** method in the SSCHA ecosystem for computing the full anharmonic free energy Hessian, including fourth-order contributions. The free energy Hessian calculation now scales as O(N_q^2) compared to O(N_q^6) of the original implementation.
- **Symmetrize Optimization**: Vectorized coordinate conversions and q-star copying operations, resulting in up to **25% speedup** for symmetry operations on typical systems. Significant Speedup of the SSCHA minimization.
- **DiagonalizeSupercell Optimization**: Major performance boost through vectorized operations and pre-computed phase factors, significantly reducing computation time for large supercell diagonalizations. Also this subroutine is massively called during the SSCHA minimization, resulting in a significative speedup.

### Migration Guide

No code changes required. Existing scripts will continue to work unchanged.

To benefit from new features:

1. **For faster Hessian calculations:** Replace `ensemble.get_free_energy_hessian()` with `QSpaceHessian` from `tdscha`
2. **For large-supercell spectra:** Use `QSpaceLanczos` instead of `Lanczos`, which will achieve an N_q^2 speedup.


### 🐛 Bug Fixes

- **Fortran Compiler Compatibility**: Fixed acoustic sum rule errors that occurred with newer Fortran compilers (gfortran 15+), ensuring compatibility with modern HPC environments.
- **ForceTensor Error Messages**: Improved error handling and messages for incorrect file formats in both second-order and third-order force tensors.
- **DiagonalizeSupercell**: Fixed the `lo_to_split` argument handling and a missing timer variable that caused NameError exceptions.
- **Spglib Integration**: Removed the restrictive `spglib<=2.2` requirement and fixed symmetrization bugs for better compatibility with newer spglib versions.

### ✨ New Features

- **get_primitive_cell() Method**: New method in the `Structure` class to easily obtain the primitive cell from any crystal structure, simplifying workflow for high-throughput calculations.

### 🔧 Improvements

- **Timer Support**: Added optional `timer` parameter to `SymmetrizeFCQ`, `SetupQPoint`, `SymmetrizeDynQ`, `ApplyQStar`, and `ImposeSumRule` functions for detailed performance profiling.
- **Fortran Module Updates**: Enhanced `symdynph_gq_new.f90` to properly enforce symmetries after small-group symmetrization.

## Detailed Changes

### Commits since v1.5

1. **684036b** - Optimize SymmetrizeFCQ with vectorized coordinate conversions and q-star copying
2. **d7db321** - Add get_primitive_cell() method to Structure class
3. **e5f5fff** - Fix NameError: add missing t_main_loop_start timer in DiagonalizeSupercell_slow
4. **b462c05** - Optimize generate_supercell with O(N) set_tau_fast Fortran routine
5. **c49db94** - Optimize DiagonalizeSupercell with vectorized operations and pre-computed phase factors
6. **8da226c** - Fixed a typo
7. **697666c** - Fixed an error in the lo_to_split argumento of DiagonalizeSupercell
8. **9415f83** - Fixed the error message when the fileformat is wrong in the ForceTensor
9. **a7c9f46** - Fixed a missing error message in the file_format
10. **502225d** - Fix another fortran error in third order
11. **6be1e8e** - Merge pull request #118 from SSCHAcode/fix_fortran_compiler
12. **4228fd4** - New version. Fixed the error with older fortran compilers
13. **dd6fd10** - Fixed the error of the acoustic sum rule error for using a new fortran compiler
14. **4a3bb93** - Fixed another spglib test
15. **6e014e7** - Removed the requirement for spglib<=2.2
16. **d4a100a** - Merge pull request #117 from SSCHAcode/spglib_fix
17. **62649f2** - Fix a spelling
18. **cc4fe44** - Fixed a bug
19. **49f36b6** - Fixed the spglib symmetrization
20. **4045be7** - Fixing the interpolate mesh subroutine

## Compatibility

- **Python**: 3.8+
- **NumPy**: 1.20+
- **ASE**: Compatible with latest versions
- **Fortran Compiler**: gfortran 15+ and Intel Fortran
- **Spglib**: Now compatible with all recent versions (removed <=2.2 restriction)

## Upgrade Notes

This release is fully backward compatible. No API changes were made - all optimizations maintain the existing function signatures and behavior. Users can upgrade seamlessly and immediately benefit from the performance improvements.

## Contributors

Thanks to all contributors who made this release possible, particularly for the performance optimizations and compiler compatibility fixes.

---

