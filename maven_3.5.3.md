## Install `maven` v3.5.3


### Dependencies

* needs jre/1.8.0_162 module for execution

### Downlaod and install

```
mkdir -p /app1/centos6.3/
wget http://www-eu.apache.org/dist/maven/maven-3/3.5.3/binaries/apache-maven-3.5.3-bin.tar.gz
tar xvf apache-maven-3.5.3-bin.tar.gz
mkdir maven
mv apache-maven-3.5.3 maven/3.5.3

```

### Modulefile

below module file is used for canu v1.7

```
#%Module -*****-
##
## modulefile
##
set tool maven
set version 3.5.3
set prefix /app1/centos6.3/${tool}/${version}

proc ModulesHelp { } {
        global version prefix tool
        puts stderr "\tenvironment for Loading the $tool Library for GNU C Compiler"
}

module-whatis   "Loads the enviornment for $tool Library Version $version\n"


if { ![is-loaded jre/1.8.0_162 ] } {
        module load jre/1.8.0_162
}

prereq jre/1.8.0_162

prepend-path        PATH                            ${prefix}/bin

```