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

## Notes for GPU Usage

To have access to the GPUs when running docker you will need all the 
relevant drivers installed and `nvidia-docker`:

  https://github.com/NVIDIA/nvidia-docker

Before building the Dockerfile, you will (potentially) need to change 
line 280:

    ENV GPU 61

The number here is the compute compatability code for your GPU.  To 
find what GPU is installed on your computer just use:

    nvidia-smi -L

You can then find the relevant code by looking up your GPU either 
[here](https://arnon.dk/matching-sm-architectures-arch-and-gencode-for-various-nvidia-cards/) 
or [here](https://en.wikipedia.org/wiki/CUDA#GPUs_supported).  On my machine 
I have a NVIDIA GeForce GTX 1080 Ti, so looking it up I see that the relevant 
code is `sm_61` or 6.1, so the number I put on line 280 is 61.


## Other Notes

Besides the GPU code, everything else should be good to go and ... work.
However, if something does NOT work for you, please just let me know.



 



