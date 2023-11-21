# Release 1.4

We are thrilled to announce the release of version 1.4 of our code, featuring significant enhancements and exciting improvements:

## Key Highlights
 - Code Speedup: In this release, we have achieved a remarkable speedup, with performance gains ranging from 10x to 100x in specific scenarios. This substantial acceleration is due to the new integration with Julia and a comprehensive algorithm rewrite, enabling all calculations in Fourier space during the free energy minimization.
 - Enhanced Code Parallelization: Version 1.4 introduces improved code parallelization. This enhancement extends to the SSCHA minimization (now parallelizing both the evaluation of energies and forces, the gradient, and stochastic reweighting utilizing MPI) and the spectral function.
 - AiiDA Integration with Quantum Espresso: Thanks to the contributions of Lorenzo Bastonero (@bastonero), the sscha code now offers a seamless integration with AiiDA and Quantum Espresso. In this way, the SSCHA leverages AiiDA to deal with cluster communication, allowing easier integration with non-SLURM or more exotic HPC configurations. 

Do not worry; the old plain cluster module remains a supported feature, and **we care about backward compatibility**, so there is no need to change your input scripts or install AiiDA to submit on a cluster!

## Detailed changes
In addition to these significant advances, we have diligently addressed various minor issues and bugs. A more complete list follows.

Julia is not a mandatory requirement to run the new version of the SSCHA. However, while the code offers a fallback mode if Julia is unavailable, we strongly recommend having Julia installed, as failure to do so may result in a significant slowdown, reducing performance gains achieved through this release (without julia the code utilizes the same implementation as in version 1.3).

For updated installation instructions and to experience the full benefits of release 1.4, visit http://sscha.eu/download/
To update the code from PyPi:
```
pip install -U cellconstructor python-sscha tdscha
```
Note: it is important to update both cellconstructor and python-sscha, as they both require to be at the latest version to interoperate.


We're excited about this release and the opportunities it offers. Your feedback is invaluable to us, and we look forward to your continued support and engagement with our code.

Thank you for being a part of this journey.

Best regards,
Lorenzo Monacelli, on behalf of the developers

