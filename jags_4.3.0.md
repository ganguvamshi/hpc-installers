## Installing JAGS v4.3.0

#### Dependencies

tools needed
* Intel MKL lib


### Downloding source 

```
VERSION=4.3.0
wget -O JAGS-4.3.0.tar.gz  https://downloads.sourceforge.net/project/mcmc-jags/JAGS/4.x/Source/JAGS-4.3.0.tar.gz?r=https%3A%2F%2Fsourceforge.net%2Fprojects%2Fmcmc-jags%2Ffiles%2FJAGS%2F4.x%2FSource%2FJAGS-4.3.0.tar.gz%2Fdownload&ts=1527756650
tar xvf JAGS-4.3.0.tar.gz
cd JAGS-4.3.0
```

### Build and Install
```
./configure --prefix=/app1/centos6.3/gnu/jags/4.3.0  --with-blas="-lmkl_gf_lp64 -lmkl_gnu_thread -lmkl_core -liomp5 -lpthread"
make 
make install

```
### Modulefile

