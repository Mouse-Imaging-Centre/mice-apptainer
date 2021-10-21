# MICe Singularity containers

This repository contains a [Singularity](https://sylabs.io/guides/latest/user-guide) definition file to build a Singularity container containing a software suite for neuroimaging, and particularly tools used in-house at the Mouse Imaging Centre.  For a complete list of libraries and tools included, see the definition file itself.

To use an existing container image, use `singularity shell`, `singularity exec`, etc., e.g.:

```
$ singularity shell --bind /projects,/scratch /path/to/container.sif
```

or

```
$ singularity exec --bind /projects,/scratch /path/to/container.sif <...cmd...>
```

If you need to build a container from this repository, use `singularity build`, e.g.

```
$ singularity build /path/to/output/MICe-container.sif MICe-container.def
```

At the moment everything is installed from Debian/Ubuntu/CRAN/PyPI repos or compiled by hand from source.  In the future some other methods for building a container (e.g. Nix or Spack) might be usable.

Some limitations:
 - Submitting to a grid scheduler (Slurm, Torque, etc.) from inside a container likely won't work.  In particular, don't expect Pydpiper and RMINC grid backends to work.  This should be addressed in an upcoming Pydpiper release.  Of course, activating a container within a batch job is fine.
 - GL/CUDA functionality may or may not work depending on the host system.

This container is loosely based on Vlad's minc-toolkit-containers repository, with a few differences:
 - everything updated
 - much more software, e.g., FSL, openEMS, Nipype, etc.
 - no Python 2 support
 - we don't provide a Docker recipe, but you can convert the definition and/or image to Docker format if necessary
 - the container is built in a single step rather than relying on an intermediate image being uploaded to SingularityHub (which no longer exists)
 - the Git repository itself is rolling and doesn't attempt to provide allow building containers using previous versions of Ubuntu, the MINC toolkit, or other software.  To use older releases, use the Git history or an existing container.
