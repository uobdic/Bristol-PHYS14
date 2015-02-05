Bristol-CMS-PHYS14
==================

# soolin
soolin is both a condor submission machine as well as testing ground for software development.
It comes with Scientific Linux (6.6):
```shell
cat /etc/redhat-release 
Scientific Linux release 6.6 (Carbon)
```
updated GCC (4.8.2)
```shell
scl enable devtoolset-2 bash
gcc --version
```

It has the following hardware:
 - 2 x Intel(R) Xeon(R) CPU E5405  @ 2.00GHz
 - 16 GB of RAM (DIMM DDR2 667 MHz (1.5 ns))
 - around 4.1 TB of non-backed up file storage (on mount /storage)

It has also access to both our GPFS (/gpfs_phys) and HDFS (/hdfs) storage

## software
soolin comes with CVMFS, which means that software for the ATLAS, ALICE, CMS, ILC and LHCb experiments is available under (/cvmfs). Since it is an automount the folder you are looking for (e.g. /cvmfs/cms.cern.ch) might be not mounted. Just try to access it and it will appear.
Furthermore custom software compilations are available under /software

### ROOT (compiling ROOT on soolin)
```shell
scl enable devtoolset-2 bash
# get ROOT source
# select git tag you want
git tag -l
git checkout v5-34-25
./configure --enable-roofit --enable-minuit2 --enable-builtin-freetype
make jobs=4
```
