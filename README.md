EUPS packaged version of Mike Jarvis' TreeCorr

https://github.com/rmjarvis/TreeCorr/archive/v3.2.3.tar.gz

# Explanatory Notes
# 2017-07-27: Michael Wood-Vasey
1. We have specifically pinned to the 3.2.3 version
to avoid the `libffi`, `cffi`, `pyfits` dependencies introduced in more recent versions.  These dependencies make sense for `TreeCorr` qua `TreeCorr`, but add dependencies to the LSST validate_drp stack that we wish to avoid for now.

In the future we may update.  `libffi` and `cffi` should be set up as shim packages, particularly because `libffi` is available on many systems.  The `pyfits` dependency we would have to step around because we do wish to avoid adding a 3rd (4th?) different python FITS interface to the LSST stack.

For more discussion see
https://jira.lsstcorp.org/browse/RFC-296

If performance becomes an issue, we may want to update to more recent TreeCorr.  But currently basic I/O from the catalog files dominates any in-memory correlation calculations.  Thus until it becomes a performance bottleneck, I judge that the dependency minimization is the better option for the LSST validate_drp stack.

2. "pandas" could be a setupOptional dependency.
If pandas is not present, then reading of ASCII catalogs will be slower.
But because we don't use that functionality, I've left that out as a dependency.
