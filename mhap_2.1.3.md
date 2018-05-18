## Install `maven` v3.5.3


### Dependencies

* needs jre/1.8.0_162, maven modules for execution

### Downlaod and install

```
DIRPATH="/app1/bioinfo/mhap/2.1.3"
mkdir -p $DIRPATH
wget https://github.com/marbl/MHAP/releases/download/2.1.3/mhap-2.1.3.jar.gz
gunzip mhap-2.1.3.jar.gz

```

### Modulefile

below module file is used for canu v1.7

```
#%Module -*****-
##
## modulefile
##
set tool mhap
set version 2.1.3
set prefix /app1/bioinfo/${tool}/${version}

proc ModulesHelp { } {
        global version prefix tool
        puts stderr "\tenvironment for Loading the $tool Library for GNU C Compiler"
}

module-whatis   "Loads the enviornment for $tool Library Version $version\n"


if { ![is-loaded jre/1.8.0_162 ] } {
        module load jre/1.8.0_162
}

if { ![is-loaded maven/3.5.3 ] } {
        module load maven/3.5.3
}

prereq jre/1.8.0_162
prereq maven/3.5.3

setenv              MHAPJAR                         ${prefix}/mhap-2.1.3.jar
set-alias           mhap                            "java -jar /app1/bioinfo/mhap/2.1.3/mhap-2.1.3.jar"
prepend-path        PATH                            ${prefix}

```