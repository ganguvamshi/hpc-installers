## Install `lemon` v1.3.1


* load the dependency modules
* build and compile the source


```
module load gcc-7.3.0 cmake/3.9.3 ghostscript/9.10 glpk/4.64
mkdir build
cd build
cmake -DCMAKE_INSTALL_PREFIX=/app1/centos6.3/gnu/lemon/1.3.1 -DBUILD_SHARED_LIBS=TRUE .. -DLEMON_ENABLE_GLPK=YES -DLEMON_DEFAULT_MIP=GLPK -DGLPK_ROOT_DIR=/app1/centos6.3/gnu/glpk/4.64

```