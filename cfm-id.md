## Installig cfm-id

cfm-id-code installation on linux is done as guided here: https://sourceforge.net/p/cfm-id/wiki/Home/#on-linux
### Dependencies

```
module load cmake/3.9.3 

```

for module file

```
module load mvapich2_gnu eigen3/3.3.4 boost/1.59.0 liblbfgs/1.10 rdkit/2013_09_1
```

the liblbfgs and lpsolve (`rdkit/2013_09_1`, `liblbfgs/1.10`) will be dynamically linked within cmake command and for the module it is linked manually within the module file.

### Build, compile and Install

clone the cfm code using subversion along with the lpsolve binaries within the cfm directory

```
mkdir /app1/bioinfo/cfm-id-code/
svn checkout svn://svn.code.sf.net/p/cfm-id/code/cfm 2.0
export CFM_ROOT=/app1/bioinfo/cfm-id-code/2.0

# download the lpsolve binary into cfm src directory

mkdir -o $CFM_ROOT/lp_solve55
Download lp_solve_5.5.2.0_dev_ux64.tar.gzz from https://sourceforge.net/projects/lpsolve/files/lpsolve/5.5.2.0
tar xvf lp_solve_5.5.2.0_dev_ux64.tar.gz
```

Now build the cfm from source

```
cd $CFM_ROOT && mkdir build && cd build

export RDBASE=/app1/bioinfo/rdkit/2013_09_1
cmake .. -D INCLUDE_TESTS=ON -D INCLUDE_TRAIN=ON -DLPSOLVE_INCLUDE_DIR=$CFM_ROOT/lp_solve55 -DLPSOLVE_LIBRARY_DIR=$CFM_ROOT/lp_solve55  -DLBFGS_INCLUDE_DIR=/app1/centos6.3/gnu/liblbfgs/1.10/include -DLBFGS_LIBRARY_DIR=/app1/centos6.3/gnu/liblbfgs/1.10/lib -DBOOST_ROOT=/app1/centos6.3/gnu/boost/1.59.0  

make -j10 install
```
### Module file
```
#%Module -*****-
##
## modulefile
##
set tool cfm
set version 2.0
set prefix /app1/bioinfo
set root ${prefix}/${tool}/${version}

proc ModulesHelp { } {
        global version prefix tool
        puts stderr "\tenvironment for Loading the $tool Library for GNU C Compiler"
}

module-whatis   "Loads the enviornment for $tool Library Version $version\n"


if { ![is-loaded mvapich2_gnu ] } {
        module load mvapich2_gnu
}

if { ![is-loaded eigen3/3.3.4 ] } {
        module load eigen3/3.3.4
}

if { ![is-loaded boost/1.59.0 ] } {
        module load boost/1.59.0
}

if { ![is-loaded liblbfgs/1.10 ] } {
        module load liblbfgs/1.10
}

if { ![is-loaded rdkit/2013_09_1 ] } {
        module load rdkit/2013_09_1
}

prereq mvapich2_gnu
prereq eigen3/3.3.4
prereq boost/1.59.0
prereq liblbfgs/1.10
prereq rdkit/2013_09_1


prepend-path            PATH                            ${root}/bin
prepend-path            LD_LIBRARY_PATH                 ${root}/lib
prepend-path            LD_LIBRARY_PATH                 ${root}/lp_solve55
```

