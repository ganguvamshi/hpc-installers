## Installing meme suite program

#### Downloading source file

```
cd /app1/bioinfo/source/
wget http://meme-suite.org/meme-software/4.12.0/meme_4.12.0.tar.gz
tar zxf meme_4.12.0.tar.gz
cd meme_4.12.0

```

#### Compile and install

`meme-suite` can be installed with MPI for parallelization. Note that the dreme binary works well only with python2.7

_Compile and Install_

**Requirements**
1. MPI (for parallel)
2. Ghostscript 
3. Python
4. Perl 

```
module load mvapich2-2.3_gnu python2.7 perl5 ghostscript/9.10
./configure --prefix=/app1/bioinfo/meme/4.12.0 --enable-build-libxml2 --enable-build-libxslt --with-url="http://meme-suite.org" --with-db=/hpctmp/biodata/meme --with-contact=nusit-hpc@nus.edu.sg
```
#### Create a Module file

create a text file using `vim` with the below content

```
#%Module -*****-
##
## modulefile
##
set tool meme
set version 4.12.0
set prefix /app1/bioinfo/${tool}/${version}

proc ModulesHelp { } {
        global version prefix tool
        puts stderr "\tenvironment for Loading the $tool Library for GNU C Compiler"
}

module-whatis   "Loads the enviornment for $tool Library Version $version\n"

if { ![is-loaded mvapich2-2.3_gnu ] } {
        module load mvapich2-2.3_gnu
}

if { ![is-loaded perl5 ] } {
        module load perl5
}

if { ![is-loaded python2.7 ] } {
        module load python2.7
}

if { ![is-loaded ghostscript/9.10 ] } {
        module load ghostscript/9.10
}

prereq mvapich2-2.3_gnu
prereq python2.7
prereq perl5
prereq ghostscript/9.10


prepend-path      PATH              ${prefix}/bin



```
now create the module directory for mcl and copy this file

```
mkdir -p /app1/modules/bioinfo/meme
cp mod_meme /app1/modules/bioinfo/meme/4.12.0

```
Now the meme is ready to use via `module`. you can load it using `module load meme/4.12.0`