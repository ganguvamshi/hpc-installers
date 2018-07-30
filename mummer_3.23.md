# Mummer 3 installtion

Mummer is a prerequisite for Metassembler. more information about Mummer can be found here: http://mummer.sourceforge.net/

## Downaload 

Mummer is hosted on sourceforge. the source file is downloaded into bioinfo/source directory 

```
cd /app1/bioinfo/source
wget -O MUMmer3.23.tar.gz https://sourceforge.net/projects/mummer/files/mummer/3.23/MUMmer3.23.tar.gz/download
tar -xvf MUMmer3.23.tar.gz

```

## Compiling and installation


```

cp -vR ./MUMMer3.23 /app1/bioinfo/ 
cd /app1/bioinfo/MUMMer3.23
make check
make install

```

## Modulefile

```
#%Module -*****-
##
## modulefile
##
set tool Mummer3
set version 3.23
set prefix /app1/bioinfo/${tool}/${version}

proc ModulesHelp { } {
        global version prefix tool
        puts stderr "\tenvironment for Loading the $tool Library for GNU C Compiler"
}

module-whatis   "Loads the enviornment for $tool Library Version $version\n"


prepend-path        PATH                            ${prefix}

```