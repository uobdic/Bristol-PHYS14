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

### CMSSW (latest)
In order to enable the CMSSW commands first source
```shell
. /cvmfs/cms.cern.ch/cmsset_default.sh
```
and set SCRAM_ARCH
```shell
# this refers to the slc* folders in /cvmfs/cms.cern.ch
export SCRAM_ARCH=slc6_amd64_gcc491
```
You can get a list of available version by doing
```shell
scram list CMSSW
```
Pick the one you want (latest CMSSW_7_4_0_pre6_ROOT6 and CMSSW_7_4_0_pre6 [ROOT 5.34.X]) and get it:
```shell 
cmsrel CMSSW_7_4_0_pre6_ROOT6
cd CMSSW_7_4_0_pre6_ROOT6/src
# enable CMS environment
cmsenv
# put your code here and use your usual build methods
```
An example of such a setup can be found here: https://github.com/BristolTopGroup/AnalysisSoftware/

Additional CMSSW tools can be enabled using the ```scram setup <tool>``` command.
For a full list of available tools:
```shell
scram tool list
```


