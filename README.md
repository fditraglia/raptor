# raptor
Some notes on using Raptor - the UPenn Economics Cluster 

## IP address of the cluster
`raptor.pop.upenn.edu`

## Cluster Details
Raptor is administrated by [Kyle Small](https://www.sas.upenn.edu/computing/people/small). There is no online documentation for Raptor, but it is similar in setup to the smaller student cluster "Hawk" which is documented [here](http://sites.sas.upenn.edu/ks347/book/hawk-cluster). Like Hawk, Raptor is a Sun Grid Engine (SGE) cluster with [Open MPI](https://www.open-mpi.org/) installed.

## Using Rmpi on Raptor
A very good tutorial on using the package [Rmpi](https://cran.r-project.org/) that allows R to communicate with MPI is available [here](http://borisv.lk.net/howtos/grid-mpi-r-howto.html). If you try to install Rmpi from within R on Raptor, however you'll get this error message:

    checking mpi.h usability... no
    checking mpi.h presence... no
    checking for mpi.h... no
    configure: error: "Cannot find mpi.h header file"
    ERROR: configuration failed for package ‘Rmpi’

The problem is that R doesn't know where Open MPI is installed on Raptor. It turns out that it's installed in `usr/global/openmpi`. So to install Rmpi you need to first `wget` the `.tar.gz` containing the package source, and then follow the instructions given [here](http://www.stats.uwo.ca/faculty/yu/Rmpi/install.htm). In particular, once the `.tar.gz` file has been downloaded and is in your home directory:

    R CMD INSTALL Rmpi_0.6-6.tar.gz --configure-args=--with-mpi=/usr/global/openmpi

should work. At this point you can try this [simple example](http://borisv.lk.net/howtos/grid-mpi-r-howto.html) to make sure everything is working correctly.
