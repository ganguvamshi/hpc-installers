## Installing DFTBPLUS program

#### Downloading source file

```
cd /app1/centos6.3/source/
git clone https://github.com/dftbplus/dftbplus.git
cd dftbplus
git submodule update --init --recursive

```

#### Compile and install

```
./utils/get_opt_externals ALL
cp sys/make.x86_64-linux-intel make.arch
```

change `COMPILE_DFTD3 := 1` and `INSTALLDIR :=$installdirpath` in make.config file

```
module load mvapich2-2.3_gnu python2.7
make -j4
setenv MV2_ENABLE_AFFINITY 0
setenv OMP_NUM_THREADS 1
make test make test TEST_MPI_PROCS=8
make install
```
#### Create a Module file

create a text file using `vim` with the below content

```
#%Module -*****-
##
## modulefile
##
set tool dftplus
set version 18.1
set prefix /app1/centos6.3/gnu

proc ModulesHelp { } {
        global version prefix tool
        puts stderr "\tenvironment for Loading the $tool Library for GNU C Compiler"
}

module-whatis   "Loads the enviornment for $tool Library Version $version\n"

if { ![is-loaded mvapich2-2.3_gnu ] } {
        module load mvapich2-2.3_gnu
}

if { ![is-loaded python2.7 ] } {
        module load python2.7
}

prereq mvapich2-2.3_gnu
prereq python2.7

setenv           MV2_ENABLE_AFFINITY 0
setenv           OMP_NUM_THREADS 1

prepend-path      PATH              ${root}/bin
prepend-path      PYTHONPATH        ${root}/lib/python2.7/site-packages


```
now create the module directory for mcl and copy this file

```
mkdir -p /app1/modules/centos6.3-intel/dftbplus/
cp mod_dftbplus /app1/modules/centos6.3-intel/dftbplus/18.1

```
Now the dftbplus is ready to use via `module`. you can load it using `module load dftpbplus`