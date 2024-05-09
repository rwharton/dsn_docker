# DSN Docker Files

Here we provide two docker files to recreate the software environment 
used to process DSN pulsar/FRB data.  If you have (and want to use) 
GPU enabled software use `gpu/Dockerfile`, otherwise use the 
`cpu/Dockerfile`.  Note that our workflow is to use the Dockerfile to 
create a docker image, then convert that to a singularity file.  This 
is a bit roundabout and probably isn't the right strategy for everyone.

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

## Notes for GPU Usage

To have access to the GPUs when running docker you will need all the 
relevant drivers installed and `nvidia-docker`:

  https://github.com/NVIDIA/nvidia-docker

Before building the Dockerfile, you will (potentially) need to change 
line 283:

    ENV GPU 86

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


## Dockerfile -> Singularity Image

When you are ready to build the docker image, go to the directory 
containing `Dockerfile` and run

    docker build -t image_name .

where `image_name` is just whatever you want the image to be called. 
The `.` just tells docker to look in the current directory for 
`Dockerfile`.

This will probably take a while since it needs to download and 
run the installation of all our software.  Generally should take 
maybe 30 min to an hour.

Once the image is successfully built, you can run

    docker images

to see what images are built on the system.  You should see something 
like this:

    REPOSITORY        TAG              IMAGE ID       CREATED         SIZE
    image_name        latest           ddb06ed54acd   4 weeks ago     12.2GB
    psr_gup_04apr24   latest           777063401356   4 weeks ago     12.2GB

where if everything worked your image will be the most recent.

Now we want to convert the docker image to a singularity file, which we 
can do with

    singularity build psr_gpu.sif docker-daemon://image_name:latest

where again `image_name` is the name you gave the docker image.

If that works you will have a singularity file called `psr_gpu.sif` and 
should be good to go!
    


 



