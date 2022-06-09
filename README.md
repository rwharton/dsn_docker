# DSN Docker Files

Here we provide two docker files to recreate the software environment 
used to process DSN pulsar/FRB data.  If you have (and want to use) 
GPU enabled software use `gpu/Dockerfile`, otherwise use the 
`cpu/Dockerfile`.  

## Software Packages + Libraries

Both Dockerfiles build on an ubuntu 20.04 base and have 

* FFTW3
* CFITSIO
* PGPLOT 
* ds9
* fv
* PSRCAT
* tempo (with DSN additions to obsys.dat)
* tempo2 (with DSN additions to obervatory file)
* prepfil
* epsic
* psrchive
* SIGPROC
* sigprocpy
* dspsr
* PSRSALSA
* PRESTO 3
* psrfits2psrfits
* pyslalib
* PolyChordLite
* TempoNest
* plotres
* fitorbit
* pulse portraiture 
* tempoutils
* prepfil
* your

The GPU enabled version additionally has 

* cuda 11.2.2
* dedisp
* PSRDADA
* Heimdall
* fetch

## 



