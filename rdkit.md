## Installing RDkit for installing cfm-id

### Load dependencies

`module load cmake/3.9.3`

No need to load the boost (`boost/1.59.0`) as we are linking it with cmake command

### Build, Compile and Install


```

RDKIT_DIR=/app1/bioinfo/rdkit/2013_09_1

# change the InchiAPI link in External/INCHI-API/download-inchi.sh
cd $RDKIT_DIR/External/INCHI-API
vi download-inchi.sh
# replace the wget line with below
wget http://www.inchi-trust.org/download/104/INCHI-1-API.zip
cd $RDKIT_DIR

mkdir $RDKIT_DIR/build && cd $RDKIT_DIR/build

#cmake -DCMAKE_INSTALL_PREFIX=/app1/bioinfo/rdkit/2018_03 -DBOOST_ROOT=/app1/centos6.3/gnu/boost/1.67_py3 -DBoost_NO_SYSTEM_PATHS=ON  -DRDK_BUILD_INCHI_SUPPORT=ON -DRDK_BUILD_CAIRO_SUPPORT=ON -DBoost_USE_STATIC_LIBS=OFF -DRDK_INSTALL_INTREE=OFF -DRDK_USE_BOOST_SERIALIZATION=on -DRDK_BUILD_AVALON_SUPPORT=ON -DRDK_BUILD_PYTHON_WRAPPERS=OFF -DEIGEN3_INCLUDE_DIR=/app1/centos6.3/gnu/eigen/3.3.4/include/eigen3/ ..


# other command with another boost 
# cmake -DCMAKE_INSTALL_PREFIX=/app1/bioinfo/rdkit/2018_03_2 -DBOOST_ROOT=/app1/centos6.3/gnu/boost/1.67_py27 -DBoost_NO_SYSTEM_PATHS=ON  -DRDK_BUILD_INCHI_SUPPORT=ON -DRDK_BUILD_CAIRO_SUPPORT=ON -DBoost_USE_STATIC_LIBS=OFF -DRDK_INSTALL_INTREE=OFF -DRDK_USE_BOOST_SERIALIZATION=on -DRDK_BUILD_AVALON_SUPPORT=ON -DRDK_BUILD_PYTHON_WRAPPERS=OFF -DEIGEN3_INCLUDE_DIR=/app1/centos6.3/gnu/eigen/3.3.4/include/eigen3/ ..

## Finally this cmake command worked fine
cmake .. -DRDK_BUILD_PYTHON_WRAPPERS=OFF -DRDK_BUILD_INCHI_SUPPORT=ON -DBOOST_ROOT=/app1/centos6.3/gnu/boost/1.59.0 -DEIGEN3_INCLUDE_DIR=/app1/centos6.3/gnu/eigen3/3.3.4/include/eigen3 -DCMAKE_INSTALL_PREFIX=/app1/bioinfo/rdkit/2018_03-install

make -j20
make install 

```
### Module file

module file for rdkit, we need to load only the shared lib dir.

```
#%Module -*****-
##
## modulefile
##
set tool rdkit
set version 2013_09_1
set prefix /app1/bioinfo
set root ${prefix}/${tool}/${version}

proc ModulesHelp { } {
        global version prefix tool
        puts stderr "\tenvironment for Loading the $tool Library for GNU C Compiler"
}

module-whatis   "Loads the enviornment for $tool Library Version $version\n"

prepend-path      LD_LIBRARY_PATH              ${root}/lib

```



### Instatllation Errors

*Tips*
- Remove the SCIlibs paths from CPATH (_see below_)

- **Boost::Python** Error

boost is not properly linked 

`error: ld: cannot find -lBoost::python / lBoost::serialization`

This should possibly be boost_python and boost_serialization. Change them in the link.txt file appropriately. use the below command to change it in all the links files.

`find ./ -name "link.txt" -exec sed -i 's/Boost::/boost_/g' {} \;`

- **Other**

adding this to link.txt helped to makeresolve the error
`-shared -Wl,-soname,libRDKitChemReactions.so.1`



**Status**: Compiling with boost/1.67_py27  



CPATH after excluding SCIlibs :

```
export CPATH="/app1/centos6.3/gnu/boost/1.67_py27/include:/app1/centos6.3/gnu/gcc-7.3.0/lib/gcc/x86_64-pc-linux-gnu/7.3.0/plugin/include:/app1/centos6.3/gnu/gcc-7.3.0/lib/gcc/x86_64-pc-linux-gnu/7.3.0/install-tools/include:/app1/centos6.3/gnu/gcc-7.3.0/lib/gcc/x86_64-pc-linux-gnu/7.3.0/include:/app1/centos6.3/gnu/gcc-7.3.0/include/c++/7.3.0/x86_64-pc-linux-gnu:/app1/centos6.3/gnu/gcc-7.3.0/include/c++/7.3.0:/app1/centos6.3/gnu/gcc-7.3.0/include:/usr/include:/app1/centos6.3/Intel/xe_2015/composer_xe_2015.3.187/ipp/include:/app1/centos6.3/Intel/xe_2015/composer_xe_2015.3.187/mkl/include:/app1/centos6.3/Intel/xe_2015/composer_xe_2015.3.187/tbb/include"

```


